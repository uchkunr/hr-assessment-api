# HR Candidate Screening API (hr-assessment-api)

A high-performance REST API gateway designed for managing, distributing, and analyzing candidate personality and cognitive screening assessments. Built using the Bun runtime, Elysia.js web framework, and Prisma ORM.

## Key Features

- **Candidate Assessment Workflows**: Create and send specific assessment links to candidates.
- **Dynamic PDF Report Generation**: Utilizes Puppeteer to generate visual, formatted screening result sheets in PDF format.
- **JWT Authorization**: Route-level security with JSON Web Token parsing and verification.
- **SMTP Email Notifications**: Automated delivery of assessment links to candidates via configured mail accounts.
- **Database Architecture**: Powered by PostgreSQL with automated model mappings via Prisma ORM.
- **Highly Performance-Optimized**: Runs on Bun and compiles down to clean, minified executable binaries during production builds.

---

## Tech Stack

- **Runtime**: Bun (>= 1.1)
- **Framework**: Elysia.js (v1.4)
- **Database**: PostgreSQL (via Prisma ORM)
- **Reporting Engine**: Puppeteer (Headless Chrome)
- **Notifications**: Nodemailer

---

## Getting Started

### Prerequisites

- Bun installed locally (e.g. `curl -fsSL https://bun.sh/install | bash`)
- Running PostgreSQL database instance
- Local Google Chrome or Chromium (optional, for Puppeteer execution)

### Configuration

Copy `.env.example` to `.env` and fill out the configuration variables:

```bash
cp .env.example .env
```

Ensure the following variables are specified:

- `DATABASE_URL`: Your PostgreSQL connection string.
- `JWT_SECRET`: Secret token for JWT payload signing.
- `GMAIL_USER` & `GMAIL_PASS`: Nodemailer authentication details for link distribution.
- `SMTP_HOST` & `SMTP_PORT`: Mail server connection details.
- `CORS_ORIGIN`: Allowed origin URL for client UI requests.

### Database Setup

Run Prisma migrations or push schemas directly to sync the database:

```bash
bunx prisma db push
```

Generate the Prisma Client models:

```bash
bunx prisma generate
```

### Running Locally

Start the development server with watch mode enabled:

```bash
bun run dev
```

The API will start running at `http://localhost:3000` (or your configured `PORT`).

---

## Running with Docker

You can launch the entire ecosystem (Elysia API and PostgreSQL database) using Docker Compose.

1. Ensure your host `.env` is configured with credentials.
2. Build and start the containers:

```bash
docker compose up -d --build
```

This starts:

- **`hr-assessment-api`**: Running the compiled API binary on port `3000`.
- **`hr-assessment-db`**: Running PostgreSQL 16 on port `5432` with automated health checks.

---

## API Router Details

The API exposes endpoints prefixed under `/api/v1`:

- **Auth Routes** (Public): `POST /api/v1/auth/register`, `POST /api/v1/auth/login`
- **Candidate Assessment Actions**:
  - `POST /api/v1/assignments` - Create new assessments.
  - `GET /api/v1/questions` - Retrieve test questionnaire.
  - `POST /api/v1/universal-links` - Retrieve or set up universal screening links.
  - `GET /api/v1/result/:id/pdf` - Generates and returns a Puppeteer-rendered PDF document representing the candidate's traits charts.

---

## Project Structure

```
├── Dockerfile
├── docker-compose.yml
├── package.json
├── tsconfig.json
├── prisma
│   └── schema.prisma        # Database schema definitions and model properties
└── src
    ├── index.ts             # Elysia app router, middleware pipelines, and CORS setup
    └── modules
        ├── auth             # Registration and login actions
        ├── helpers          # Passwords, logger, JWT configuration, and SMTP setup
        ├── result           # PDF rendering and score calculation business logic
        └── user             # User administration endpoints
```
