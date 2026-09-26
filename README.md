# 🏥 Hospital Management System — Backend

A **scalable Hospital Management System backend** built using **Java, Spring Boot, Spring Cloud, and Microservices Architecture**.

The system is designed to manage hospital operations such as **user management, patient profiles, appointments, pharmacy services, and secure API communication** through a centralized API Gateway.

---

## 🚀 Project Overview

This project follows a **Microservices Architecture**, where different business functionalities are separated into independent Spring Boot services.

The backend currently contains the following services:

* 👤 **UserMS** — User management and authentication
* 🧑‍⚕️ **ProfileMS** — Patient/profile management
* 📅 **Appointment** — Appointment management
* 💊 **PharmacyMS** — Pharmacy and medicine-related operations
* 🌐 **GatewayMS** — Central API Gateway
* 🔎 **Eureka-Server** — Service discovery

The repository structure currently contains these six backend modules.

---

## 🏗️ Architecture

```text
                         ┌──────────────────────┐
                         │       React App      │
                         │      Frontend        │
                         └──────────┬───────────┘
                                    │
                                    │ REST API
                                    ▼
                         ┌──────────────────────┐
                         │      GatewayMS       │
                         │    API Gateway       │
                         │      Port: 9000      │
                         └──────────┬───────────┘
                                    │
                  ┌─────────────────┼─────────────────┐
                  │                 │                 │
                  ▼                 ▼                 ▼
           ┌────────────┐    ┌────────────┐    ┌──────────────┐
           │   UserMS   │    │ ProfileMS  │    │ Appointment  │
           │            │    │            │    │     MS       │
           └─────┬──────┘    └─────┬──────┘    └──────┬───────┘
                 │                 │                  │
                 └─────────────────┼──────────────────┘
                                   │
                                   ▼
                            ┌──────────────┐
                            │  PharmacyMS  │
                            └──────────────┘

                    ┌──────────────────────┐
                    │    Eureka Server     │
                    │   Service Discovery  │
                    └──────────────────────┘
```

---

# 🧩 Microservices

## 1. 👤 UserMS

Responsible for user-related functionality.

### Responsibilities

* User registration
* User login
* User management
* Password management
* Authentication
* JWT token generation
* User-related APIs

---

## 2. 🧑‍⚕️ ProfileMS

Responsible for managing patient/user profile information.

### Responsibilities

* Create profile
* View profile
* Update profile
* Patient information management
* Profile-related APIs

---

## 3. 📅 AppointmentMS

Responsible for hospital appointment management.

### Responsibilities

* Create appointments
* View appointments
* Update appointments
* Appointment status management
* Patient appointment workflow
* Doctor appointment workflow

---

## 4. 💊 PharmacyMS

Responsible for pharmacy-related operations.

### Responsibilities

* Medicine management
* Pharmacy information
* Medicine availability
* Pharmacy-related APIs

---

## 5. 🌐 GatewayMS

The **API Gateway** acts as the single entry point for frontend requests.

### Responsibilities

* API routing
* Centralized request handling
* CORS configuration
* JWT filtering
* Security filtering
* Communication with microservices

### Request Flow

```text
Frontend
   │
   ▼
GatewayMS
   │
   ├── /users/**        → UserMS
   ├── /profile/**      → ProfileMS
   ├── /appointment/**  → AppointmentMS
   └── /pharmacy/**     → PharmacyMS
```

---

## 6. 🔎 Eureka Server

Eureka provides **service discovery** for the microservices.

Instead of hardcoding service locations, services register themselves with Eureka.

```text
                Eureka Server
                     │
        ┌────────────┼────────────┐
        │            │            │
        ▼            ▼            ▼
      UserMS     ProfileMS    AppointmentMS
        │            │            │
        └────────────┼────────────┘
                     │
                     ▼
                PharmacyMS
```

---

# 🛠️ Tech Stack

| Technology           | Purpose                       |
| -------------------- | ----------------------------- |
| Java                 | Backend Programming           |
| Spring Boot          | Microservices                 |
| Spring Cloud         | Microservices Infrastructure  |
| Spring Cloud Gateway | API Gateway                   |
| Eureka               | Service Discovery             |
| Spring Security      | Application Security          |
| JWT                  | Authentication                |
| Spring Data JPA      | Database Access               |
| Hibernate            | ORM                           |
| MySQL                | Database                      |
| Maven                | Build & Dependency Management |
| REST API             | API Communication             |
| Postman              | API Testing                   |
| Git                  | Version Control               |
| GitHub               | Source Code Management        |

---

# 📂 Project Structure

```text
hospital-management-backend/
│
├── Appointment/
│   ├── src/
│   ├── pom.xml
│   └── ...
│
├── Eureka-Server/
│   ├── src/
│   ├── pom.xml
│   └── ...
│
├── GatewayMS/
│   ├── src/
│   ├── pom.xml
│   └── ...
│
├── PharmacyMS/
│   ├── src/
│   ├── pom.xml
│   └── ...
│
├── ProfileMS/
│   ├── src/
│   ├── pom.xml
│   └── ...
│
├── UserMS/
│   ├── src/
│   ├── pom.xml
│   └── ...
│
└── media/
```

The repository currently has the above service directories at its root.

---

# 🔐 Authentication Architecture

The application uses **JWT-based authentication**.

### Login Flow

```text
User
 │
 ▼
React Frontend
 │
 ▼
GatewayMS
 │
 ▼
UserMS
 │
 ▼
Validate Credentials
 │
 ▼
Generate JWT
 │
 ▼
Return JWT
 │
 ▼
Frontend
```

For protected requests:

```text
Frontend
   │
   │ Authorization: Bearer <JWT>
   ▼
GatewayMS
   │
   ▼
JWT Filter
   │
   ├── Valid Token ──────► Microservice
   │
   └── Invalid Token ────► 401 Unauthorized
```

---

# 🔄 Complete Request Flow

```text
┌───────────────┐
│ React Frontend│
└───────┬───────┘
        │
        │ HTTP Request
        ▼
┌───────────────┐
│   GatewayMS   │
└───────┬───────┘
        │
        │ Route
        ▼
┌───────────────┐
│ Eureka Server │
└───────┬───────┘
        │
        ▼
┌───────────────────────┐
│ Required Microservice │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│ Controller            │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│ Service Layer         │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│ Repository / JPA      │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│ MySQL Database        │
└───────────────────────┘
```

---

# 🗄️ Database

The application uses **MySQL** for persistent data storage.

Example configuration:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/hospital_db
spring.datasource.username=root
spring.datasource.password=YOUR_PASSWORD

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

For production, database credentials should be supplied through environment variables or secure configuration rather than committed to GitHub.

---

# ⚙️ Prerequisites

Install the following before running the project:

* Java 17+
* Maven
* MySQL
* Git
* Postman
* IntelliJ IDEA / Eclipse / Spring Tool Suite

---

# 🚀 Installation & Setup

## 1. Clone Repository

```bash
git clone https://github.com/tabrez-tech-09/hospital-management-backend.git
```

Navigate to the project:

```bash
cd hospital-management-backend
```

---

## 2. Configure MySQL

Create the required database:

```sql
CREATE DATABASE hospital_db;
```

Then configure the database credentials in the respective microservice configuration.

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/hospital_db
spring.datasource.username=root
spring.datasource.password=YOUR_PASSWORD
```

---

# ▶️ Running the Project

Start the services in the following order.

### Step 1 — Eureka Server

```text
Eureka-Server
```

Run:

```bash
mvn spring-boot:run
```

---

### Step 2 — UserMS

```text
UserMS
```

Run:

```bash
mvn spring-boot:run
```

---

### Step 3 — ProfileMS

```text
ProfileMS
```

Run:

```bash
mvn spring-boot:run
```

---

### Step 4 — AppointmentMS

```text
Appointment
```

Run:

```bash
mvn spring-boot:run
```

---

### Step 5 — PharmacyMS

```text
PharmacyMS
```

Run:

```bash
mvn spring-boot:run
```

---

### Step 6 — GatewayMS

```text
GatewayMS
```

Run:

```bash
mvn spring-boot:run
```

---

# 🌐 Service Ports

Example service configuration:

| Service       |   Port |
| ------------- | -----: |
| GatewayMS     | `9000` |
| UserMS        | `8081` |
| ProfileMS     | `9100` |
| AppointmentMS | `9200` |
| Eureka Server | `8761` |

> Update these values if your current `application.yml` / `application.properties` uses different ports.

---

# 🧪 API Testing

Use **Postman** or another REST API client for testing.

Example APIs:

```http
POST /users/register
POST /users/login

GET /profile/...

POST /appointment/...
GET /appointment/...

GET /pharmacy/...
POST /pharmacy/...
```

Protected APIs should receive the JWT token:

```http
Authorization: Bearer <JWT_TOKEN>
```

---

# 🔒 Security

Security features include:

* JWT authentication
* Password hashing
* Gateway-level JWT filtering
* Protected APIs
* CORS configuration
* Authentication and authorization

### Security Best Practices

Never commit:

```text
❌ Database passwords
❌ JWT secrets
❌ API keys
❌ Private credentials
```

Use:

```text
.env
Environment Variables
Secret Manager
```

for sensitive configuration.

---

# 🌍 Frontend Integration

The frontend communicates with the backend through the Gateway.

```text
React
  │
  │ HTTP
  ▼
GatewayMS : 9000
  │
  ├── UserMS
  ├── ProfileMS
  ├── AppointmentMS
  └── PharmacyMS
```

Frontend Repository:

https://github.com/tabrez-tech-09/hospital-management-frontend

Live Application:

https://pulse-five-ruby.vercel.app/login

---

# 📌 Key Features

* ✅ Microservices Architecture
* ✅ Spring Boot
* ✅ Spring Cloud
* ✅ Eureka Service Discovery
* ✅ Spring Cloud Gateway
* ✅ JWT Authentication
* ✅ User Management
* ✅ Patient Profile Management
* ✅ Appointment Management
* ✅ Pharmacy Management
* ✅ MySQL Database
* ✅ Spring Data JPA
* ✅ REST APIs
* ✅ CORS Configuration
* ✅ Postman API Testing

---

# 📈 Future Improvements

* [ ] Docker & Docker Compose
* [ ] Centralized configuration with Spring Cloud Config
* [ ] Redis caching
* [ ] Kafka/RabbitMQ messaging
* [ ] Swagger/OpenAPI documentation
* [ ] Centralized logging
* [ ] Prometheus monitoring
* [ ] Grafana dashboards
* [ ] CI/CD with GitHub Actions
* [ ] Kubernetes deployment
* [ ] Rate limiting
* [ ] Distributed tracing

---

# 🧠 What This Project Demonstrates

This project demonstrates practical understanding of:

* Microservices architecture
* Spring Boot
* Spring Cloud
* API Gateway
* Service Discovery
* JWT authentication
* REST API development
* Database integration
* Inter-service communication
* CORS configuration
* Backend security
* Distributed application architecture

---

# 👨‍💻 Author

## Tabrez Rabbani

**Java Backend Developer | Spring Boot | Microservices | React**

### Profiles

* GitHub: https://github.com/tabrez-tech-09
* LinkedIn: https://www.linkedin.com/in/tabrez-rabbani/
* LeetCode: https://leetcode.com/u/tabrez_tech/

---

# ⭐ Support

If you find this project useful, consider giving the repository a ⭐.

---

## 🏥 Hospital Management System

**Frontend:** React.js
**Backend:** Java + Spring Boot
**Architecture:** Microservices
**Gateway:** Spring Cloud Gateway
**Service Discovery:** Eureka
**Database:** MySQL
**Authentication:** JWT
**Deployment:** Cloud-ready

