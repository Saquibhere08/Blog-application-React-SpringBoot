# Blog Application

Full-stack **Blog Application** built with **React** (frontend) and **Spring Boot** (backend). This README gives developers a quick start, describes features, architecture, environment variables, and deployment notes.

---

## Table of contents

- [Project Overview](#project-overview)
- [Tech Stack](#tech-stack)
- [Features](#features)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Quick Start](#quick-start)
  - [Backend (Spring Boot)](#backend-spring-boot)
  - [Frontend (React)](#frontend-react)
- [Environment variables](#environment-variables)
- [API Endpoints (examples)](#api-endpoints-examples)
- [Database](#database)
- [Testing](#testing)
- [Build & Deploy](#build--deploy)
- [Contributing](#contributing)
- [Acknowledgements](#acknowledgements)

---

## Project Overview

This repository contains a simple yet extendable blog platform where users can create, edit, and delete posts, comment, and browse by category or tag. The frontend is a React single-page app that consumes a RESTful Spring Boot API.

Use this project as a starter kit for personal blogs, portfolio projects, or as a learning resource for full‑stack Java + React development.

## Tech Stack

- Frontend: React (create-react-app or Vite compatible)
- Backend: Spring Boot (Java 11+)
- Database: PostgreSQL / H2 (dev)
- Authentication: JWT (configurable)
- Build tools: Maven (backend) / npm or yarn (frontend)

## Features

- User registration & authentication (JWT)
- Create / Read / Update / Delete (CRUD) for blog posts
- Comments on posts
- Categories and tags
- Image upload (optional; e.g., S3 or local storage)
- Pagination & search
- Role-based access (USER, ADMIN)

## Architecture

- Frontend (React): handles UI, routing, and API calls to the backend. Recommended structure: `src/components`, `src/pages`, `src/services` (API), `src/hooks`.
- Backend (Spring Boot): REST controllers, services, repositories (Spring Data JPA), DTOs, entities, and security layer (JWT filter).

## Prerequisites

- Java 11 or newer
- Maven 3.6+
- Node 14+ / npm 6+ (or yarn)
- PostgreSQL (or use embedded H2 for local dev)

## Quick Start

> These commands assume the repository root contains two folders: `/backend` and `/frontend`.

### Backend (Spring Boot)

1. Open a terminal and go to `backend/`

2. Configure environment variables (see [Environment variables](#environment-variables)). You can also use `application-dev.properties` for local settings.

3. Run with Maven wrapper:

```bash
# from repository/backend
./mvnw spring-boot:run   # Linux / macOS
mvnw.cmd spring-boot:run # Windows
```

Or build and run the jar:

```bash
./mvnw clean package
java -jar target/blog-backend-0.0.1-SNAPSHOT.jar
```

### Frontend (React)

1. Open a terminal and go to `frontend/`

2. Install dependencies:

```bash
npm install
# or
yarn
```

3. Start the dev server (ensure backend is running):

```bash
npm start
# or
yarn start
```

The React app should open at `http://localhost:3000` by default.

## Environment variables

Add these to your backend environment (or `application.properties` / `application-dev.properties`):

```properties
# Spring datasource (Postgres example)
spring.datasource.url=jdbc:postgresql://localhost:5432/blogdb
spring.datasource.username=bloguser
spring.datasource.password=secret
spring.jpa.hibernate.ddl-auto=update

# JWT (example)
jwt.secret=replace_with_a_strong_random_key
jwt.expirationMs=86400000

# Server port (optional)
server.port=8080
```

Frontend environment (create `.env` in `frontend/`):

```env
REACT_APP_API_URL=http://localhost:8080/api
```

## API Endpoints (examples)

- `POST /api/auth/register` — register user  
- `POST /api/auth/login` — authenticate (returns JWT)  
- `GET /api/posts` — list posts (with pagination)  
- `GET /api/posts/{id}` — get a single post  
- `POST /api/posts` — create post (auth required)  
- `PUT /api/posts/{id}` — update post  
- `DELETE /api/posts/{id}` — delete post  
- `POST /api/posts/{id}/comments` — add comment  
- `GET /api/categories`, `GET /api/tags`  

## Database

### Local development (H2)

Use H2 for quick testing with:

```
spring.datasource.url=jdbc:h2:mem:blogdb
spring.h2.console.enabled=true
```

### Production (Postgres)

```
CREATE DATABASE blogdb;
CREATE USER bloguser WITH ENCRYPTED PASSWORD 'secret';
GRANT ALL PRIVILEGES ON DATABASE blogdb TO bloguser;
```

## Testing

### Backend

```
./mvnw test
```

### Frontend

```
npm test
```

## Build & Deploy

### Backend

```
./mvnw clean package
```

### Frontend

```
npm run build
```

## Contributing

Contributions are welcome!

## Acknowledgements

Thanks to the open-source community!
