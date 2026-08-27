# Cloud Architecture Overview

The application is a small monorepo with a React frontend, an Express API, and an in-memory SQLite store owned by the backend. Task data is held for the lifetime of the API process and is not persisted externally.

```mermaid
flowchart LR
    User[User] --> Browser[Web Browser]
    Browser --> Frontend[React Frontend]
    Frontend -->|HTTP / JSON| API[Express API]
    API --> Store[(In-memory SQLite Store)]
```

## Creating a TODO

```mermaid
sequenceDiagram
    actor User
    participant Browser as Web Browser
    participant Frontend as React Frontend
    participant API as Express API
    participant Store as In-memory SQLite Store

    User->>Browser: Enter TODO title and submit
    Browser->>Frontend: Trigger create-task action
    Frontend->>API: POST /api/tasks with task data
    API->>API: Validate title and task fields
    API->>Store: Insert task
    Store-->>API: Return created task
    API-->>Frontend: 201 Created with task data
    Frontend-->>Browser: Update TODO list
    Browser-->>User: Display new TODO
```

- The React frontend provides the task-management user interface.
- The Express API handles task requests and validation.
- The in-memory SQLite store holds task data while the backend process is running.
- No external database, cloud service, or persistent storage is part of the current architecture.
