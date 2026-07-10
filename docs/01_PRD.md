# Maestro

## Product Requirements Document (PRD)

**Sprint:** Sprint 0 - Product Planning  
**Deliverable:** Deliverable 1 - Product Requirements Document  
**Project Name:** Maestro (Working Codename)  
**Version:** 1.0 MVP  
**Author:** Tanay Dhupkar  
**Date:** July 2026

---

## 1. Product Vision

### Vision

Build an AI-powered platform that helps independent music teachers establish a professional online presence, manage student enquiries, automate repetitive tasks, and grow their teaching business.

The first customer and pilot user is Shubhada, a violinist and music teacher based in Mumbai.

The platform will initially support a single teacher but will be architected to support multiple teachers in the future.

---

## 2. Problem Statement

Independent music teachers face several challenges:

- No professional online presence.
- Dependence on WhatsApp and word-of-mouth.
- Student enquiries are scattered across multiple channels.
- Repeatedly answering the same questions.
- Difficulty managing leads and trial classes.
- No centralized student CRM.
- No analytics.

---

## 3. Objectives

### Primary Objectives

- Increase student enquiries.
- Increase trial class bookings.
- Improve teacher discoverability.
- Reduce manual communication.
- Build teacher credibility.

### Secondary Objectives

- Showcase backend engineering skills.
- Demonstrate AI integration.
- Build a production-grade portfolio project.
- Create a scalable SaaS foundation.

---

## 4. Success Metrics (MVP)

### Business

- Website is publicly accessible.
- Teacher receives enquiries through website.
- AI chatbot answers FAQs.
- Trial bookings are managed from dashboard.

### Technical

- Dockerized deployment.
- PostgreSQL database.
- Redis caching.
- JWT authentication.
- AI RAG implemented.
- AWS deployment.

### Portfolio

- Public GitHub repository.
- Live demo.
- Documentation.
- Architecture diagrams.

---

## 5. Target Users

### Primary User: Music Teacher

**Example:** Shubhada

**Goals**

- Get students.
- Build online presence.
- Manage enquiries.
- Showcase performances.

**Pain Points**

- Manual communication.
- No CRM.
- No website.
- No AI assistant.

### Secondary User: Parent

**Goals**

- Find music teacher.
- Check teaching quality.
- Book trial.

### Third User: Student

**Goals**

- Learn music.
- Contact teacher.
- Ask questions.
- View performances.

---

## 6. User Stories

### Guest

As a visitor, I should be able to:

- View teacher profile.
- View performances.
- Read testimonials.
- Ask AI questions.
- Submit enquiry.
- Book trial class.

### Teacher

As a teacher, I should be able to:

- Login.
- Update profile.
- Add videos.
- Upload photos.
- Manage enquiries.
- Reply to leads.
- View analytics.

---

## 7. MVP Scope

### Included

- Landing page
- About
- Courses
- Gallery
- Videos
- Testimonials
- Contact
- AI chatbot
- Lead form
- Admin dashboard
- JWT authentication

### Excluded

- Payments
- Student login
- Attendance
- Google Calendar
- WhatsApp automation
- Multi-teacher UI
- Mobile app

---

## 8. Functional Requirements

### Landing Page

Display:

- Hero section
- CTA
- Teacher introduction
- Featured performances

### Teacher Profile

Display:

- Biography
- Qualifications
- Awards
- Experience
- Instruments

### Courses

Display:

- Name
- Duration
- Mode
- Level
- Description

### Gallery

Display:

- Images
- Videos

### Testimonials

- Display student reviews.

### AI Chat

Allow users to ask about:

- Fees
- Timings
- Location
- Experience
- Online classes
- Instruments
- Trial class

Answers are generated using RAG + OpenAI.

### Lead Management

Capture:

- Name
- Parent name
- Phone
- Email
- Instrument
- Preferred timing
- Mode
- Message

### Dashboard

Teacher can:

- View leads
- Update status
- Manage website content
- View statistics

---

## 9. Non-Functional Requirements

### Availability

- 99%

### Performance

- Page load time under 2 seconds.

### Security

- JWT
- HTTPS
- Input validation
- SQL injection prevention

### Scalability

Architecture should support:

- 100+ teachers

### Maintainability

- Modular Django apps.

---

## 10. Technology Stack

### Frontend

- Next.js
- TypeScript
- Tailwind

### Backend

- Django
- Django REST Framework (DRF)

### Database

- PostgreSQL
- pgvector

### Cache

- Redis Stack

### Background Tasks

- Celery

### AI

- LangChain
- OpenAI

### Infrastructure

- Docker
- Nginx
- AWS

---

## 11. Risks

### OpenAI API Cost

**Mitigation:** Cache responses.

### Large Media Uploads

**Mitigation:** Store on S3 later.

### Spam Enquiries

**Mitigation:** Google reCAPTCHA.

### Hallucinations

**Mitigation:** RAG.

---

## 12. Future Roadmap

### Version 2

- Student portal
- WhatsApp integration
- Calendar
- Payment gateway
- Attendance
- AI content generator
- AI practice feedback
- Mobile app
- Multi-teacher SaaS

