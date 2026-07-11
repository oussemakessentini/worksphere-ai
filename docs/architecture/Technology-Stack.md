# Document Information

**Document:** Technology Stack  
**Project:** WorkSphere AI  
**Version:** 1.0  
**Status:** Draft  
**Author:** Oussama Ksantini  
**Last Updated:** 2026-07-10

---

# Technology Stack

## 1. Purpose

This document defines the technologies selected for WorkSphere AI and explains why each technology is used.

The stack is designed to support:

- Microservices
- Event-driven communication
- Scalability
- Fault tolerance
- Observability
- Cloud deployment
- Professional testing and DevOps practices

---

# 2. Backend

## Java 21

Java 21 is the primary backend language.

### Reasons

- Long-term support version
- Strong enterprise ecosystem
- Excellent performance
- Modern language features
- Large community
- Strong compatibility with Spring Boot

---

## Spring Boot

Spring Boot is used to build all backend services.

### Responsibilities

- REST APIs
- Dependency injection
- Validation
- Security
- Data access
- Configuration
- Health checks

---

## Spring Cloud

Spring Cloud provides distributed-system capabilities.

### Components

- Spring Cloud Gateway
- Spring Cloud Config
- Netflix Eureka
- OpenFeign
- LoadBalancer
- Circuit breaker integration

---

## Spring Security

Used for:

- Authentication
- Authorization
- JWT validation
- Role-based access control
- Method-level security

---

## Spring Data JPA

Used for relational persistence.

### Reasons

- Simplifies database access
- Integrates with Hibernate
- Supports repositories
- Reduces boilerplate

---

## Hibernate

Hibernate is the ORM implementation used by Spring Data JPA.

---

## Maven

Maven is the build and dependency-management tool.

### Reasons

- Familiarity
- Strong Spring ecosystem support
- Multi-module project support
- Reliable dependency management

---

# 3. Frontend

## React

React is used for the web application.

### Reasons

- Component-based architecture
- Large ecosystem
- Strong community
- Good fit for dashboards and portals

---

## TypeScript

TypeScript provides static typing for frontend development.

### Benefits

- Fewer runtime errors
- Better IDE support
- Safer API integration
- Easier refactoring

---

## Vite

Vite is used as the frontend build tool.

### Reasons

- Fast development server
- Fast builds
- Simple configuration

---

## UI Library

Initial recommendation:

- Material UI

Alternative:

- Tailwind CSS

Final choice will be documented in a separate ADR.

---

# 4. Databases

## PostgreSQL

Each business service owns its own PostgreSQL database.

### Reasons

- Reliable relational database
- Strong transaction support
- JSON support
- Mature indexing
- Suitable for enterprise applications

### Initial Databases

- identity_db
- talent_db
- workforce_db
- learning_db
- engagement_db

---

## Redis

Redis will be introduced after the MVP.

### Planned Uses

- Caching
- Rate limiting
- Temporary tokens
- Distributed locks
- Session-related data
- Leaderboards

---

# 5. Messaging

## Apache Kafka

Kafka is the primary event-streaming platform.

### Planned Uses

- Domain events
- Service decoupling
- Asynchronous processing
- Analytics event collection
- Notification workflows

### Example Events

- OfferAccepted
- EmployeeCreated
- QuizCompleted
- CertificateIssued
- RecognitionGiven

Kafka may be introduced after the first working synchronous MVP.

---

# 6. Service Communication

## REST

REST is used for synchronous communication when an immediate response is required.

---

## OpenFeign

OpenFeign provides declarative REST clients between services.

### Planned Uses

- Retrieve employee data
- Retrieve job data
- Validate related resources

---

## Spring Cloud LoadBalancer

Used for client-side load balancing between multiple service instances.

---

## Resilience4j

Used for resilience patterns.

### Patterns

- Circuit breaker
- Retry
- Rate limiter
- Bulkhead
- Time limiter

---

# 7. Platform Infrastructure

## API Gateway

Spring Cloud Gateway provides:

- Request routing
- CORS
- Token validation
- Rate limiting
- Correlation IDs
- Centralized API access

---

## Discovery Service

Netflix Eureka provides:

- Service registration
- Service discovery
- Instance lookup
- Load-balancing support

---

## Configuration Service

Spring Cloud Config Server provides:

- Centralized configuration
- Environment-specific configuration
- Git-backed configuration
- Shared service properties

Production secrets will not be stored in Git.

---

# 8. Containers

## Docker

Every service will have its own Docker image.

---

## Docker Compose

Docker Compose will run the local development environment.

### Planned Containers

- Config Server
- Discovery Service
- API Gateway
- Business services
- PostgreSQL databases
- Kafka
- Redis
- Observability tools

---

## Kubernetes

Kubernetes is a future production-scale learning goal.

It is not required for the MVP.

---

# 9. Observability

## Spring Boot Actuator

Provides:

- Health checks
- Application information
- Metrics endpoints

---

## Micrometer

Micrometer connects application metrics to monitoring systems.

---

## Prometheus

Prometheus collects metrics.

---

## Grafana

Grafana displays dashboards and alerts.

---

## OpenTelemetry

OpenTelemetry provides standardized tracing and telemetry instrumentation.

---

## Zipkin or Grafana Tempo

One distributed tracing backend will be selected later.

---

## ELK Stack

Planned centralized logging stack:

- Elasticsearch
- Logstash
- Kibana

An alternative such as OpenSearch may also be evaluated.

---

# 10. File Storage

## Amazon S3

Planned storage for:

- Resumes
- Profile images
- Company logos
- Course files
- Generated certificates

For local development, an S3-compatible tool such as MinIO may be used.

---

# 11. Email

Initial options:

- Amazon SES
- SendGrid

Email will support:

- Account verification
- Password reset
- Invitations
- Offers
- Training reminders
- Certificates

The final provider will be documented through an ADR.

---

# 12. AI Integration

AI features are planned for a future version.

### Planned Uses

- Resume analysis
- Candidate matching
- Quiz generation
- Interview question generation
- Learning recommendations
- Analytics summaries

The AI provider must return structured, validated output.

---

# 13. Testing

## JUnit 5

Primary Java testing framework.

---

## Mockito

Used for unit-test mocking.

---

## Testcontainers

Used for integration testing with real infrastructure.

### Planned Containers

- PostgreSQL
- Kafka
- Redis

---

## Spring Boot Test

Used for service-level and integration tests.

---

## REST Assured

May be used for API tests.

---

## React Testing Library

Used for frontend component testing.

---

## Playwright

Planned for end-to-end browser testing.

---

# 14. API Documentation

## OpenAPI and Swagger UI

Every public REST API must be documented.

Documentation should include:

- Endpoints
- Request bodies
- Responses
- Error formats
- Authentication requirements

---

# 15. Database Migrations

## Flyway

Flyway manages database schema migrations.

### Rules

- No manual production schema changes
- Every schema change requires a migration
- Migrations are version-controlled

---

# 16. CI/CD

## GitHub Actions

Planned workflows:

- Build
- Unit tests
- Integration tests
- Static analysis
- Docker image creation
- Security scanning
- Deployment

---

# 17. Code Quality

Planned tools:

- Checkstyle
- SpotBugs
- JaCoCo
- SonarQube or SonarCloud
- ESLint
- Prettier

---

# 18. Cloud Platform

## AWS

Planned AWS services:

- EC2 or ECS
- RDS
- S3
- CloudFront
- Route 53
- ACM
- SES
- CloudWatch
- Secrets Manager

The MVP will first run locally using Docker Compose.

---

# 19. Initial MVP Stack

The first implementation phase will use:

- Java 21
- Spring Boot
- Spring Security
- Spring Data JPA
- PostgreSQL
- Maven
- Spring Cloud Gateway
- Eureka
- Spring Cloud Config
- React
- TypeScript
- Docker
- Docker Compose
- JUnit
- Mockito
- Testcontainers
- OpenAPI
- Flyway

Advanced infrastructure will be added incrementally.