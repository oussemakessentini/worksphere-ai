# Document Information

**Document:** Database Strategy
**Project:** WorkSphere AI
**Version:** 1.0
**Status:** Draft
**Author:** Oussama Ksantini
**Last Updated:** 2026-07-11

---

# Purpose

This document defines the database architecture of WorkSphere AI.

It establishes the rules governing data ownership, persistence, consistency, identifiers, auditing, and communication between services.

---

# Database Philosophy

WorkSphere AI follows the **Database per Service** pattern.

Each microservice owns its own database.

No database is shared.

Each service is the single source of truth for its own business entities.

---

# Initial Databases

Identity Database

```
identity_db
```

Talent Database

```
talent_db
```

Workforce Database

```
workforce_db
```

Learning Database

```
learning_db
```

Engagement Database

```
engagement_db
```

---

# Database Ownership

Each service owns:

- schema
- tables
- indexes
- migrations
- constraints

No other service may modify its data directly.

---

# Cross-Service Communication

Services never perform joins across databases.

Instead they communicate using:

- REST APIs
- Kafka Events

---

# Primary Keys

All entities use UUID as their primary key.

Example

```
Employee

id

UUID
```

Reasons

- Distributed systems
- Multi-tenancy
- Kafka
- Independent databases
- Easier replication

---

# Foreign Keys

Foreign keys exist only inside the same service.

Example

Learning Service

Quiz

↓

Questions

↓

Answers

Allowed.

---

Employee Service

↓

Quiz Table

❌ Not allowed.

Cross-service relationships are represented using UUID references.

---

# Example

EmployeeProfile

```
employeeId

UUID
```

QuizAttempt

```
employeeId

UUID
```

Learning Service does not know Employee details.

It only stores Employee UUID.

---

# Multi-Tenant Strategy

Every business entity belongs to one company.

Most tables include

```
company_id
```

This allows strict tenant isolation.

Identity Service is the exception because users may exist before joining a company.

---

# Auditing

Every entity should contain

created_at

created_by

updated_at

updated_by

These values are automatically maintained.

---

# Soft Delete

Business data should not be permanently deleted.

Instead

```
deleted

deleted_at
```

or

```
status = DELETED
```

Historical data is preserved.

---

# Migrations

Flyway manages all schema changes.

Rules

- No manual production changes
- One migration per schema change
- Version controlled

---

# Transactions

Transactions are local to one service.

Cross-service transactions are avoided.

Business workflows use:

- Domain Events
- Eventual Consistency

---

# File Storage

Binary files are not stored in PostgreSQL.

Examples

- resumes
- certificates
- avatars
- logos

Stored in:

Amazon S3

Database stores only metadata.

---

# Naming Convention

Tables

snake_case

Columns

snake_case

Primary Key

```
id
```

Foreign Keys

```
employee_id

company_id

quiz_id
```

---

# Indexing

Indexes should exist on:

- email
- username
- company_id
- created_at
- status

Additional indexes are created only when justified.

---

# Future Improvements

- Read replicas
- Database partitioning
- CQRS read models
- Event sourcing (research only)
- Materialized views