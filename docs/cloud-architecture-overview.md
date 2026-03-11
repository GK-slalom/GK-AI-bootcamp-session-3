# Cloud Architecture Overview

This document provides a simple system-context diagram for the monorepo architecture: a React frontend, an Express API, and an in-memory store used by the backend.

```mermaid
graph LR
  User[User / Browser]
  Frontend[React Frontend\n(packages/frontend)]
  API[Express API\n(packages/backend)]
  Store[In-memory SQLite\n(:memory:) - better-sqlite3]

  User -->|Interacts via browser| Frontend
  Frontend -->|HTTP fetch /api/*| API
  API -->|Reads/Writes| Store

  classDef infra fill:#f8f9fa,stroke:#dfe6ee,color:#222;
  class Frontend,API,Store infra
```

Notes:
- The current repository contains both frontend and backend in a single monorepo.
- The Express API uses an in-memory SQLite database (`:memory:`) in the backend for runtime persistence.
- In development the frontend may use localStorage for local persistence per PRD; the canonical backend API is available at `/api/tasks`.

## Sequence: Create a TODO

```mermaid
sequenceDiagram
  participant User as User/Browser
  participant FE as React Frontend (packages/frontend)
  participant API as Express API (packages/backend)
  participant DB as In-memory SQLite (:memory:)

  User->>FE: Fill task form and submit
  FE->>FE: Validate title; normalize `due_date` to YYYY-MM-DD
  FE->>API: POST /api/tasks { title, description, due_date }
  API->>DB: INSERT task row (title, description, due_date)
  DB-->>API: Return created task (id, created_at...)
  API-->>FE: 201 Created + new task JSON
  FE->>FE: Update UI (render new task); optionally persist to localStorage

  Note right of FE: If PRD local-only mode is enabled, frontend may bypass API and store tasks in `localStorage` instead.
```
