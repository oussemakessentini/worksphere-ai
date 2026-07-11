# Document Information

**Document:** Domain Model
**Project:** WorkSphere AI
**Version:** 1.0
**Status:** Draft
**Author:** Oussama Ksantini
**Last Updated:** 2026-07-10

---

# Domain Model

## Overview

WorkSphere AI manages the complete employee lifecycle.

The platform is divided into business domains.

Each domain groups closely related business entities and business rules.

These domains will later become independent microservices.

---

# Business Domains

## 1. Identity Domain

Responsible for authentication and authorization.

### Entities

- User
- Role
- Permission
- RefreshToken
- VerificationToken
- PasswordResetToken

---

## 2. Organization Domain

Represents the company structure.

### Entities

- Company
- Department
- Team
- Office
- Position

Relationships

Company

↓

Departments

↓

Teams

↓

Employees

---

## 3. Talent Domain

Responsible for recruitment.

### Entities

- Job
- Candidate
- Resume
- Application
- Interview
- InterviewFeedback
- Offer

Workflow

Candidate

↓

Application

↓

Interview

↓

Offer

↓

Employee

---

## 4. Workforce Domain

Represents employees.

### Entities

- Employee
- Manager
- Onboarding
- EmploymentContract
- EmploymentStatus

---

## 5. Learning Domain

Employee development.

### Entities

- LearningPath
- Course
- Module
- Quiz
- Question
- Answer
- QuizAttempt
- Certificate

---

## 6. Community Domain

Internal communication.

### Entities

- ForumCategory
- Post
- Comment
- Reaction
- Announcement

---

## 7. Recognition Domain

Employee engagement.

### Entities

- Recognition
- Badge
- Reward
- EmployeePoints
- EmployeeOfMonth

---

## 8. Notification Domain

### Entities

- Notification
- NotificationTemplate
- Email
- DeviceToken

---

## 9. Analytics Domain

### Entities

- Dashboard
- Metric
- ActivityLog
- AuditLog
- Report

---

## Future Domains

### AI Domain

- ResumeAnalysis
- CandidateScore
- AIRecommendation
- QuizGeneration
- LearningRecommendation

---

### Billing Domain

- Subscription
- Plan
- Invoice
- Payment

---

# High-Level Relationships

Company

↓

Department

↓

Team

↓

Employee

↓

Learning

↓

Recognition

---

Candidate

↓

Application

↓

Interview

↓

Offer

↓

Employee

---

Employee

↓

Forum

↓

Recognition

↓

Analytics

---

Employee

↓

Quiz

↓

Certificate