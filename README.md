# BugSquash – Full-Stack Bug Tracking System

A complete SPA and RESTful application for collaborative bug management.

---

## Overview

BugSquash is a full-stack web application designed to manage bugs inside software development projects. It enables team members to report issues, assign responsibilities, collaborate efficiently, and track the entire lifecycle of a bug.

The platform includes:

* A RESTful backend built in Node.js
* A Single Page Application frontend built with React.js
* A relational database accessed through an ORM
* Integration with GitHub/GitLab APIs for commit validation
* Deployment on a free-tier hosting environment

The project brings together all documentation and development requirements into a coherent system.

---

## General Objective

The goal is to build a fully functional, realistic web application consisting of:

* A SPA frontend suitable for desktop, tablet, and mobile
* A RESTful backend connected to a relational database
* Integration with an external service for commit verification
* A permission system for different project roles
* A structured development workflow from documentation to full implementation

---

## Technology Stack

| Layer            | Requirement                 | Implementation                  |
| ---------------- | --------------------------- | ------------------------------- |
| Frontend         | Component-based SPA         | React.js                        |
| Backend          | Node.js with REST interface | Node.js + Express               |
| Database         | Relational database         | PostgreSQL                      |
| Persistence      | ORM                         | Sequelize                       |
| External Service | Commit validation           | GitHub or GitLab API            |
| Version Control  | Git                         | GitHub                          |
| Deployment       | Free-tier hosting           | Render / Vercel / Railway, etc. |

---

## Functional Description

### Authentication

* Email-based registration and login
* Token-based session handling
* Roles associated with project membership

### Project Management

* Users can create software projects to be monitored
* Projects include descriptions, repository URLs, and team members
* Other users may join projects as testers
* Project members manage the configuration and oversight of the project

### Bug Management

* Testers can submit bugs with:

  * Severity
  * Priority
  * Description
  * Commit link where the bug was identified

* Project members can:

  * View bugs associated with their projects
  * Assign themselves to a bug
  * Update the status of a bug after resolving it
  * Add the commit link used for the fix

### Permission System

| Action                  | Required Role            |
| ----------------------- | ------------------------ |
| Add or modify a project | Project Member (Manager) |
| Add a bug               | Tester                   |
| Assign a bug            | Project Member           |
| Update bug status       | Project Member           |
| View bugs               | Project Member or Tester |

---

## Data Model (ORM)

### Entities

**User**

* id
* email
* password_hash
* name
* global role

**Project**

* id
* name
* description
* repository_url

**ProjectMember**

* project_id
* user_id
* role (Manager or Tester)

**Bug**

* id
* project_id
* reporter_id
* assigned_to_id
* severity
* priority
* status
* description
* opened_commit_link
* resolution_commit_link

### Relationships

* User to Project: Many-to-Many through ProjectMember
* Project to Bug: One-to-Many
* User to Bug (reporter): One-to-Many
* User to Bug (assigned): One-to-Many

---

## REST API Overview

All routes use the `/api` prefix.

### Authentication Routes

| Method | Route              | Description            |
| ------ | ------------------ | ---------------------- |
| POST   | /api/auth/login    | Login                  |
| POST   | /api/auth/register | Register               |
| GET    | /api/users/me      | Get authenticated user |

### Project Routes

| Method | Route                     | Description     |
| ------ | ------------------------- | --------------- |
| POST   | /api/projects             | Create project  |
| GET    | /api/projects             | List projects   |
| GET    | /api/projects/:id         | Project details |
| PUT    | /api/projects/:id         | Update project  |
| POST   | /api/projects/:id/testers | Join as tester  |

### Bug Routes

| Method | Route                         | Description       |
| ------ | ----------------------------- | ----------------- |
| POST   | /api/bugs                     | Create bug        |
| GET    | /api/projects/:projectId/bugs | List project bugs |
| PATCH  | /api/bugs/:bugId/assign       | Assign bug        |
| PATCH  | /api/bugs/:bugId/status       | Update bug status |

---

## External Service Integration

The backend validates commit links using the GitHub or GitLab API.

When a bug is created:

1. The project, repository, and commit SHA are parsed from the commit link.

2. The backend calls:

   ```
   GET /repos/{owner}/{repo}/commits/{sha}
   ```

3. The service confirms that the commit exists.

4. Metadata may be retrieved and stored as needed.

The same procedure applies when updating a bug with a resolution commit link.

---

## Project Timeline

### Stage 1 – Documentation and Setup

Deadline: 16.11.2025
Deliverables:

* Specifications
* Project plan
* Repository initialization

### Stage 2 – RESTful Backend

Deadline: 06.12.2025
Deliverables:

* Backend code
* ORM models and database setup
* Authentication and authorization
* External API integration
* Backend run instructions

### Stage 3 – Complete Application

Deadline: Final seminar
Deliverables:

* Full frontend SPA
* Integration with backend
* Interface with forms, dashboards, and routing
* Deployment
* Final demonstration

---

## Code Quality and Standards

* Clear project organization
* Consistent naming conventions and formatting
* Descriptive variable and function names
* Documented classes and functions
* Incremental Git commits with meaningful messages
* Coherent business logic

Optional:

* Automated tests
* Test coverage metrics

---

## Deployment

The project is intended to be deployed on free-tier hosting platforms, for example:

* Frontend: Vercel, Netlify
* Backend: Render, Railway, Fly.io
* Database: Supabase, Neon, ElephantSQL

Deployment is required as part of the final project stage.

---

## Example Use Cases

* A tester submits a bug describing the issue and the commit where it was found.
* A project member assigns the bug to themselves.
* The project member resolves the bug and updates the status with a fix commit link.
* Team members can monitor bug progress and project status through the interface.

---

## Conclusion

BugSquash provides a structured and modern approach to bug tracking through a full-stack architecture. With a React frontend, Node.js backend, relational database, and commit verification integration, it delivers a complete and scalable system suitable for real-world project environments.

