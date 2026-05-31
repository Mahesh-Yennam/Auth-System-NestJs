# NestJS Authentication API

A secure authentication backend built with NestJS, Prisma, PostgreSQL, and JWT. This project implements user registration, login, logout, refresh token rotation, password hashing, request validation, and protected routes using NestJS guards.

## Features

* User Registration
* User Login
* User Logout
* JWT Authentication
* Refresh Token Rotation
* Password Hashing with bcrypt
* Protected Routes using JWT Guards
* Request Validation with class-validator
* Prisma ORM
* PostgreSQL Database
* Docker Compose Setup
* Environment-based Configuration
* TypeScript Support

---

## Tech Stack

* NestJS
* TypeScript
* PostgreSQL
* Prisma ORM
* JWT (JSON Web Tokens)
* Passport
* bcrypt
* Docker Compose

---

## Project Structure

```text
src/
├── auth/
│   ├── dto/
│   ├── guards/
│   ├── strategies/
│   ├── types/
│   ├── auth.controller.ts
│   ├── auth.module.ts
│   └── auth.service.ts
│
├── users/
│   ├── users.module.ts
│   └── users.service.ts
│
├── prisma/
│   ├── prisma.module.ts
│   └── prisma.service.ts
│
├── app.module.ts
└── main.ts
```

---

## Authentication Flow

### Register

```http
POST /auth/register
```

Request Body:

```json
{
  "username": "mahesh",
  "email": "mahesh@gmail.com",
  "password": "Password123"
}
```

---

### Login

```http
POST /auth/login
```

Request Body:

```json
{
  "email": "mahesh@gmail.com",
  "password": "Password123"
}
```

Response:

```json
{
  "access_token": "jwt_access_token",
  "refresh_token": "jwt_refresh_token"
}
```

---

### Get Profile

```http
GET /auth/profile
```

Headers:

```text
Authorization: Bearer ACCESS_TOKEN
```

---

### Refresh Token

```http
POST /auth/refresh
```

Request Body:

```json
{
  "refreshToken": "jwt_refresh_token"
}
```

Response:

```json
{
  "access_token": "new_access_token",
  "refresh_token": "new_refresh_token"
}
```

---

### Logout

```http
POST /auth/logout
```

Headers:

```text
Authorization: Bearer ACCESS_TOKEN
```

Logout removes the stored refresh token, preventing further token refresh requests.

---

## Environment Variables

Create a `.env` file in the project root:

```env
DATABASE_URL="postgresql://postgres:postgres@localhost:5432/auth_db"

JWT_ACCESS_SECRET="your_access_secret"
JWT_REFRESH_SECRET="your_refresh_secret"
```

---

## Docker Setup

Create a `docker-compose.yml` file:

```yaml
version: '3.9'

services:
  postgres:
    image: postgres:17
    container_name: nest-auth-postgres
    restart: unless-stopped

    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: auth_db

    ports:
      - "5432:5432"

    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

Start PostgreSQL:

```bash
docker compose up -d
```

Stop PostgreSQL:

```bash
docker compose down
```

Remove database volume:

```bash
docker compose down -v
```

---

## Installation

Install dependencies:

```bash
npm install
```

Generate Prisma Client:

```bash
npx prisma generate
```

Run database migrations:

```bash
npx prisma migrate dev --name init
```

Start the development server:

```bash
npm run start:dev
```

Application runs on:

```text
http://localhost:3000
```

---

## Security Features

* Passwords are hashed using bcrypt before being stored.
* Access Tokens have a short expiration time.
* Refresh Tokens are stored as hashes in the database.
* Refresh Token Rotation is implemented.
* JWT Guard protects private routes.
* Request payloads are validated using DTOs.
* Unauthorized requests return appropriate HTTP status codes.

---

## Future Improvements

* Swagger API Documentation
* Role-Based Authorization (RBAC)
* Global Exception Filters
* Email Verification
* Forgot Password Flow
* Password Reset Tokens
* Rate Limiting
* Account Lockout Protection
* Audit Logging
* Refresh Token Cookies

---
