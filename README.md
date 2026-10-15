# HireFlow

HireFlow is a full-stack applicant tracking system for hiring teams. Manage open jobs, organize candidates through a hiring pipeline, schedule interviews, and capture structured feedback in one live workspace.

## Features

- Live candidate pipeline: Applied, Screening, Interview, Offer, Hired, and Rejected
- Job openings with department, location, employment type, and status
- Candidate profiles with contact details, experience, source, and location
- Drag candidates between hiring stages
- Assign applications to recruiters and hiring managers
- Schedule interviews with an interviewer, date, duration, meeting link, and notes
- Structured scorecards for communication, technical skills, problem solving, and culture add
- Candidate recommendations and average interview scores
- Hiring dashboard, candidate search, job list, interview list, and funnel analytics
- Owner, recruiter, hiring manager, and read-only viewer roles
- Responsive interface with readable text sizing
- PostgreSQL-compatible local PGlite database persisted under `server/data`
- Workspace-scoped authenticated Server-Sent Events update the UI without refresh

## Requirements

- Node.js 20.19 or newer
- npm

## Run locally

```bash
npm install
```

Copy `.env.example` to `.env` and set a unique `JWT_SECRET`. Start the app:

```bash
npm run dev
```

Open the Vite address printed in the terminal (usually `http://localhost:5173`). The development runner starts the API on port 4005 and local PGlite storage automatically.

## Demo accounts

All seeded accounts use the password `HireFlow!2026`:

| Role | Email |
| --- | --- |
| Owner | `owner@hireflow.local` |
| Recruiter | `priya@hireflow.local` |
| Recruiter | `jordan@hireflow.local` |
| Hiring manager | `sam@hireflow.local` |
| Read-only viewer | `viewer@hireflow.local` |

## Verify

Run the following with the development stack already running:

```bash
npm run build
npm run test:api
```

The API smoke suite covers authentication and access controls, jobs and candidate CRUD, applications, interview scheduling, scorecards, analytics, and real-time event delivery.

## Stack

- React 19, TypeScript, and Vite
- Node.js, Express 5, Zod validation, and `pg`
- PGlite for persistent local PostgreSQL-compatible storage
- HTTP-only JWT session cookies
- Server-Sent Events for live board updates

## API overview

- `GET /api/health`
- `POST /api/auth/login`, `GET /api/auth/me`, `POST /api/auth/logout`
- `GET /api/dashboard`, `GET /api/team`
- `GET /api/jobs`, `POST /api/jobs`, `PATCH /api/jobs/:id`, `DELETE /api/jobs/:id`
- `GET /api/candidates`, `POST /api/candidates`, `PATCH /api/candidates/:id`, `DELETE /api/candidates/:id`
- `GET /api/applications`, `GET /api/applications/:id`, `PATCH /api/applications/:id`, `DELETE /api/applications/:id`
- `POST /api/applications/:id/interviews`, `PATCH /api/interviews/:id`
- `POST /api/applications/:id/scorecards`
- `GET /api/events` (authenticated SSE stream)

Keep `.env` and `server/data` out of source control. For production, use a managed PostgreSQL service and a strong secret.
