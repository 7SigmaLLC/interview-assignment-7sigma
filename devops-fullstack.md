# 7Sigma Full-Stack + DevOps Web Application Assessment

## Overview

Create a full-stack web application that demonstrates DevOps & Fullstack proficiency. The app should:

1. Authenticate users via Google OAuth 2.0 (using your own GCP credentials).
2. Allow authenticated users to create, read, and delete TODO items stored in Google Cloud SQL (Postgres).
3. Automatically delete any TODO items older than 2 minutes using a scheduled Cloud Function.
4. Use a trpc or OpenAPI-defined backend with auto-generated TypeScript SDK for frontend.
5. Deploy the application to Google Cloud Run for external demo access.
6. Implement basic multitenancy support (each user belongs to a predefined org via email domain).
7. Maintain communication throughout the test – confirm scope, ask clarifying questions, and share updates regularly via an agreed upon messaging channel.

---

## Deliverables

- A private Git repository (invite @robertjchristian)
- A Loom video walkthrough
- README with setup instructions, architecture explanation, and DevOps documentation
- Usable demo with public URL (cloudrun url)
- Optional: Infrastructure provisioning via Pulumi or Google Cloud CLI

---

## Tech Stack

### Frontend:
- TypeScript + React (no strict UI library requirement)
- TypeScript SDK (auto-generated from OpenAPI)
- Should be implemented as part of a monorepo

### Backend:
- Fastify with OpenAPI route definitions
- tRPC (used in limited scope to demonstrate typed procedure calls)
- Google Cloud:
  - OAuth 2.0
  - Cloud SQL (Postgres) for TODO storage
  - Cloud Functions (scheduled job to delete TODOs older than 2 minutes)
  - Cloud Run (for deployment)
- WebSockets (optional) for real-time updates
- Optional: Pulumi or gcloud CLI for infrastructure provisioning

---

## Functional Requirements

### Authentication & Security

- Implement Google OAuth login
- Securely store and retrieve tokens (JWT/session/cookie-based) - login/logout functions
- Store all secrets in Google Secret Manager and document setup in README
- Protect all routes with authentication
- Restrict access based on tenant org (users must belong to a provisioned org such as @7sigma.io)
  

### TODO List Functionality

- Authenticated users can create, view, and delete TODO items
- Store TODOs in Google Cloud SQL (Postgres)
- Each TODO should be associated with a user and tenant org
  - TODO list is per org, not per user.  Assign each user to two orgs for demonstrating.

### Automated Cleanup with Cloud Functions

- A scheduled Cloud Function should delete TODOs older than 2 minutes
- Use structured logging (JSON preferred) for observability
- Document how this cleanup works in the README

---

## DevOps Requirements

### Secrets Management

- Secrets (OAuth credentials, DB creds, etc.) must be stored in Google Secret Manager
- App must fetch secrets securely at startup or on-demand
- README should include:
  - Secret names used
  - Access method
  - Rotation strategy if applicable

### Infrastructure Provisioning (Recommended)

- Use Pulumi (TypeScript) or Google Cloud CLI scripts to provision:
  - OAuth consent screen
  - Cloud SQL instance
  - Secret Manager entries
  - Cloud Function for cleanup
  - Cloud Run deployment target
- Document all setup steps and assumptions in the README

### Logging & Observability

- Use structured logging throughout backend and functions (pino)
- Mention how to view logs in Google Cloud Console

### IAM & Permissions

- Document required GCP IAM roles for service accounts
- Ensure roles follow least privilege principles

### CI/CD (Bonus)

- Include a GitHub Actions or similar pipeline that:
  - Lints or type-checks code
  - Optionally deploys Cloud Functions and Cloud Run
  - Runs basic tests if applicable

---

## UI Requirements

- Dashboard page post-login:
  - Display list of TODOs
  - Ability to add or delete TODOs
  - Show timestamps and TTL status

---

## Loom Video Walkthrough (Required)

- Demonstrate the working app (end-to-end flow)
- Show secure secret handling
- Walk through project structure (monorepo, backend/frontend separation, etc.)
- Show deployment to Cloud Run
- Show scheduled Cloud Function deleting expired TODOs
- Discuss design tradeoffs and DevOps setup (manual or scripted)

---

## Evaluation Criteria

### Level 1: Basic
- OAuth login works
- Users can add/view TODOs
- TODOs stored in Cloud SQL
- Cloud Function deletes old TODOs

### Level 2: Intermediate
- OpenAPI + SDK generation
- tRPC integrated
- Secure secret handling via Secret Manager
- Cloud Run deployment
- Multitenant filtering by email/org

### Level 3: Advanced
- Infra provisioning with Pulumi/gcloud
- Structured logging and traceability
- IAM roles documented and minimized
- Full monorepo with CI/CD pipeline (git actions / husky minimum)
- Real-time UI updates and solid error handling

---

## Timeframe
- Aim to spend about one week on this.
- If you can’t complete everything, focus on a smaller scope but keep the code and scripts well structured.
- Focus on clean architecture, working deployment, and documentation

---

## Communication

Please maintain regular communication throughout the test. Confirm scope, ask clarifying questions, and share updates in your preferred messaging channel. This is part of the evaluation – simulating real-world async team collaboration.

Timeframe
Aim to spend about one week on this.
If you can’t complete everything, focus on a smaller scope but keep the code well structured.
⸻

Good Luck!

This assignment is meant to simulate a real-world environment with multiple moving parts. It’s not easily solved with simple AI prompts alone — setup, debugging, and design decisions will require genuine problem-solving. It's okay if not everything is implemented within the time allotted. This is measured on a curve. We do consider the state of the art LLMs at the time of this writing, and expect you to take full advantage of available AI tools.

We look forward to seeing your approach, design, and final product.
