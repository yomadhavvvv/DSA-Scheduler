# DSA Revision Platform

A full-stack application for organizing personal Data Structures and Algorithms (DSA) practice, tracking attempts, and helping learners revisit previously solved problems.

**Author:** Madhav Kumar

## Overview

Students often solve DSA problems but struggle to revisit them consistently. This application provides a personal problem library, records practice attempts, and surfaces problems for review. Topic-level progress information helps users identify areas that may need more practice.

## Features

- **Personal problem library:** Add and manage DSA problems for individual practice.
- **Problem deduplication:** Identify duplicate problems using canonical URLs and slugs.
- **Revision queue:** Surface problems for review based on their stored scheduling information.
- **Submission history:** Record attempts and display a history for each problem.
- **Progress tracking:** View topic-level statistics and problem coverage.
- **Authentication:** Protect user-specific functionality with JWT-based authentication and password hashing.
- **REST API:** Backend endpoints support problem management, submissions, revision information, and user progress.

## Technology Stack

| Layer | Technologies |
|---|---|
| Frontend | React, TypeScript, Vite |
| Backend | Python, FastAPI |
| Database and ORM | PostgreSQL, SQLAlchemy |
| Authentication | JWT, bcrypt password hashing |
| Database migrations | Alembic |
| Containerization | Docker, Docker Compose |

## Architecture

The application separates the frontend, API backend, and relational database.

```text
React + TypeScript frontend
          |
          | HTTP / REST
          v
      FastAPI backend
          |
          | SQLAlchemy
          v
       PostgreSQL
          |
          v
     Alembic migrations
```

- The frontend provides the interface for managing problems and reviewing progress.
- FastAPI handles application endpoints, request validation, and user-specific operations.
- SQLAlchemy maps application entities to PostgreSQL tables.
- Alembic manages database schema migrations.
- Docker Compose provides a repeatable local development environment.

## Core Workflows

### 1. Manage a personal problem library

Users can add DSA problems and maintain their own practice collection. Canonical URL and slug handling helps prevent duplicate entries.

### 2. Record practice attempts

The application stores submission records and makes attempt history available alongside problem information.

**Current limitation:** The supplied implementation does not execute submitted source code against test cases. Stored verdicts should not be interpreted as independently verified online-judge results. Integrating a code-execution service is a future improvement.

### 3. Review problems

The application maintains review scheduling information and generates a queue of problems due for revision. The current scheduling logic uses interval-based updates and should not be described as a complete SM-2 implementation.

### 4. Track progress

The frontend presents topic-level progress information to help users understand their practice coverage and identify areas that may need more attention.

## Backend and Data Engineering

The backend uses a relational PostgreSQL database accessed through SQLAlchemy. Database schema changes are managed with Alembic migrations. Authentication uses JWTs, while passwords are stored using bcrypt hashing rather than plaintext.

The API is organized around application resources such as problems, submissions, revision information, and user progress.

## Getting Started

### Prerequisites

- Python version supported by the backend dependencies
- Node.js and npm
- PostgreSQL, or Docker with Docker Compose
- Git

### 1. Clone the repository

```bash
git clone https://github.com/yomadhavvvv/DSA-Scheduler.git
cd DSA-Scheduler/dsa-revision-platform-main/dsa-revision-platform-main
```

### 2. Configure environment variables

Create the environment files expected by the backend and Docker Compose configuration. Set the database connection details and a strong application secret key.

Do not commit `.env` files, database passwords, JWT secrets, or other credentials.

### 3. Start the application

If using Docker Compose, run the command from the directory containing `docker-compose.yml`:

```bash
docker compose up --build
```

For manual setup, install the backend dependencies, configure PostgreSQL, apply the Alembic migrations, and start the FastAPI application. Then install the frontend dependencies and start the Vite development server.

Refer to the backend and frontend project directories for their dependency files and exact scripts.

## Testing

The repository includes backend and frontend test-related configuration. Run the available tests using the commands and dependencies specified by the project.

```bash
# Backend (from the backend directory, with dependencies installed)
pytest

# Frontend (from the frontend directory)
npm test
```

A successful test run depends on the required environment variables and test database/configuration being available.

## Current Limitations and Future Improvements

- Integrate a real code-execution service and evaluate submissions against test cases.
- Strengthen validation and error handling around submission and revision workflows.
- Expand automated tests for authentication, API behavior, and scheduling edge cases.
- Ensure progress analytics are correctly scoped to the current user's problem library.
- Further refine the scheduling logic and document the algorithm with tests and examples.

## Security Notes

- Keep secrets in environment variables or a hosting platform's secret manager.
- Never commit API keys, database passwords, or JWT signing secrets.
- Use a separate test database for automated tests.
- Treat code execution as an untrusted workload. If an execution service is added, use an isolated sandbox with resource limits.

## Author

**Madhav Kumar**
