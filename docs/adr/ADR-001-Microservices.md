# Document Information

**Document:** ADR-001 – Adopt Microservices Architecture  
**Project:** WorkSphere AI  
**Version:** 1.0  
**Status:** Accepted  
**Author:** Oussama Ksantini  
**Last Updated:** 2026-07-10

---

# ADR-001: Adopt Microservices Architecture

## 1. Context

WorkSphere AI is designed to manage multiple business capabilities, including:

- Authentication
- Recruitment
- Employee management
- Learning
- Community
- Recognition
- Notifications
- Analytics
- AI features

These areas have different responsibilities, data models, scaling needs, and development lifecycles.

The project is also intended to provide practical experience with:

- Spring Cloud
- API Gateway
- Service discovery
- Centralized configuration
- Kafka
- Circuit breakers
- Load balancing
- Distributed logging
- Monitoring
- Distributed tracing
- Docker
- AWS deployment

A monolithic architecture would be easier to build initially, but it would not provide the same learning opportunities or demonstrate distributed-system design.

---

## 2. Decision

WorkSphere AI will use a microservices architecture.

The initial implementation will use a small number of domain-oriented services rather than creating one service per entity or feature.

Initial services:

1. Config Server
2. Discovery Service
3. API Gateway
4. Identity Service
5. Talent Service
6. Workforce Service
7. Learning Service
8. Engagement Service

Future services may include:

- Notification Service
- Analytics Service
- AI Service
- Billing Service
- File Service

Services will be split only when there is a clear business, deployment, ownership, or scaling reason.

---

## 3. Architectural Rules

- Every service must have a clearly defined responsibility.
- Every business entity must have one owning service.
- Each business service owns its database.
- Services must not directly access another service’s database.
- Synchronous communication uses REST.
- Asynchronous communication uses Kafka.
- Public traffic enters through the API Gateway.
- Services register with the Discovery Service.
- Shared configuration is provided by the Config Server.
- Shared libraries must not contain domain-specific business logic.
- Circular service dependencies must be avoided.
- Services should remain independently deployable.

---

## 4. Why Microservices Were Chosen

### Independent Development

Each business capability can evolve separately.

For example, the Learning Service can change without requiring changes to the Talent Service.

### Independent Deployment

Services can be built and deployed separately.

### Scalability

High-demand services can scale independently.

For example:

- Talent Service may receive heavy traffic during recruiting campaigns.
- Learning Service may receive heavy traffic during mandatory training.
- Engagement Service may receive frequent forum and notification activity.

### Fault Isolation

A failure in one service should not bring down the entire platform.

### Technology Practice

The architecture provides realistic opportunities to implement:

- Service discovery
- Load balancing
- Resilience patterns
- Event-driven communication
- Centralized logging
- Distributed tracing
- Monitoring
- Container orchestration

### Portfolio Value

The project demonstrates more than CRUD development. It demonstrates architectural decision-making and distributed-system engineering.

---

## 5. Alternatives Considered

## 5.1 Traditional Monolith

### Advantages

- Simpler development
- Easier debugging
- Easier local setup
- Simple transactions
- Faster initial delivery

### Disadvantages

- Tight coupling
- One deployment unit
- Harder independent scaling
- Limited distributed-systems practice
- Larger long-term codebase

### Reason Rejected

The monolith does not meet the project’s learning goals and long-term architecture vision.

---

## 5.2 Modular Monolith

### Advantages

- Strong internal boundaries
- Simpler operations
- Easier testing
- Easier transactions
- Lower infrastructure complexity

### Disadvantages

- Still one deployment unit
- No real network communication
- No service discovery
- Limited fault-tolerance practice
- Limited experience with event-driven microservices

### Reason Not Selected as Final Architecture

A modular monolith would be the safest production choice for a small team. However, WorkSphere AI is also a structured learning project focused on microservices and cloud engineering.

The project will still apply modular design principles inside every service.

---

## 5.3 Many Fine-Grained Microservices

Example:

- Auth Service
- User Service
- Company Service
- Department Service
- Employee Service
- Recruitment Service
- Interview Service
- Offer Service
- Quiz Service
- Certificate Service
- Forum Service
- Recognition Service
- Notification Service

### Advantages

- Very small deployment units
- Maximum separation
- Fine-grained scaling

### Disadvantages

- Excessive boilerplate
- Too many repositories or modules
- Complex local development
- More network calls
- Harder debugging
- Increased DevOps overhead
- High risk of distributed monolith behavior

### Reason Rejected

This would be too complex for the MVP and could prevent the project from being completed.

---

## 6. Consequences

## Positive Consequences

- Clear domain boundaries
- Independent databases
- Independent deployment
- Realistic distributed-system practice
- Natural use of Kafka
- Easier service-specific scaling
- Strong portfolio and interview value

## Negative Consequences

- More infrastructure
- More configuration
- More Docker containers
- Harder debugging
- Network failures
- Distributed transactions
- Eventual consistency
- More testing complexity
- More operational overhead

---

## 7. Risks

### Risk: The Project Becomes Too Large

Mitigation:

- Limit the initial service count.
- Build a focused MVP.
- Keep future services in the roadmap.
- Do not split services prematurely.

### Risk: Distributed Monolith

Mitigation:

- Avoid excessive synchronous calls.
- Use domain events for lifecycle transitions.
- Prevent shared database access.
- Avoid circular dependencies.

### Risk: Local Development Complexity

Mitigation:

- Use Docker Compose.
- Provide startup scripts.
- Use health checks.
- Document service startup order.
- Introduce infrastructure incrementally.

### Risk: Data Consistency

Mitigation:

- Prefer eventual consistency.
- Use idempotent event consumers.
- Introduce saga patterns only when required.
- Avoid cross-service database transactions.

### Risk: Service Duplication

Mitigation:

- Maintain service-boundary documentation.
- Assign ownership for every entity.
- Document APIs and events before implementation.

---

## 8. Implementation Strategy

The project will not introduce all distributed-system components on the first day.

### Stage 1

- Config Server
- Discovery Service
- API Gateway
- Identity Service
- One business service
- PostgreSQL
- Docker Compose

### Stage 2

- Remaining MVP services
- REST communication
- OpenFeign
- Load balancing

### Stage 3

- Kafka
- Event-driven workflows
- Idempotent consumers

### Stage 4

- Resilience4j
- Circuit breaker
- Retry
- Timeouts
- Fallbacks

### Stage 5

- Centralized logging
- Metrics
- Distributed tracing
- AWS deployment

---

## 9. Validation Criteria

The decision will be considered successful when:

- Services can start and deploy independently.
- Each service owns its data.
- Clients access services through the API Gateway.
- Service discovery supports multiple instances.
- Configuration is centralized.
- Cross-service failures are handled safely.
- Kafka supports important lifecycle events.
- Logs and traces can follow requests across services.
- The MVP remains understandable and maintainable.

---

## 10. Review Conditions

This decision should be reviewed if:

- Development becomes unmanageable.
- Service boundaries repeatedly cause circular dependencies.
- Infrastructure work prevents business features from progressing.
- The system behaves like a distributed monolith.
- The project cannot reach a deployable MVP within the planned timeline.

If those conditions occur, some business services may be temporarily merged without abandoning the long-term architecture.