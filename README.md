# messaging-app

REST API for private messaging between users, with persistent conversation history and a React frontend.

## Screenshots

![Backend](./docs/screenshot-postman.png)

## Stack

**Backend:** Node.js · Express 5 · PostgreSQL (Neon) · Prisma · JWT · Passport.js · bcrypt  
**Frontend:** React 19 · Vite

## Features

- JWT authentication with secure password hashing
- Private conversations between any two users
- Persistent message history stored in PostgreSQL
- List all users to start a new conversation
- Update your own profile
- Clean REST API design with protected routes

## Structure

```
messaging-app/
├── backend/    # Express REST API + Prisma + PostgreSQL
└── frontend/   # React client (Vite)
```

## API Endpoints

### Auth

| Method | Path | Auth | Description |
| --- | --- | --- | --- |
| POST | /api/auth/register | — | Create account |
| POST | /api/auth/login | — | Returns JWT token |

### Users

| Method | Path | Auth | Description |
| --- | --- | --- | --- |
| GET | /api/users | Required | List all users |
| GET | /api/users/:id | Required | Get user profile |
| PUT | /api/users/:id | Required (own) | Update own profile |

### Messages

| Method | Path | Auth | Description |
| --- | --- | --- | --- |
| GET | /api/messages/:userId | Required | Get conversation with a user |
| POST | /api/messages/:userId | Required | Send a message to a user |

## Run locally

```bash
git clone https://github.com/paulperrin-stack/messaging-app
cd messaging-app/backend
cp .env.example .env   # add DATABASE_URL and JWT_SECRET
npm install
npx prisma generate
npx prisma migrate dev
node src/app.js
```

In a second terminal:

```bash
cd messaging-app/frontend
cp .env.example .env   # add VITE_API_URL=http://localhost:3000/api
npm install
npm run dev
```

## Environment variables

**backend/.env.example**

```dotenv
DATABASE_URL=       # PostgreSQL connection string (e.g. Neon)
JWT_SECRET=         # Any long random string
PORT=3000           # Default: 3000
```

**frontend/.env.example**

```dotenv
VITE_API_URL=       # e.g. http://localhost:3000/api
```