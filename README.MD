# Microservices Project with NestJS & Docker Compose

## Overview

This project implements a microservices architecture using NestJS. Each microservice is responsible for a specific domain and communicates using REST APIs.

## Tech Stack

- **Backend:** NestJS (TypeScript)
- **Database:** PostgreSQL (using Prisma ORM)
- **Containerization:** Docker & Docker Compose

## Microservices

- **User Service**: Manages user authentication and profiles.
- **Task Service**: Handles task management and assignment.
- **Token Service**: Handles task management and assignment.

## Project Structure

```
├── users/        # User management service
│   ├── src/
│   ├── prisma/
│   ├── Dockerfile
│   └── ...
├── tasks/        # Task handling service
│   ├── src/
│   ├── prisma/
│   ├── Dockerfile
│   └── ...
├── token/        # Token handling service
│   ├── src/
│   ├── prisma/
│   ├── Dockerfile
│   └── ...
├── docker-compose.yml   # Orchestrates microservices
├── .env.example                 # Environment variables
└── README.md            # Project documentation
```

## Getting Started

### Prerequisites

Ensure you have the following installed:

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/)
- [Node.js](https://nodejs.org/) (for local development without Docker)

### Setup & Run

#### 1. Clone the Repository

```sh
git clone https://github.com/Jonathanxl1/microservices-nestjs
cd nestjs-microservices
```

#### 2. Configure Environment Variables

Create a `.env` file in the root directory and define necessary variables:

```sh
POSTGRES_DB=<DB_NAME>
POSTGRES_USER=<DB_USER>
POSTGRES_PASSWORD=<DB_PASSWORD>
POSTGRES_HOST=<DB_HOST>
POSTGRES_PORT=<DB_PORT>
POSTGRES_URL=postgres://${POSTGRES_USER}:${POSTGRES_PASSWORD}@${POSTGRES_HOST}:${POSTGRES_PORT}/${POSTGRES_DB}

USERS_PORT=3000
USERS_URL="http://localhost:3000"

TASKS_PORT=3001
TASKS_URL=http://localhost:3001

TOKEN_PORT=3002
TOKEN_URL=http://localhost:3002
JWT_SECRET=<JWT_SECRET>
```

#### 3. Start Services with Docker Compose

```sh
docker-compose up --build
```

This will:

- Start PostgreSQL databases for each service
- Run migrations using Prisma (execute Dockerfile migrate command)
- Start the NestJS microservices

#### 4. Verify Services

- **User Service**: `http://localhost:3000/`
- **Task Service**: `http://localhost:3001/tasks`
- **Token Service**: `http://localhost:3002/`

## API Endpoints

| Service       | Endpoint     | Method | Description         | Authentication |
| ------------- | ------------ | ------ | ------------------- | -------------- |
| User Service  | `/signUp`    | POST   | Register a new user | NO             |
| User Service  | `/signIn`    | POST   | Authenticate a user | NO             |
| Task Service  | `/tasks`     | GET    | List all tasks      | YES            |
| Task Service  | `/tasks`     | POST   | Create tasks        | YES            |
| Task Service  | `/tasks/:id` | GET    | Get task details    | YES            |
| Task Service  | `/tasks/:id` | PUT    | Update task         | YES            |
| Task Service  | `/tasks/:id` | DELETE | Delete task details | YES            |
| Token Service | `/generate`  | POST   | Generate jwt token  | YES            |
| Token Service | `/validate`  | POST   | validate jwt token  | YES            |

## Request Body DTO

### User SignUp/SignIn

```json
{
  "email": "test@email.com",
  "password": "password"
}
```

### Task

```json
{
  "title": "title test", //REQUIRED
  "description": "",
  "assignee": 2,
  "status": "OPEN",
  "createdBy": 1 //REQUIRED
}
```

## Pending Features

- [ ] Assign task by User regitered
- [ ] Integrate a message broker (RabbitMQ/Kafka)
- [ ] Logger
- [ ] Optimize services and deploy

## License

MIT License

---

Developed by **[Your Name]**
