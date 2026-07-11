# Document Information

**Document:** Microservice Boundaries  
**Project:** WorkSphere AI  
**Version:** 1.0  
**Status:** Draft  
**Author:** Oussama Ksantini  
**Last Updated:** 2026-07-10

---

# Microservice Boundaries

## 1. Purpose

This document defines the initial microservices of WorkSphere AI, their responsibilities, owned data, communication patterns, and boundaries.

The MVP will use a limited number of services to keep development manageable while still practicing real microservices concepts.

---

# 2. Initial Services

## 2.1 API Gateway

### Responsibilities

- Single entry point for client applications
- Route requests to internal services
- Validate access tokens
- Apply rate limiting
- Add correlation IDs
- Handle CORS
- Centralize public API exposure

### Owns Data

None.

### Communicates With

- Identity Service
- Talent Service
- Workforce Service
- Learning Service
- Engagement Service

---

## 2.2 Discovery Service

### Responsibilities

- Service registration
- Service discovery
- Support client-side load balancing
- Track available service instances

### Technology

- Spring Cloud Netflix Eureka

### Owns Data

None.

---

## 2.3 Identity Service

### Responsibilities

- User registration
- Login
- Logout
- Email verification
- Password reset
- Refresh tokens
- Roles
- Permissions
- Authentication
- Account status

### Owned Entities

- User
- Role
- Permission
- RefreshToken
- VerificationToken
- PasswordResetToken

### Publishes Events

- UserRegistered
- UserVerified
- UserRoleAssigned
- UserAccountLocked

### Does Not Own

- Candidate data
- Employee data
- Company data
- Recruitment data

---

## 2.4 Talent Service

### Responsibilities

- Job openings
- Candidate profiles
- Resumes
- Job applications
- Interview stages
- Interview feedback
- Offer management
- Recruitment workflow

### Owned Entities

- CandidateProfile
- Resume
- JobOpening
- Application
- Interview
- InterviewFeedback
- Offer

### Publishes Events

- CandidateApplied
- ApplicationStatusChanged
- InterviewScheduled
- OfferCreated
- OfferAccepted
- OfferRejected

### Consumes Events

- UserRegistered
- UserVerified

### Important Rule

The Talent Service does not create employee records directly.

When an offer is accepted, it publishes `OfferAccepted`.

The Workforce Service consumes this event and creates the employee profile.

---

## 2.5 Workforce Service

### Responsibilities

- Company management
- Departments
- Teams
- Positions
- Employee profiles
- Manager assignments
- Employment status
- Onboarding checklists
- Recognition
- Employee points
- Employee of the Month

### Owned Entities

- Company
- Department
- Team
- Position
- EmployeeProfile
- ManagerAssignment
- OnboardingChecklist
- OnboardingTask
- Recognition
- EmployeePoints
- EmployeeOfMonth

### Publishes Events

- CompanyCreated
- EmployeeCreated
- EmployeeAssignedToTeam
- OnboardingStarted
- OnboardingCompleted
- RecognitionGiven
- EmployeeOfMonthSelected

### Consumes Events

- OfferAccepted
- QuizCompleted
- CertificateIssued
- UserRegistered

### Important Rule

The Workforce Service owns the transition from candidate to employee.

It does not manage authentication credentials.

---

## 2.6 Learning Service

### Responsibilities

- Learning paths
- Courses
- Modules
- Question bank
- Quizzes
- Quiz attempts
- Quiz scoring
- Certificates

### Owned Entities

- LearningPath
- Course
- CourseModule
- Quiz
- Question
- AnswerOption
- QuizAttempt
- QuizResponse
- Certificate

### Publishes Events

- LearningPathAssigned
- QuizAssigned
- QuizStarted
- QuizCompleted
- CertificateIssued

### Consumes Events

- EmployeeCreated
- OnboardingStarted

---

## 2.7 Engagement Service

### Responsibilities

- Forum categories
- Posts
- Comments
- Reactions
- Announcements
- In-app notifications
- News feed

### Owned Entities

- ForumCategory
- Post
- Comment
- Reaction
- Announcement
- Notification

### Publishes Events

- PostCreated
- CommentCreated
- ReactionAdded
- AnnouncementPublished
- NotificationCreated

### Consumes Events

- UserRegistered
- EmployeeCreated
- InterviewScheduled
- OfferCreated
- QuizAssigned
- CertificateIssued
- RecognitionGiven
- EmployeeOfMonthSelected

---

# 3. Future Services

These services are not part of the initial MVP.

## Analytics Service

- Aggregated metrics
- Dashboard projections
- Reports
- Engagement trends
- Recruitment statistics

## AI Service

- Resume analysis
- Candidate ranking
- Quiz generation
- Interview question generation
- Learning recommendations

## Billing Service

- Subscription plans
- Payments
- Invoices
- Usage limits

## File Service

- Resume storage
- Profile pictures
- Certificates
- Company logos
- Document metadata

---

# 4. Database Ownership

Each service owns its own PostgreSQL database.

```text
identity_db
talent_db
workforce_db
learning_db
engagement_db