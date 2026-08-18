# Stash Task

Task manager with a Go API and a Next.js client. Small domain on purpose — the point is a backend where every operation is an explicit use case rather than a controller doing five things at once.

## Structure

```
cmd/app/main.go                 Fiber server, explicit route registration
internal/
  usecase/task/                 8 use cases: Create, GetByID, ListAll, ListByUser,
                                Update, Delete, Complete, Uncomplete
  usecase/user/                 7 use cases: Create, Login, List, GetByID,
                                GetByEmail, UpdateByID, DeleteByID
  infra/web/handlers/           HTTP layer — injects use cases, binds Fiber routes
  infra/gateway/                PostgreSQL gateways behind interfaces
frontend/                       Next.js 14 app, separately containerised
```

One use case per file, each with a single `Execute`. Handlers translate HTTP to input DTOs and nothing more, so the business rules are testable without a router.

## Decisions

- **pgx v5, no ORM.** Raw SQL with prepared statements — the query is the query.
- **JWT via `gofiber/contrib/jwt`**, validated in middleware before a use case is ever constructed.
- **bcrypt** (`golang.org/x/crypto`) for password hashing; **viper** for config; **sonic** for JSON encoding.
- **Frontend is a separate container** on :3000 talking to the API on :8080 — no coupled build, no shared runtime.
- **Client state stays boring:** Zustand for stores, react-hook-form + Zod for forms, sonner for toasts, next-themes for dark mode.

## API

`POST /users` · `POST /users/login` · `GET /users` · `GET /users/:id` · `GET /users/email/:email` · `PUT /users/:id` · `DELETE /users/:id`

`POST /tasks` · `GET /tasks` · `GET /tasks/:id` · `GET /users/:userId/tasks` · `PUT /tasks/:id` · `DELETE /tasks/:id` · `POST /tasks/:id/complete` · `POST /tasks/:id/uncomplete`

Task routes require a bearer token.

## Stack

Go 1.21 · Fiber v2 · pgx v5 · PostgreSQL · JWT · viper · Next.js 14 · React 18 · TypeScript · Tailwind · Zustand · react-hook-form + Zod · Docker Compose

## Run it

```bash
cp .env.example .env          # POSTGRES_USER, POSTGRES_PASSWORD
docker compose up -d --build  # client :3000 · API :8080 · Postgres :5432
```

## Status

Demo-quality and functional: all fifteen operations work, auth is enforced, data persists. Honest gaps — the schema is not under a migration tool (only `init.sql` creating the database), there are no Go tests, and there is no graceful shutdown or request timeout yet.
