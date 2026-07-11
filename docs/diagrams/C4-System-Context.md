# Document Information

**Document:** C4 System Context Diagram  
**Project:** WorkSphere AI  
**Version:** 1.0  
**Status:** Draft  
**Author:** Oussama Ksantini  
**Last Updated:** 2026-07-11

---

# C4 System Context Diagram

## Purpose

This diagram shows WorkSphere AI at the highest level.

It identifies:

- Who uses the platform
- Which external systems interact with it
- The primary responsibilities of WorkSphere AI

It intentionally does not show individual microservices or databases.

---

## System Context

```mermaid
flowchart LR
    PLATFORM_OWNER["Platform Owner<br/>Manages tenants, subscriptions,<br/>modules and platform operations"]

    COMPANY_ADMIN["Company Owner / Administrator<br/>Configures company, roles,<br/>permissions and organization"]

    HR["HR Manager / Recruiter<br/>Manages jobs, candidates,<br/>interviews, offers and onboarding"]

    MANAGER["Manager<br/>Manages teams, projects,<br/>learning and recognition"]

    EMPLOYEE["Employee<br/>Completes work, learning,<br/>attendance and collaboration"]

    CANDIDATE["Candidate<br/>Searches jobs, applies,<br/>interviews and accepts offers"]

    WORKSPHERE["WorkSphere AI<br/><br/>Global Workforce Operating System<br/>for recruitment, workforce management,<br/>learning, engagement and analytics"]

    EMAIL["Email Provider<br/>Account verification, invitations,<br/>offers and notifications"]

    STORAGE["Cloud File Storage<br/>Resumes, documents,<br/>images and certificates"]

    CALENDAR["Calendar Providers<br/>Google Calendar and<br/>Microsoft Outlook"]

    GITHUB["GitHub / GitLab<br/>Repositories, tasks,<br/>pull requests and webhooks"]

    COLLAB["Slack / Microsoft Teams<br/>Notifications and<br/>collaboration integrations"]

    AI["AI Provider<br/>Resume analysis, quiz generation,<br/>recommendations and insights"]

    PAYROLL["Payroll / HR Providers<br/>Compensation and<br/>payroll integrations"]

    PLATFORM_OWNER --> WORKSPHERE
    COMPANY_ADMIN --> WORKSPHERE
    HR --> WORKSPHERE
    MANAGER --> WORKSPHERE
    EMPLOYEE --> WORKSPHERE
    CANDIDATE --> WORKSPHERE

    WORKSPHERE --> EMAIL
    WORKSPHERE --> STORAGE
    WORKSPHERE --> CALENDAR
    WORKSPHERE --> GITHUB
    WORKSPHERE --> COLLAB
    WORKSPHERE --> AI
    WORKSPHERE --> PAYROLL
```

---

# Primary Actors

## Platform Owner

Operates the WorkSphere AI SaaS platform.

Responsibilities include:

- Tenant management
- Subscription management
- Module activation
- Platform monitoring
- Support and administration

---

## Company Owner or Administrator

Configures a company tenant.

Responsibilities include:

- Company settings
- Departments and teams
- Offices and positions
- Roles and permissions
- Module configuration
- Company branding

---

## HR Manager or Recruiter

Manages the talent lifecycle.

Responsibilities include:

- Job postings
- Candidate review
- Interviews
- Offers
- Hiring
- Employee onboarding

---

## Manager

Manages employees and team operations.

Responsibilities include:

- Team assignments
- Projects and tasks
- Learning progress
- Recognition
- Meetings
- Team analytics

---

## Employee

Uses WorkSphere AI during daily work.

Responsibilities include:

- Profile management
- Onboarding
- Learning and quizzes
- Projects and tasks
- Attendance
- Collaboration
- Recognition

---

## Candidate

Uses the public recruitment portal.

Responsibilities include:

- Candidate profile
- Resume upload
- Job applications
- Interview scheduling
- Offer acceptance

---

# External Systems

## Email Provider

Supports:

- Email verification
- Password reset
- Employee invitations
- Interview notifications
- Offer delivery
- Training reminders

---

## Cloud File Storage

Stores:

- Resumes
- Employee documents
- Company logos
- Profile images
- Course files
- Certificates

---

## Calendar Providers

Support:

- Interview scheduling
- Company meetings
- Training sessions
- Calendar synchronization
- Meeting invitations

---

## GitHub and GitLab

Support:

- Repository connections
- Pull request tracking
- Webhooks
- Task linking
- Development activity synchronization

---

## Slack and Microsoft Teams

Support:

- Company notifications
- Project updates
- Recognition announcements
- Collaboration workflows

---

## AI Provider

Supports:

- Resume analysis
- Candidate matching
- Quiz generation
- Interview preparation
- Learning recommendations
- Analytics summaries

---

## Payroll and HR Providers

Future integrations may support:

- Payroll export
- Compensation synchronization
- Benefits information
- Employee record synchronization

---

# System Boundary

WorkSphere AI owns:

- Authentication and authorization
- Tenant management
- Recruitment workflows
- Employee profiles
- Organization structure
- Learning and quizzes
- Recognition
- Engagement
- Internal business workflows

External providers remain responsible for their specialized capabilities, such as email delivery, cloud storage, payroll processing and third-party calendars.