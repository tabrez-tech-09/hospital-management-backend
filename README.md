# 🏥 Hospital Management Backend

A **Microservices-based Hospital Management System** built using **Java, Spring Boot, Spring Cloud, REST APIs, and MySQL**.

The project is designed to manage hospital-related operations such as users, patient profiles, appointments, pharmacy services, and service communication through an API Gateway.

## 🚀 Project Overview

The Hospital Management Backend follows a **Microservices Architecture**, where different business functionalities are separated into independent services.

### Main Services

* **Eureka Server** — Service discovery and registration
* **GatewayMS** — API Gateway and centralized request routing
* **UserMS** — User registration, authentication, and user management
* **ProfileMS** — Patient/user profile management
* **Appointment** — Appointment management
* **PharmacyMS** — Pharmacy-related operations

## 🏗️ Architecture

```text
                         ┌─────────────────────┐
                         │      Frontend       │
                         │   React / Client    │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │      GatewayMS      │
                         │   API Gateway       │
                         │   Port: 9000        │
                         └──────────┬──────────┘
                                    │
              ┌─────────────────────┼─────────────────────┐
              │                     │                     │
              ▼                     ▼                     ▼
       ┌─────────────┐       ┌─────────────┐       ┌─────────────┐
       │   UserMS    │       │  ProfileMS  │       │ Appointment │
       │             │       │             │       │     MS      │
       └──────┬──────┘       └──────┬──────┘       └──────┬──────┘
              │                     │                     │
              └─────────────────────┼─────────────────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │   MySQL Database    │
                         └─────────────────────┘


                         ┌─────────────────────┐
                         │    Eureka Server    │
                         │  Service Discovery  │
                         └─────────────────────┘
```

## 📂 Project Structure

```text
hospital-management-backend/
│
├── Appointment/
│   └── Appointment Microservice
│
├── Eureka-Server/
│   └── Service Discovery Server
│
├── GatewayMS/
│   └── API Gateway
│
├── PharmacyMS/
│   └── Pharmacy Microservice
│
├── ProfileMS/
│   └── Profile Microservice
│
├── UserMS/
│   └── User Microservice
│
└── media/
    └── Project media/resources
```

## 🛠️ Technologies Used

| Technology           | Purpose                        |
| -------------------- | ------------------------------ |
| Java                 | Backend programming            |
| Spring Boot          | Microservice development       |
| Spring Cloud         | Microservices infrastructure   |
| Spring Cloud Gateway | API Gateway                    |
| Eureka               | Service Discovery              |
| Spring Data JPA      | Database operations            |
| Hibernate            | ORM                            |
| MySQL                | Relational database            |
| REST API             | Service communication          |
| Maven                | Dependency management          |
| JWT                  | Authentication & authorization |
| Postman              | API testing                    |
| Git & GitHub         | Version control                |

## 🔐 Authentication Flow

The application can use JWT-based authentication for securing APIs.

```text
Client
  │
  │ Login
  ▼
GatewayMS
  │
  ▼
UserMS
  │
  ├── Validate User
  ├── Generate JWT
  │
  ▼
JWT Token
  │
  ▼
Client
```

For subsequent requests:

```text
Client
   │
   │ Authorization: Bearer <JWT>
   ▼
GatewayMS
   │
   ├── Validate JWT
   │
   ▼
Microservice
   │
   ▼
Response
```

## 🔄 Request Flow

A typical API request follows this flow:

```text
Frontend
   ↓
API Gateway
   ↓
Service Discovery
   ↓
Required Microservice
   ↓
Repository
   ↓
MySQL
```

Example:

```text
POST /users/login
        ↓
GatewayMS
        ↓
UserMS
        ↓
UserRepository
        ↓
MySQL
```

## 🌐 Service Responsibilities

### 1. UserMS

Responsible for:

* User registration
* User login
* User authentication
* Password management
* JWT generation
* User-related operations

### 2. ProfileMS

Responsible for:

* Patient profile management
* Personal information
* Profile creation/update
* Patient-related information

### 3. AppointmentMS

Responsible for:

* Creating appointments
* Updating appointments
* Viewing appointments
* Appointment status management
* Patient-doctor appointment workflow

### 4. PharmacyMS

Responsible for:

* Medicine-related operations
* Pharmacy management
* Medicine information
* Pharmacy-related APIs

### 5. GatewayMS

Acts as the single entry point for client requests.

Responsibilities:

* Request routing
* Centralized API entry point
* CORS handling
* JWT filtering/security
* Communication with backend services

### 6. Eureka Server

Responsible for:

* Service registration
* Service discovery
* Maintaining information about available microservices
* Helping services communicate without hardcoding service locations

## ⚙️ Prerequisites

Before running the project, install:

* Java 17+
* Maven
* MySQL
* Git
* Postman
* IDE such as IntelliJ IDEA / Eclipse / Spring Tool Suite

## 🔧 Configuration

Configure database credentials in each microservice's:

```text
application.properties
```

or

```text
application.yml
```

Example:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/hospital_db
spring.datasource.username=root
spring.datasource.password=YOUR_PASSWORD

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

> **Important:** Never commit real database passwords, JWT secrets, API keys, or other credentials to GitHub. Use environment variables or a local configuration file.

## ▶️ How to Run

### 1. Clone Repository

```bash
git clone https://github.com/tabrez-tech-09/hospital-management-backend.git
```

```bash
cd hospital-management-backend
```

### 2. Start Eureka Server

Navigate to:

```text
Eureka-Server
```

Run:

```bash
mvn spring-boot:run
```

### 3. Start Backend Microservices

Start the services individually:

```text
UserMS
ProfileMS
Appointment
PharmacyMS
```

### 4. Start Gateway

Finally start:

```text
GatewayMS
```

The frontend should communicate with the backend through the **Gateway**, rather than directly calling every microservice.

## 🧪 API Testing

Use **Postman** to test APIs.

Example:

```http
POST /users/register
POST /users/login
GET  /profile/...
POST /appointment/...
GET  /pharmacy/...
```

Actual endpoints may vary according to the controllers implemented in each microservice.

## 🔒 Security

Security-related components include:

* JWT authentication
* Gateway-level request filtering
* Authorization
* Password hashing
* Protected APIs

### Recommended Security Practices

* Store JWT secrets in environment variables.
* Never commit passwords to Git.
* Never expose production database credentials.
* Use HTTPS in production.
* Validate and sanitize incoming requests.

## 📊 Microservices Communication

The project uses a service-oriented architecture where services can communicate through APIs and service discovery.

```text
                 Eureka Server
                      │
        ┌─────────────┼─────────────┐
        │             │             │
        ▼             ▼             ▼
     UserMS       ProfileMS    AppointmentMS
        │             │             │
        └─────────────┼─────────────┘
                      │
                 PharmacyMS
```

## 🎯 Key Features

* ✅ Microservices Architecture
* ✅ Service Discovery using Eureka
* ✅ API Gateway
* ✅ JWT Authentication
* ✅ User Management
* ✅ Patient Profile Management
* ✅ Appointment Management
* ✅ Pharmacy Management
* ✅ REST APIs
* ✅ MySQL Database
* ✅ Spring Data JPA
* ✅ Maven-based project
* ✅ Postman API testing

## 📈 Future Improvements

* Docker & Docker Compose
* Centralized configuration using Spring Cloud Config
* Redis caching
* Kafka/RabbitMQ for asynchronous communication
* Centralized logging
* API documentation with Swagger/OpenAPI
* Rate limiting
* Monitoring with Prometheus & Grafana
* CI/CD using GitHub Actions
* Cloud deployment

## 👨‍💻 Author

**Tabrez Rabbani**

* GitHub: https://github.com/tabrez-tech-09
* LinkedIn: https://www.linkedin.com/in/tabrez-rabbani/

## ⭐ Support

If you find this project useful, consider giving the repository a ⭐ on GitHub.

---

**Hospital Management Backend**
*Built with Java + Spring Boot + Spring Cloud + Microservices*
