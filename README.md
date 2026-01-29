# PERN Todo App 

A fullstack Todo application built with the PERN stack (PostgreSQL, Express.js, React, Node.js) and GraphQL.\
This project demonstrates a task management system where users can create, read, update, and delete todos using a GraphQL API and a React frontend.

## Table of Contents

- [Description](#description)
- [Features](#features)
- [Technologies & Stack Explanation](#technologies--stack-explanation)
- [Architecture & Flow](#architecture--flow)
- [Installation & Run](#installation--run)
- [Project Structure](#project-structure)
- [GraphQL API](#graphql-api)
- [Author](#author)

## Description

This application allows users to:

- Manage tasks with a fully functional GraphQL API
- Create, Read, Update, and Delete (CRUD) todos
- Experience a type-safe development environment with TypeScript
- Connect to a cloud-based PostgreSQL database (Neon.tech)

The backend is built with **Node.js**, **Express**, and **GraphQL**.\
The frontend is built with **React (Vite)**, **TypeScript**, and **Tailwind CSS**.

> **Note:** Authentication is not implemented yet, so all users can modify the database.

## Features

- View all todos
- Add a new todo
- Update a todo (description & completion status)
- Delete a todo
- Fully functional GraphQL API
- React frontend with state management (Context API / Hooks)

## Technologies & Stack Explanation

- **PostgreSQL:** relational database to store tasks (`todo` table with `todo_id`, `description`, `completed`).
- **Node.js / Express.js:** backend server handles requests and executes database queries.
- **React (Vite):** frontend framework for building a responsive UI and communicating with backend.
- **GraphQL / graphql-http:** backend GraphQL API to query and mutate todo data.
- **pg:** Node.js library for connecting to PostgreSQL.
- **CORS:** allows frontend to communicate with backend on a different port.
- **Tailwind CSS** — Utility-first styling
- **Docker & Docker Compose** — For containerization and environment orchestration

This stack is known as **PERN**, with the addition of GraphQL for modern API design.

## Architecture & Flow

1. **Frontend React** sends GraphQL queries/mutations to the backend.
2. **Express.js server** receives requests and passes them to GraphQL handler.
3. **Resolvers** handle database queries via pg and return data.
4. **PostgreSQL** stores the todo data.
5. **Frontend** updates UI based on response.
6. In development, **Docker Volumes** enable instant Hot Reload for both TS services.

> Example: Adding a todo:
>
> - React sends a `mutation to /graphql` with `{ description }`.
> - GraphQL resolver executes `INSERT` query in PostgreSQL.
> - New todo is returned and React updates the state.

## Installation & Run

### 1. The Quickest Way (Docker Compose)

_Requires [Docker](https://www.docker.com/get-started/)_

1. Create a `.env` file inside `backend/` (see variables below)
2. Run everything with one command:
   ```bash
   docker-compose up --build
   ```
3. Open http://localhost:5173 in your browser

### 2. Manual Setup (For Development)

If you want to run the services separately without Docker:

#### Backend

```bash
cd backend
npm install dotenv cors express pg nodemon grahpql graphql-http
# Create .env with PORT, CONNECTION_STRING, CLIENT_URL
npm run dev
```

Backend .env variables:
```bash
PORT=4999
CONNECTION_STRING=postgres://user:password@host/neondb?sslmode=require
```

---

#### Frontend

```bash
cd frontend
npm install @tailwindcss/vite tailwindcss
# Create .env with VITE_API_URL
npm run dev
```

Frontend .env variables:
```bash
VITE_API_URL=http://localhost:4999
```

Frontend will be available at:
http://localhost:5173

---

## Project Structure

```
todo/
├─ docker-compose.yml
├─ backend/
│  ├─ Dockerfile
│  ├─ config/
│  │  └─ db.js          # PostgreSQL connection pool
│  ├─ resolvers/
│  │  └─ todoResolvers.ts # GraphQL resolvers
│  ├─ schema/
│  │  └─ todoSchema.ts  # GraphQL schema
│  ├─ index.ts          # Express + GraphQL server
│  └─ package.json
├─ frontend/
│  ├─ Dockerfile
│  ├─ src/
│  │  ├─ App.tsx        # Main App component
│  │  ├─ main.tsx       # Entry point
│  │  └─ components/    # UI components
│  └─ package.json
```

## GraphQL API

Get Todos:
```bash
query {
  getTodos {
    todo_id
    description
    completed
  }
}
```

Add Todo:
```bash
mutation {
  addTodo(description: "Learn GraphQL") {
    todo_id
    description
    completed
  }
}
```

Update a todo:
```bash
mutation {
  updateTodo(todo_id: 1, description: "Learn TS", completed: true) {
    todo_id
    description
    completed
  }
}
```

Delete a todo:
```bash
mutation {
  deleteTodo(todo_id: 1) {
    todo_id
    description
    completed
  }
}
```

## Author

**Taras Poiatsyka**\
[GitHub](https://github.com/tvsxar)