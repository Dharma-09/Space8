# spaceM8

spaceM8 is a full‑stack web application that helps roommates manage shared living tasks such as space setup, chores, announcements, grocery lists, and shared expenses in one place.[file:1]

## Features

- Secure authentication (register, login, JWT, forgot/reset password).[file:1]
- Create and join spaces via unique space codes.[file:1]
- Manage space members and their profiles.[file:1]
- Create, assign, update, finish, and delete tasks for roommates.[file:1]
- Post and manage space‑wide announcements.[file:1]
- Shared grocery lists with items, quantities, and purchased status.[file:1]
- Track shared expenses, split amounts between participants, and record settle‑ups.[file:1]
- View recent expense and settle‑up activities per space.[file:1]

## Tech Stack

**Frontend**

- Next.js (React framework)
- TypeScript
- Tailwind CSS
- ShadcnUI components[file:1]

**Backend**

- Java
- Spring Boot (REST APIs, security, data access)[file:1]

**Database**

- MySQL (relational database for all core entities)[file:1]

**Authentication & Security**

- JWT for stateless authentication and session management
- BCrypt for password hashing
- Route protection with Spring Security/WebConfig
- GDPR‑oriented data protection practices[file:1]

**DevOps & Tooling**

- Docker for containerization (frontend and backend)
- GitLab CI/CD pipelines
- Postman for API testing
- JUnit & Mockito for automated testing
- Testcontainers for integration tests
- VS Code as primary IDE[file:1]

## Architecture

spaceM8 follows a client–server architecture:

- **Frontend (Next.js)** renders the UI and calls backend APIs using the JWT stored in local storage.[file:1]
- **Backend (Spring Boot)** exposes REST endpoints for authentication, spaces, tasks, announcements, groceries, expenses, settle‑ups, activities, and profiles.[file:1]
- **Database (MySQL)** stores users, spaces, tasks, expenses, grocery lists, activity logs, etc.[file:1]

Core entities include:

- `User`, `Space`, `UserSpace`
- `Task`, `Announcement`
- `Expense`, `Participant`, `SettleUp`, `Activity`
- `Grocery`, `GroceryItems`
- `PasswordResetToken`[file:1]

## How It Works

1. A user registers or logs in with email and password.
2. The backend validates credentials and returns a JWT that encodes user and space details.[file:1]
3. The frontend stores the JWT (e.g., local storage) and attaches it to each API request.
4. The backend validates the token, executes business logic, and persists data in MySQL.[file:1]

Example user flows:

- **Space setup:** Create a space, share the code, roommates join using the code, and members list is updated.[file:1]
- **Tasks:** Create a task for a space, assign it to a roommate, mark it as finished when done.[file:1]
- **Expenses:** Add an expense, select participants, the backend automatically splits the amount and creates participant records and activities.[file:1]
- **Settle‑up:** Use the calculations endpoint to see who owes whom, then record settle‑up payments.[file:1]

## API Overview

Some representative endpoints:

- `POST /api/v1/auth/register` – register a new user
- `POST /api/v1/auth/login` – login and receive JWT
- `POST /api/v1/space/create` – create a new space
- `POST /api/v1/space/join` – join space by code
- `GET /task/get-all` – list all tasks for current space
- `POST /api/v1/expense/add` – add an expense with participants
- `GET /api/v1/settleup/calculations` – get who‑owes‑whom calculations
- `GET /api/v1/activity/all` – view activity history for space[file:1]

(See API docs section of the technical design document or backend code for the complete list.)[file:1]

## Running Locally

> The commands and environment variables here are examples; adjust them to match your actual repository structure and Docker setup.[file:1]

### Prerequisites

- Docker and Docker Compose
- Java 17+
- Node.js (LTS) + npm or yarn
- MySQL (local or Docker) if not using the DB container[file:1]

### Option 1: Docker Compose

```bash
# From project root
docker compose up --build
