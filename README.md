# Microservices-Task

## Overview
This document provides details on testing various services after running the `docker-compose` file. These services include User, Product, Order, and Gateway Services. Each service has its own endpoints for testing purposes.

## Microservices Task Project Overview

This project demonstrates a Microservices Architecture using Docker and Docker Compose.

The application consists of the following independent services:

- User Service
- Product Service
- Order Service
- Gateway Service

Each service runs inside its own Docker container and communicates through Docker networking.
  -<img width="1536" height="1024" alt="microservice docker" src="https://github.com/user-attachments/assets/0f784879-a127-4d86-a109-4364f617edef" />

---

# Architecture

```text
                    +-------------------+
                    |      Client       |
                    +---------+---------+
                              |
                              v
                    +-------------------+
                    |  Gateway Service  |
                    |     Port 3003     |
                    +----+----+----+----+
                         |    |    |
            -------------    |    -------------
            |                |                |
            v                v                v

    +---------------+ +---------------+ +---------------+
    | User Service  | | Product Svc   | | Order Service |
    |   Port 3000   | |   Port 3001   | |   Port 3002   |
    +---------------+ +---------------+ +---------------+
```

---

# Technologies Used

- Node.js
- Express.js
- Docker
- Docker Compose
- Microservices Architecture

---

# Project Structure

```text
Microservices-Task/
│
├── docker-compose.yml
├── README.md
│
├── user-service/
│   ├── Dockerfile
│   ├── package.json
│
├── product-service/
│   ├── Dockerfile
│   ├── package.json
│
├── order-service/
│   ├── Dockerfile
│   ├── package.json
│
├── gateway-service/
│   ├── Dockerfile
│   ├── package.json
│
└── images/
    ├── architecture-diagram.png
    ├── docker-running.png
    ├── user-service.png
    ├── product-service.png
    ├── order-service.png
    └── gateway-service.png
```

---

# Prerequisites

Before running the project, install the following:

## 1. Docker

Download:

https://www.docker.com/

Verify installation:

```bash
docker --version
```

---

## 2. Docker Compose

Verify installation:

```bash
docker compose version
```

---

# Step-by-Step Deployment

---

# Step 1 — Clone Repository

```bash
git clone https://github.com/mohanDevOps-arch/Microservices-Task.git
```

Move into project directory:

```bash
cd Microservices-Task
```

---

# Step 2 — Verify Files

```bash
ls
```
*****************************
Expected:

```text
docker-compose.yml
user-service
product-service
order-service
gateway-service
README.md
```
*****************************
---

# Step 3 — Build Docker Images

```bash
docker compose build
```

This command:
- Builds Docker images
- Installs dependencies
- Prepares containers

---

# Step 4 — Start All Services

```bash
docker compose up -d
```

Expected output:

```text
Creating network "microservices_default"
Creating user-service
Creating product-service
Creating order-service
Creating gateway-service
```

---

# Step 5 — Verify Running Containers

```bash
docker ps
```

Expected running containers:

| Container | Port |
|---|---|
| user-service | 3000 |
| product-service | 3001 |
| order-service | 3002 |
| gateway-service | 3003 |

---

# Docker Containers Screenshot

 ---
 -<img width="1918" height="1030" alt="compose build" src="https://github.com/user-attachments/assets/099afb52-03c3-44c1-981f-cce8c3908724" />
# API Testing

---

# User Service

## Base URL

```text
http://localhost:3000
```

## Endpoint

### List Users

```bash
curl http://localhost:3000/users
```
 -<img width="1860" height="402" alt="user" src="https://github.com/user-attachments/assets/f2c8771e-7ca8-421b-9d5d-8876d8c59914" />

Browser:

```text
http://localhost:3000/users
```

---

# User Service Screenshot

 -<img width="1860" height="402" alt="user" src="https://github.com/user-attachments/assets/f2c8771e-7ca8-421b-9d5d-8876d8c59914" />

---

# Product Service

## Base URL

```text
http://localhost:3001
```

## Endpoint

### List Products

```bash
curl http://localhost:3001/products
```

Browser:

```text
http://localhost:3001/products
```

---

# Product Service Screenshot

  -<img width="1837" height="367" alt="prod" src="https://github.com/user-attachments/assets/902b524a-87cb-4052-9a9a-50ef97518809" />

---

# Order Service

## Base URL

```text
http://localhost:3002
```

## Endpoint

### List Orders

```bash
curl http://localhost:3002/orders
```

Browser:

```text
http://localhost:3002/orders
```

---

# Order Service Screenshot

  -<img width="1851" height="241" alt="orders" src="https://github.com/user-attachments/assets/cdfba925-ed1a-497d-9186-a7954fe2f969" />

---

# Gateway Service

## Base URL

```text
http://localhost:3003/api
```

## Gateway Endpoints

### Users API

```bash
curl http://localhost:3003/api/users
```

### Products API

```bash
curl http://localhost:3003/api/products
```

### Orders API

```bash
curl http://localhost:3003/api/orders
```

---

# Gateway Service Screenshot

  -<img width="1860" height="156" alt="3003" src="https://github.com/user-attachments/assets/ee773889-6f3f-4ebc-bbf3-f02d615dc0fd" />

---

# Docker Compose Configuration

```yaml
version: "3.8"

services:
  user-service:
    build: ./Microservices/user-service
    ports:
      - "3000:3000"
    networks:
      - microservice-network

  product-service:
    build: ./Microservices/product-service
    ports:
      - "3001:3001"
    networks:
      - microservice-network

  order-service:
    build: ./Microservices/order-service
    ports:
      - "3002:3002"
    networks:
      - microservice-network

  gateway-service:
    build: ./Microservices/gateway-service
    ports:
      - "3003:3003"
    depends_on:
      - user-service
      - product-service
      - order-service
    networks:
      - microservice-network

networks:
  microservice-network:
    driver: bridge

```

---

# Useful Docker Commands

## View Running Containers

```bash
docker ps
```

---

## Restart Services

```bash
docker compose restart
```

---

## Stop Services

```bash
docker compose down
```

---

## Rebuild Services

```bash
docker compose up -d --build
```

<img width="1917" height="1035" alt="comp build png 3" src="https://github.com/user-attachments/assets/8f4086c3-d937-40bf-bd5a-7b177183cbae" />
<img width="1918" height="931" alt="comp build png 2" src="https://github.com/user-attachments/assets/292275ce-7d65-471b-a328-f9395f6f63e3" />
<img width="1916" height="501" alt="comp build" src="https://github.com/user-attachments/assets/6edf3930-955b-45d8-af1e-065444f301b2" />
<img width="1918" height="1030" alt="compose build" src="https://github.com/user-attachments/assets/a09cef40-8eb3-424d-af13-8e7aabfd14e0" />
<img width="1918" height="1032" alt="done" src="https://github.com/user-attachments/assets/c799b9a0-0dbe-47df-801f-b726024f1dc5" />
<img width="1918" height="442" alt="container run" src="https://github.com/user-attachments/assets/5b095151-1ec2-4d26-81ff-b024cc7baf54" />

---

# Troubleshooting

---

## Port Already in Use

Check ports:

```bash
lsof -i :3000
```

Kill process:

```bash
kill -9 <PID>
```

---

## Container Not Starting

Check logs:

```bash
docker logs <container-id>
```

---

## Validate Docker Compose File

```bash
docker compose config
```

---

# Cleanup

Stop and remove containers:

```bash
docker compose down
```

Remove unused Docker resources:

```bash
docker system prune -a
```

---

# Final Validation Checklist

- Docker installed
- Docker Compose installed
- All containers running
- User Service working
- Product Service working
- Order Service working
- Gateway Service working
- APIs accessible
- No container crashes
- No port conflicts

---

# Author

Santosh Kumar Sharma -(DevOps, Batch-15)
