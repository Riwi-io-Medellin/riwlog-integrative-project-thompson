# Riwlog Integrative Project: Problem Catalog & Code Classifier

An integrative full-stack platform for generating, classifying, and solving programming problems. The system features an AI-driven problem evaluation engine, a robust catalog backend, and a modern frontend code editor.

## Project Architecture

This repository is split into three main microservices:

1. **Frontend (`/frontend`)**: A vanilla JavaScript single-page application built with Vite, utilizing modern web standards. It features Tailwind CSS v4, CodeMirror for code editing, and Playwright for end-to-end testing.
2. **Backend (`/backend`)**: A robust REST API running on [Bun](https://bun.sh/) and Express. Handles data persistence with PostgreSQL via Kysely, user authentication, leaderboards, and OpenAPI/Swagger documentation generation using Zod.
3. **AI Provider API (`/api`)**: A Python-based FastAPI microservice that utilizes OpenAI and Google GenAI models for problem classification, generation, and automated code evaluation.

## Technologies Used

* **Frontend**: Vanilla JS, Vite 8, Tailwind v4, CodeMirror, Playwright, Bun.
* **Backend**: Bun, Express, PostgreSQL, Kysely, Zod schemas, Pino logging.
* **AI Service**: Python, FastAPI, OpenAI API, Google GenAI API, Pydantic.
* **Deployment**: Docker & Docker Compose (Render configs available for AI service).

## Getting Started

### Prerequisites

Ensure you have the following installed on your local machine:
* [Bun](https://bun.sh/) (v1.3.9+)
* [Python](https://www.python.org/) 3.10+
* Docker & Docker Compose (for database and container orchestration)
* Node.js (optional, but recommended as a fallback alongside Bun)

### 1. Database Setup
Ensure you have a local PostgreSQL instance running or start one up using Docker.
Configuration defaults to standard local postgres settings, or you can supply custom `.env` files.

### 2. Backend Setup
The backend runs on Bun.

```bash
cd backend
bun install
# Run database migrations
bun run db:migrate
# Start the development server
bun run dev
```

### 3. AI API Setup
The Python classification service runs via FastAPI.

```bash
cd api
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
./start.sh # Or run: fastapi dev main.py
```
*(Make sure to configure `.env` with your `OPENAI_API_KEY` or `GOOGLE_API_KEY` as needed).*

### 4. Frontend Setup
The frontend uses Bun as the package manager and Vite for development.

```bash
cd frontend
bun install
# Start the Vite development server
bun run dev
```

## Testing

Each service maintains its own test suite:

* **Backend**: `bun run test` (uses memory store or supply `STORE_PROVIDER=postgres` for DB).
* **Frontend**: 
  * Unit Tests: `bun run test`
  * E2E Tests: `bun run test:e2e` (Uses Playwright)

## Docker Deployment

Every service contains a `Dockerfile` for easy containerization. 
You can build and run individual services:
```bash
docker build -t riwlog-frontend ./frontend
docker build -t riwlog-backend ./backend
docker build -t riwlog-ai-api ./api
```

## Documentation

* Detailed API Endpoints contract: `backend/docs/api-contract.md`
* Backend Admin functions: `backend/docs/admin-endpoints.md`
* You can generate a live openapi spec by running `bun run export:openapi` in the backend directory.

## License
This project is proprietary and confidential unless stated otherwise.
