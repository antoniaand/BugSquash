# Detailed Specifications - BUG SQUASH

## 1. Relational Data Model (Database/ORM)

This model defines the structure of data stored in the relational database, to be implemented using an ORM (Sequelize or TypeORM).

### Entities (Tables) and Attributes

| Entity | Attribute | Data Type | Details/Relationships |
| :---: | :---: | :---: | :---: |
| User | id | UUID/INT | Primary Key (PK) |
| | email | String | UNIQUE, used for authentication |
| | password\_hash | String | Hashed password |
| | name | String | Full name of the user |
| | role | Enum/String | Global role: 'STUDENT', 'ADMIN', etc. (Default: 'STUDENT') |
| Project | id | UUID/INT | PK |
| | name | String | Project name |
| | description | Text | Project description |
| | repository\_url | String | Link to the Git repository (GitHub/GitLab) |
| ProjectMember | project\_id | INT | Primary Key (PK) & Foreign Key (FK) to Project.id |
| | user\_id | INT | PK & FK to User.id |
| | role | Enum/String | 'MANAGER' or 'TESTER' (Defines role within the project) |
| Bug | id | UUID/INT | PK |
| | project\_id | INT | FK to Project.id |
| | reporter\_id | INT | FK to User.id (reported by) |
| | assigned\_to\_id | INT | FK to User.id (allocated for resolution). Can be NULL. |
| | severity | Enum/String | 'Low', 'Medium', 'High', 'Critical' |
| | priority | Enum/String | 'Low', 'Medium', 'High', 'Urgent' |
| | status | Enum/String | 'New', 'InProgress', 'Fixed', 'Verified', 'Closed' |
| | description | Text | Detailed bug description |
| | opened\_commit\_link | String | Link to the commit where the bug was found |
| | resolution\_commit\_link | String | Link to the resolution commit. Can be NULL. |

### Relationships

* User - Project (via ProjectMember): Many-to-Many
* Project - Bug: One-to-Many
* User - Bug (Reporter): One-to-Many
* User - Bug (Assigned): One-to-Many

---

## 2. RESTful Interface Design (API Endpoints)

The RESTful interface will be built using Node.js and Express. All routes will start with the `/api` prefix.

### 2.1. Authentication and User Routes

| Objective | HTTP Method | URI (Route) | Permissions |
| :---: | :---: | :---: | :---: |
| Login | POST | /api/auth/login | PUBLIC |
| Register | POST | /api/auth/register | PUBLIC |
| User Details | GET | /api/users/me | AUTHENTICATED |

### 2.2. Project Management Routes

| Objective | HTTP Method | URI (Route) | Permissions |
| :---: | :---: | :---: | :---: |
| Create Project | POST | /api/projects | AUTHENTICATED (User becomes MANAGER) |
| Get Project Details | GET | /api/projects/:id | PROJECT\_MEMBER |
| Modify Project | PUT | /api/projects/:id | PROJECT\_MANAGER |
| List Projects | GET | /api/projects | AUTHENTICATED |
| Register as Tester | POST | /api/projects/:id/testers | AUTHENTICATED (non-member) |

### 2.3. Bug Management Routes

| Objective | HTTP Method | URI (Route) | Permissions |
| :---: | :---: | :---: | :---: |
| Register Bug | POST | /api/bugs | TESTER |
| List Project Bugs | GET | /api/projects/:projectId/bugs | PROJECT\_MEMBER |
| Assign Bug (to self) | PATCH | /api/bugs/:bugId/assign | PROJECT\_MANAGER |
| Update Status | PATCH | /api/bugs/:bugId/status | PROJECT\_MANAGER |

---

## 3. External Service Integration

The application will use an external service to handle source code information.

### Selected External Service: GitHub API (or GitLab API)

Purpose: Validating and extracting metadata about the commit links provided when a bug is reported or resolved.

External API Route (GitHub Example):

* Endpoint: GET /repos/{owner}/{repo}/commits/{sha}
* Usage:
    1.  When a **TESTER** registers a **Bug**, the backend extracts the owner, repo, and sha from the `opened_commit_link`.
    2.  The backend makes a call to the **GitHub API** to verify the commit exists and retrieve details like the commit date.
    3.  The same logic applies when updating the status with the `resolution_commit_link`.

---

## 4. Permissions System (Authorization)

Permissions will be managed based on the user's defined role within the specific project (`role` attribute in the **ProjectMember** table).

| Action | Permission Condition |
| :---: | :---: |
| Register Project | User is creating the project and is set as a **MANAGER** for that project. |
| Add Bug | User has the **TESTER** role for the project. |
| View Bugs/Projects | User has the **MANAGER** or **TESTER** role for the project (**PROJECT\_MEMBER**). |
| Assign/Update Bug | User has the **MANAGER** role for the project (**PROJECT\_MANAGER**). |