# ShopHub - E-Commerce Microservices Platform

A fully-featured, scalable e-commerce platform developed using a modern microservices architecture.

This project demonstrates service isolation, API Gateway usage, container orchestration, and event-driven communication principles in a real system.

## 🏗 System Architecture

```
┌──────────────────┐
│  React Frontend  │ :5173
│   (Vite + TS)    │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│   API Gateway    │ :9000
│   (Express.js)   │
└────────┬─────────┘
         │
    ┌────┴────┬────────────┐
    ▼         ▼            ▼
┌────────┐ ┌────────┐ ┌────────┐
│ User   │ │Product │ │ Order  │
│Service │ │Service │ │Service │
│:3000   │ │:5000   │ │:8080   │
│Node.js │ │Flask   │ │Spring  │
└────┬───┘ └────┬───┘ └────┬───┘
     │          │          │
     ▼          ▼          ▼
┌────────┐ ┌────────┐ ┌────────┐
│MongoDB │ │Postgres│ │ MySQL  │
│:27017  │ │:5432   │ │:3306   │
└────────┘ └────────┘ └────────┘
                │          │
                ▼          ▼
          ┌──────────┐ ┌────────────┐
          │Elastic   │ │ RabbitMQ   │
          │Search    │ │:5672,:15672│
          │:9200     │ └────────────┘
          └──────────┘
```

## 🛠 Technologies

| Service | Technologie | Port |
|--------|-----------|------|
| Frontend | React + Vite + TypeScript | 5173 |
| API Gateway | Node.js + Express | 9000 |
| User Service | Node.js + Express + MongoDB | 3000 |
| Product Service | Python + Flask + PostgreSQL | 5000 |
| Order Service | Java + Spring Boot + MySQL | 8080 |
| Message Broker | RabbitMQ | 5672, 15672 |
| Search Engine | Elasticsearch | 9200 |

🎯 Project Purpose

Use microservices architecture instead of a monolithic structure

Make services independently deployable

Provide centralized routing via API Gateway

Run the entire system with a single command using Docker Compose

Demonstrate RESTful services and event-driven communication (RabbitMQ) integration

## 🚀 Installation & Running

### 1. Start All Services with Docker
```bash
docker-compose up -d --build
```

### 2. Seed the Databases
```bash
# # Add products
docker-compose exec -T product-service python seed_products.py

# Add product images
docker-compose exec -T product-service python update_images.py
```

### 3. Start the Frontend
```bash
cd e-commerce-frontend
npm install
npm run dev
```

### 4. Open in Browser
- Frontend: http://localhost:5173
- RabbitMQ Dashboard: http://localhost:15672 (guest/guest)

## 📁 Project Structure

```
proje/
├── api-gateway/         # Express.js API Gateway
├── user-service/        # Node.js user service (MongoDB)
├── product-service/     # Flask product service (PostgreSQL)
├── order-service/       # Spring Boot order service (MySQL)
├── e-commerce-frontend/ # React frontend
├── docker-compose.yml   # Service orchestration
└── README.md
```

## 🔗 API Endpoints

### User Service (`/api/users`)
| Method | Endpoint | Description |
|--------|----------|----------|
| POST | /register | Register new user |
| POST | /login | User login with JWT |

### Product Service (`/api/products`)
| Method | Endpoint | Description |
|--------|----------|----------|
| GET | / | List all products |
| GET | /?q=laptop | Search product |
| POST | / | Add new product |

### Order Service (`/api/orders`)
| Method | Endpoint | Description|
|--------|----------|----------|
| GET | / | List all orders |
| GET | /{id} | Order detail |
| GET | /user/{userId} | Orders of a specific user |
| POST | / | Create new order |
| PUT | /{id} | Update ordere |
| DELETE | /{id} | Cancel order |

## 🧪 Test

```bash
# List Products
curl http://localhost:9000/api/products

# Register User
curl -X POST http://localhost:9000/api/users/register \
  -H "Content-Type: application/json" \
  -d '{"username": "test@test.com", "password": "123456"}'

# Create Order
curl -X POST http://localhost:8080/api/orders \
  -H "Content-Type: application/json" \
  -d '{"userId": "user1", "productId": "1", "quantity": 2, "totalPrice": 100}'
```

## 📊 Features

User registration & login with JWT

✅ 20 preloaded products (seed data)

✅ Real product images

✅ Elasticsearch-powered search

✅ Order creation

✅ Event-driven stock update via RabbitMQ

✅ Responsive design

✅ Shopping cart operations

✅ Microservice isolation

✅ API Gateway routing

## 🐳 Docker Commands

```bash
# Check running services
docker-compose ps

# View logs
docker-compose logs -f [servis-adı]

# Restart service
docker-compose restart [servis-adı]

# Stop entire system
docker-compose down
```
🏛 Architectural Characteristics

Loose Coupling

Service Isolation

RESTful API Communication

Event-Driven Architecture (RabbitMQ)

Independent Databases per Service

Centralized API Gateway

Containerized Deployment
