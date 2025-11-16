# Project Plan - Bug Tracker Application

---

## 1. General Objective

[cite_start]To develop a **full-stack application** (SPA + RESTful Backend) for bug management, meeting all technological constraints and minimum functionality requirements.

---

## 2. Technology Stack (Constraints and Choices)

[cite_start]Acest tabel detaliază alegerea tehnologiilor pentru fiecare componentă a aplicației.

| Component | Required Technology | Chosen Technology |
| :---: | :---: | :---: |
| **Backend** | Node.js (REST Interface) | Node.js + Express (for a fast, minimal API) |
| **Database** | Relational | PostgreSQL (robust, open-source relational database) |
| **ORM** | ORM (Persistence API) | Sequelize (mature and well-documented ORM for Node.js) |
| **Frontend** | Component-based Framework | React.js (covered in the course, excellent for SPAs) |
| **Version Control** | Git | Git & GitHub/GitLab |

---

## 3. Timeline and Deliverables

[cite_start]The project is divided into three stages, aligning with the required delivery dates.

### Stage 1: Documentation and Setup (Deadline: 16.11.2025)

[cite_start]Deliverable: `SPECIFICATII.md`, `PLAN_PROIECT.md` files, and an initialized Git repository.

| # | Task | Status |
| :-: | :---: | :---: |
| 1.1 | Git Set-up: Create GitHub/GitLab repository, initialize local Git. | Completed |
| 1.2 | Project Structure: Create `backend/`, `frontend/`, `docs/` folders. | Completed |
| 1.3 | Data Modeling: Define entities, attributes, and relationships (see `SPECIFICATII.md`). | PENDING |
| 1.4 | API Design: Define RESTful routes (URIs, HTTP Methods, Permissions). | PENDING |
| 1.5 | External Service: Select and specify integration method with GitHub/GitLab API. | PENDING |
| 1.6 | Planning: Write this project plan, select technology stack. | PENDING |
| 1.7 | Commit: Final commit containing all documentation files in the `docs/` folder. | PENDING |

---

### Stage 2: Functional RESTful Service (Deadline: 06.12.2025)

[cite_start]Deliverable: Complete functional backend code, accessing the DB and External Service, with clear running instructions.

| # | Task | Priority |
| :-: | :---: | :---: |
| 2.1 | Backend Setup: Initialize Node.js, configure Express, Sequelize/TypeORM. | MAX |
| 2.2 | Database Models: Create ORM models and migration scripts for tables. | MAX |
| 2.3 | Authentication: Implement login/registration (with password hashing) and authorization/permissions middleware. | MAX |
| 2.4 | Core Routes: Implement Project and Bug REST routes (Create, List, Assign, Status Update). | MAX |
| 2.5 | External Integration: Logic to call the GitHub/GitLab API upon bug reporting/resolution. | HIGH |
| 2.6 | Instructions: Create `backend/README.md` with clear running instructions (dependencies, env variables, commands). | MAX |

---

### Stage 3: Complete Application (Deadline: Last Seminar)

[cite_start]Deliverable: Complete Front-end (SPA) application, integrated with the Backend, ready for demo.

| # | Task | Priority |
| :-: | :---: | :---: |
| 3.1 | Frontend Setup: Initialize the React.js project structure. | MAX |
| 3.2 | UI & Style: Implement responsive design (desktop/mobile/tablet) using Tailwind CSS/Custom CSS. | HIGH |
| 3.3 | Login/Dashboard Components: Create authentication pages and the main project dashboard. | MAX |
| 3.4 | Management Components: Create forms and components for Project CRUD and Bug CRUD (listing, detail, assignment). | MAX |
| 3.5 | Frontend Services: Implement services to make HTTP calls to the Backend API. | MAX |
| 3.6 | Routing: Configure navigation within the SPA. | MAX |
| 3.7 | Demo & Deployment: Prepare for the final demo and deployment on a free-tier server. | MAX |