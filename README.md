# GrievanceOps – AI-Powered IT Service Management Platform

A full-stack IT Service management system that uses NLP to automatically classify, prioritize, and route complaints in real time. Built with a Spring Boot backend and a Python FastAPI microservice for ML-based classification, sentiment analysis, and duplicate detection, with Redis caching for fast lookups. The entire pipeline — testing, building, and deployment — is automated through GitHub Actions, with all services containerized via Docker for consistent, production-style delivery.

## Architecture

React Frontend (Tailwind + Recharts)
        │  REST (JWT)
        ▼
Spring Boot API (Auth, Tickets, RBAC)
        │
        ├──► PostgreSQL (tickets, users)
        ├──► Redis (duplicate-lookup cache, token blacklist)
        └──► FastAPI ML Service
                 - TF-IDF category classification
                 - Priority prediction
                 - Sentiment analysis
                 - Duplicate detection

## Services

| Service    | Stack                            | Port |
|------------|-----------------------------------|------|
| backend    | Spring Boot 3 + Spring Security   | 8080 |
| ml-service | FastAPI + scikit-learn            | 8000 |
| frontend   | React + Vite + Tailwind           | 5173 |
| postgres   | PostgreSQL 16                     | 5432 |
| redis      | Redis 7                           | 6379 |

## Quickstart

```bash
docker compose up --build
```

- Frontend: http://localhost:5173
- Backend Swagger: http://localhost:8080/swagger-ui.html
- ML service docs: http://localhost:8000/docs

Default seeded admin: `admin@support.com` / `Admin@123`

## CI/CD

`.github/workflows/ci-cd.yml` runs on every push to `main`:
lint → unit tests (JUnit + pytest) → build jars/images → push to GHCR → deploy webhook (Render/Railway).

## Folder Structure

```
GrievanceOps/
├── backend/            Spring Boot REST API
├── ml-service/          FastAPI ML microservice
├── frontend/            React + Tailwind SPA
├── docker-compose.yml
└── .github/workflows/ci-cd.yml
```
