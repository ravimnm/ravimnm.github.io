---
title: "Secure Finance Backend"
layout: single
permalink: /projects/secure-finance-backend/
author_profile: true
toc: true
toc_label: "Contents"
---

# Secure Finance Backend

A production-style backend application built using **Spring Boot**, **Spring Security**, and **MongoDB** for secure financial transaction management. The system provides JWT-based authentication, Role-Based Access Control (RBAC), transaction management, analytics dashboards, pagination, and centralized error handling while following a layered backend architecture.

---

# Executive Summary

Modern financial applications require more than CRUD functionality. They must securely authenticate users, authorize operations based on roles, manage financial records efficiently, expose scalable REST APIs, and provide analytical insights for users and administrators.

The Secure Finance Backend demonstrates these principles by implementing a layered backend architecture with stateless JWT authentication, role-based authorization, MongoDB aggregation pipelines for analytics, paginated APIs, structured exception handling, and basic request rate limiting.

Although designed as a standalone backend service, the project also integrates with the Secure Multi-Tenant Audit Platform (SMTAP) for centralized audit logging and with the Java Runtime Security Agent (JRSA) for runtime security telemetry.

---

# Problem Statement

Many introductory finance applications focus primarily on CRUD operations without addressing backend security, authorization, scalability, or analytical reporting.

The objective of this project was to design a backend service capable of:

- Securing REST APIs using JWT authentication.
- Restricting operations through Role-Based Access Control.
- Managing financial transactions efficiently.
- Generating analytical summaries from transaction data.
- Providing scalable APIs using pagination.
- Returning consistent error responses.
- Applying basic request rate limiting.

---

# Motivation

This project was developed to strengthen practical backend engineering skills beyond basic Spring Boot applications.

Key learning objectives included:

- Implementing Spring Security with JWT authentication.
- Designing layered backend architecture.
- Working with MongoDB repositories and aggregation pipelines.
- Building production-style REST APIs.
- Applying authorization using user roles.
- Designing reusable exception handling.
- Structuring scalable API responses.

---

# System Architecture

```
                Client
                   │
                   ▼
            Spring Security
                   │
          JWT Authentication Filter
                   │
          Role-Based Authorization
                   │
        --------------------------
        | Controllers            |
        --------------------------
                   │
             Service Layer
                   │
          Repository Layer
                   │
               MongoDB
```

The application follows a layered architecture separating presentation, business logic, persistence, and security concerns.

---

# Technology Stack

| Category | Technology |
|----------|------------|
| Language | Java 17+ |
| Framework | Spring Boot |
| Security | Spring Security, JWT |
| Database | MongoDB |
| Data Access | Spring Data MongoDB |
| Build Tool | Maven |
| Testing | Postman |
| Authentication | JWT |
| Authorization | RBAC |

---

# Project Structure

```
controller/
service/
repository/
entity/
security/
dto/
exception/
```

### Controller Layer

Responsible for exposing REST APIs.

Components include:

- AuthController
- TransactionController
- DashboardController
- AdminController

---

### Service Layer

Contains business logic.

Services:

- AuthService
- TransactionService

---

### Repository Layer

Responsible for database operations.

Repositories include:

- UserRepository
- TransactionRepository
- RoleRepository

---

### Security Layer

Implements authentication and authorization.

Key components include:

- JwtFilter
- JwtUtil
- SecurityConfig
- CustomUserDetailsService

---

# Authentication & Authorization

Authentication is implemented using JSON Web Tokens (JWT).

Authentication flow:

1. User registers.
2. User logs in.
3. JWT token is generated.
4. Client sends the token in the Authorization header.
5. Spring Security validates every request.

Example:

```
Authorization: Bearer <JWT_TOKEN>
```

The application remains stateless by validating the token for every incoming request.

---

# Role-Based Access Control (RBAC)

Three user roles are implemented.

| Role | Permissions |
|------|-------------|
| ADMIN | Full transaction management and dashboard access |
| ANALYST | Read operations and analytics |
| VIEWER | Dashboard access only |

RBAC is enforced using Spring Security authorization rules to ensure users can only perform operations permitted by their assigned role.

---

# Transaction Management

The backend provides REST APIs for managing financial transactions.

Supported operations include:

- Create transaction
- View transactions
- Update transactions
- Delete transactions
- Filter transactions
- Monthly transaction trends

Pagination is supported to improve scalability when handling larger datasets.

Example:

```
GET /transactions?page=0&size=10
```

---

# Dashboard Analytics

The project uses MongoDB Aggregation Pipelines to generate analytical summaries.

Available analytics include:

- Total income versus expenses
- Category-wise spending
- Monthly transaction trends

Using aggregation pipelines allows calculations to be performed within the database, reducing application-side processing.

---

# REST API Overview

## Authentication

- POST `/auth/register`
- POST `/auth/login`

## Transactions

- POST `/transactions`
- GET `/transactions`
- PUT `/transactions/{id}`
- DELETE `/transactions/{id}`
- GET `/transactions/filter`
- GET `/transactions/trends`

## Dashboard

- GET `/dashboard/summary`
- GET `/dashboard/category`

## Admin

- GET `/admin/data`

---

# Pagination

Transaction APIs support pagination for improved scalability.

Example response:

```json
{
  "content": [],
  "page": 0,
  "size": 10,
  "totalElements": 25,
  "totalPages": 3
}
```

Pagination reduces response sizes while enabling clients to retrieve large datasets efficiently.

---

# Security Features

Security features implemented include:

- JWT Authentication
- Spring Security
- Role-Based Access Control
- Password protection using Spring Security
- Centralized authorization
- Structured exception handling
- Basic IP-based rate limiting

These features provide multiple layers of protection for REST endpoints.

---

# Error Handling

The application centralizes exception handling using a global exception handler.

Typical error response:

```json
{
  "timestamp": "...",
  "status": 400,
  "error": "Bad Request",
  "message": "...",
  "path": "/transactions"
}
```

Consistent error responses improve client-side error handling and debugging.

---

# Rate Limiting

A basic IP-based rate limiting filter is implemented to reduce excessive request traffic.

If request limits are exceeded, the application returns HTTP 429 (Too Many Requests).

Current implementation is memory-based and intended as a foundation for future distributed rate limiting.

---

# Integration with Other Projects

This backend is designed to integrate with other security projects in the portfolio.

### SMTAP

Provides:

- Centralized audit logging
- Audit integrity verification
- Compliance reporting

### Java Runtime Security Agent (JRSA)

Provides:

- JVM runtime monitoring
- Runtime telemetry
- Security event generation

Together, these projects demonstrate how multiple backend components can participate in a larger security ecosystem.

---

# Challenges

During development, several engineering challenges were addressed:

- Designing stateless authentication using JWT.
- Enforcing authorization across multiple user roles.
- Building analytical queries using MongoDB Aggregation.
- Structuring reusable exception handling.
- Supporting scalable API responses through pagination.
- Organizing the application into maintainable layers.

---

# Lessons Learned

This project strengthened practical knowledge in:

- Spring Boot backend development
- Spring Security
- JWT authentication
- Role-Based Access Control
- MongoDB Aggregation Framework
- REST API design
- Exception handling
- Backend architecture

---

# Future Improvements

Potential future enhancements include:

- Refresh token support
- Redis-based distributed rate limiting
- Swagger / OpenAPI documentation
- Advanced filtering and search capabilities
- Performance monitoring
- Docker-based deployment

---

# Gallery

> Screenshots will be added here.

- Login API
- Transaction APIs
- Dashboard analytics
- MongoDB collections
- Postman testing

---

# GitHub

**Repository**

`https://github.com/ravimnm/secure-finance-backend`

---

# Conclusion

The Secure Finance Backend demonstrates secure backend application development using Spring Boot and MongoDB. The project combines authentication, authorization, financial transaction management, analytical reporting, pagination, structured exception handling, and layered architecture into a cohesive backend service. It also serves as a foundation for broader security integrations with SMTAP and JRSA, illustrating how backend services can be designed with extensibility and security in mind.
