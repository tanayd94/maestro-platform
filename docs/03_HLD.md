# Maestro Platform

## High Level Design (HLD)

**Project Name:** Maestro Platform  
**Version:** 1.0  
**Author:** Tanay Dhupkar  
**Date:** July 2026

---

## 1. Purpose

The Maestro Platform is an AI-powered web application that enables independent music teachers to establish their online presence, manage student enquiries, automate repetitive communication using AI, and provide a professional experience to prospective students.

The platform is designed as a cloud-native, containerized application with modular services and future support for multi-teacher SaaS deployment.

---

## 2. Goals

### Functional Goals

- Teacher portfolio website
- Student enquiry management
- AI FAQ assistant using RAG
- Admin dashboard
- Content management
- Secure authentication

### Non-Functional Goals

- Highly maintainable
- Modular architecture
- Scalable
- Dockerized
- Cloud deployable
- API-first
- Production ready

---

## 3. System Architecture

### High-Level Application Split

```text
Frontend
   |
   v
Django API
   |
+--+--+
|     |
v     v
Core  AI Service
API
```

The frontend communicates only with the Django API. The Django API then routes requests to either the Core API layer for normal business operations or the AI Service layer for RAG-based chatbot workflows.

### Container-Level Architecture

```text
Internet
   |
   v
HTTPS (443)
   |
   v
Public DNS
   |
   v
Nginx Container
Reverse Proxy
   |
+--+------------------+
|                     |
v                     v
Next.js Frontend      Django REST API
                      |
                      v
              Authentication
              Business Logic
                      |
                      v
                 Django ORM
                      |
      +---------------+---------------+
      |               |               |
      v               v               v
PostgreSQL          Redis        Celery Worker
+ pgvector          Cache        Background Jobs
      |                               |
      +---------------+---------------+
                      |
                      v
              OpenAI + LangChain
```

### Why This Architecture?

Every component has one primary responsibility.

| Component | Responsibility |
| --- | --- |
| Next.js | UI |
| Django | Business logic |
| PostgreSQL | Persistent data |
| pgvector | Semantic search |
| Redis | Cache and broker |
| Celery | Async tasks |
| Nginx | Reverse proxy |
| OpenAI | AI generation |

No component should own two unrelated responsibilities.

---

## 4. Component Responsibilities

### Frontend

**Technology:** Next.js

**Responsibilities**

- Render UI
- Authentication screens
- Dashboard
- Forms
- AI chat UI

The frontend should not contain business logic.

### Backend

**Technology:** Django + Django REST Framework (DRF)

**Responsibilities**

- APIs
- Authentication
- Authorization
- Business rules
- ORM
- Validation

### Core API

**Responsibilities**

- Teacher profile APIs
- Course APIs
- Gallery APIs
- Video APIs
- Testimonial APIs
- Lead management APIs
- Dashboard APIs

### AI Service

**Responsibilities**

- Receive chat requests
- Generate embeddings
- Perform pgvector similarity search
- Build prompts using retrieved context
- Call OpenAI
- Return grounded answers

The AI Service should never answer directly without retrieval.

### PostgreSQL

**Responsibilities**

Store:

- Users
- Teachers
- Courses
- Leads
- Gallery items
- Videos
- Testimonials

### pgvector

**Responsibilities**

Store:

- Embeddings
- Chunks
- Metadata

pgvector is used only by the AI Service.

### Redis

**Responsibilities**

- Cache
- Celery broker
- Session cache
- Pub/Sub for future use

Redis should not store critical business data.

### Celery

**Responsibilities**

Background tasks:

- Send email
- Generate AI embeddings
- Optimize images
- Future WhatsApp automation

### OpenAI

**Responsibilities**

- Generate answers from retrieved context.

OpenAI should be called only through the RAG pipeline.

---

## 5. Request Flow

### Homepage

```text
Browser
   |
   v
Next.js
   |
   v
GET /teacher
   |
   v
Django API
   |
   v
Core API
   |
   v
PostgreSQL
   |
   v
JSON response
   |
   v
Next.js
   |
   v
Browser
```

### AI Chat

```text
User
   |
   v
Next.js
   |
   v
POST /chat
   |
   v
Django API
   |
   v
AI Service
   |
   v
Embedding
   |
   v
pgvector Similarity Search
   |
   v
Top Chunks
   |
   v
Prompt Builder
   |
   v
OpenAI
   |
   v
Answer
   |
   v
Browser
```

### Trial Booking

```text
User
   |
   v
Submit Form
   |
   v
Django API
   |
   v
Validation
   |
   v
PostgreSQL
   |
   v
Redis Event
   |
   v
Celery
   |
   v
Email
   |
   v
Dashboard Updated
```

Saving the enquiry does not wait for the email to be sent. This keeps the booking flow fast and uses asynchronous processing for slower work.

---

## 6. Authentication Flow

```text
Admin Login
   |
   v
JWT Access Token
   |
   v
Refresh Token
   |
   v
Protected APIs
   |
   v
Dashboard
```

Visitors do not need authentication.

---

## 7. AI Architecture

### Avoided Flow

```text
User
   |
   v
LLM
```

### Planned RAG Flow

```text
User
   |
   v
Query
   |
   v
Embedding
   |
   v
pgvector Search
   |
   v
Relevant Documents
   |
   v
Prompt Builder
   |
   v
LLM
   |
   v
Answer
```

This reduces hallucinations and ensures responses come from Shubhada's actual information.

---

## 8. Deployment Architecture

```text
AWS EC2
   |
   v
Docker Compose
   |
   +-- nginx
   +-- frontend
   +-- backend
   +-- postgres
   +-- redis
   +-- celery
```

Everything runs inside Docker containers.

---

## 9. Security

| Area | Approach |
| --- | --- |
| Authentication | JWT |
| Authorization | Role-based access |
| HTTPS | Nginx |
| Passwords | BCrypt |
| SQL injection | Prevented via Django ORM |
| XSS | Frontend sanitization |
| CSRF | Handled by Django where applicable |
| Rate limiting | Redis |

---

## 10. Scalability Strategy

### Today

- 1 teacher

### Tomorrow

- 100+ teachers

The system should support growth without requiring a database redesign. Scaling should primarily happen through horizontal scaling and tenant-aware data modeling.

---

## 11. Future Expansion

The architecture already supports:

- Multiple teachers
- Student portal
- Payments
- Mobile app
- Analytics
- Recommendation engine
- AI practice review
- WhatsApp integration

No major redesign should be required for these future capabilities.

---

## 12. Design Principles

The project follows:

- Separation of concerns
- Single Responsibility Principle
- API-first design
- Event-driven background processing
- Modular Django apps
- Containerized deployment
- Stateless backend
- RESTful APIs

