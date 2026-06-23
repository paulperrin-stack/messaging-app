# messaging-app

A REST API for private messaging between users, with a minimal React frontend for local development.

**API:** https://messaging-app-4ug1.onrender.com

## Features

- JWT authentication with secure password hashing
- Private conversations between any two users
- Persistent message history stored in PostgreSQL
- List all users to start a new conversation
- Update your own profile (display name, bio, avatar)
- Clean REST API design with protected routes

## Tech stack

**Backend:** Node.js · Express 5 · PostgreSQL (Neon) · Prisma · Passport JWT · bcrypt  
**Frontend:** React 19 · Vite *(local development only)*

## Project structure

```
messaging-app/
├── backend/    Express REST API + Prisma + PostgreSQL
└── frontend/   React client (Vite) — run locally against the API
```

## Getting started

### Prerequisites

- Node.js 20+
- A PostgreSQL database (e.g. [Neon](https://neon.tech) free tier)

### Backend

```bash
cd backend
npm install
cp .env.example .env      # fill in the values below
npx prisma generate
npx prisma migrate deploy
npm run dev
```

`backend/.env`:

| Variable       | Description                              |
| -------------- | ---------------------------------------- |
| `DATABASE_URL` | PostgreSQL connection string             |
| `JWT_SECRET`   | Any long random string                   |
| `PORT`         | API port (default: 3000)                 |

### Frontend

```bash
cd frontend
npm install
echo "VITE_API_URL=http://localhost:3000/api" > .env
npm run dev
```

The app runs at `http://localhost:5173`.

## API endpoints

### Auth

| Method | Path                  | Auth     | Description              |
| ------ | --------------------- | -------- | ------------------------ |
| POST   | `/api/auth/register`  | —        | Create account           |
| POST   | `/api/auth/login`     | —        | Returns JWT token        |

### Users

| Method | Path               | Auth     | Description              |
| ------ | ------------------ | -------- | ------------------------ |
| GET    | `/api/users`       | Required | List all users           |
| GET    | `/api/users/:id`   | Required | Get user profile         |
| PUT    | `/api/users/:id`   | Required (own) | Update own profile |

### Messages

| Method | Path                      | Auth     | Description                    |
| ------ | ------------------------- | -------- | ------------------------------ |
| GET    | `/api/messages/:userId`   | Required | Get conversation with a user   |
| POST   | `/api/messages/:userId`   | Required | Send a message to a user       |

All endpoints except `/api/auth/register` and `/api/auth/login` require a `Bearer` token in the `Authorization` header.

## Deployment

The backend deploys to [Render](https://render.com) (free tier) with [Neon](https://neon.tech) as the PostgreSQL database.

> The Render free tier spins down after 15 minutes of inactivity. The first request after a period of inactivity may take 30–60 seconds to respond.

The frontend is not deployed — run it locally against the live API by setting `VITE_API_URL` to your Render backend URL.

## License

MIT — see [LICENSE](./LICENSE).