# Maestro Platform

## User Stories & Acceptance Criteria

**Version:** 1.0 MVP

---

## Epic 1 - Public Website

### US-001: View Home Page

**User Story**

As a visitor, I want to land on a professional homepage so that I can quickly understand who the teacher is and what she offers.

**Acceptance Criteria**

- Homepage loads within 2 seconds.
- Displays hero section.
- Shows CTAs:
  - Book Trial Class
  - Ask AI
- Shows featured performance.
- Mobile responsive.

**Priority:** High

### US-002: View Teacher Profile

**User Story**

As a visitor, I want to know about the teacher so I can decide whether she is suitable for me.

**Acceptance Criteria**

- Displays:
  - Biography
  - Teaching experience
  - Qualifications
  - Awards
  - Instruments taught
  - Languages spoken
  - Teaching philosophy

**Priority:** High

### US-003: Browse Courses

**User Story**

As a visitor, I want to explore available music courses before contacting the teacher.

**Acceptance Criteria**

- Every course displays:
  - Name
  - Instrument
  - Level
  - Duration
  - Online/Offline
  - Description

**Priority:** High

### US-004: View Gallery

**User Story**

As a visitor, I want to see photos and performances so I can evaluate the teacher's experience.

**Acceptance Criteria**

- Supports:
  - Images
  - Videos
  - YouTube embeds

**Priority:** Medium

### US-005: Read Testimonials

**User Story**

As a visitor, I want to read reviews from students so that I gain confidence before enrolling.

**Acceptance Criteria**

- Displays:
  - Student name
  - Rating
  - Review
  - Date

**Priority:** Medium

---

## Epic 2 - AI Assistant

### US-006: Ask AI Questions

**User Story**

As a visitor, I want to ask questions about the teacher and courses so I receive immediate answers without waiting for a reply.

**Acceptance Criteria**

- AI answers questions about:
  - Fees
  - Timings
  - Instruments
  - Teaching experience
  - Online classes
  - Trial classes
  - Location
- Response time is less than 5 seconds.
- If an answer is unavailable, display: `"I'm unable to answer that. Please submit an enquiry."`

**Priority:** High

### US-007: AI Uses RAG

**User Story**

As a visitor, I want AI answers to be based on the teacher's actual information rather than fabricated responses.

**Acceptance Criteria**

- Retrieves information from:
  - FAQ
  - Teacher profile
  - Courses
  - Documents
- No direct LLM answers without retrieval.

**Priority:** High

---

## Epic 3 - Lead Management

### US-008: Submit Trial Booking

**User Story**

As a parent, I want to submit a trial booking request so the teacher can contact me.

**Acceptance Criteria**

- Required fields:
  - Name
  - Phone
  - Instrument
  - Preferred mode
  - Preferred timing
- Validation:
  - Phone number
  - Required fields
- Creates a lead with status `NEW`.

**Priority:** Critical

### US-009: Duplicate Protection

**User Story**

As a teacher, I don't want duplicate enquiries from accidental repeated submissions.

**Acceptance Criteria**

- Prevent duplicate submissions within 5 minutes using the same phone number or email.

**Priority:** Medium

---

## Epic 4 - Dashboard

### US-010: Login

**User Story**

As a teacher, I want secure login access so only I can manage the website.

**Acceptance Criteria**

- JWT authentication is required.
- Invalid credentials show an error.

**Priority:** Critical

### US-011: View Leads

**User Story**

As a teacher, I want to view all enquiries in one place.

**Acceptance Criteria**

- Displays:
  - Name
  - Phone
  - Instrument
  - Date
  - Status
- Search is supported.

**Priority:** High

### US-012: Update Lead Status

**User Story**

As a teacher, I want to update enquiry progress.

**Acceptance Criteria**

- Supported statuses:
  - `NEW`
  - `CONTACTED`
  - `TRIAL BOOKED`
  - `JOINED`
  - `LOST`
- Status updates immediately.

**Priority:** High

### US-013: Manage Courses

**User Story**

As a teacher, I want to update courses without contacting a developer.

**Acceptance Criteria**

- CRUD operations are supported:
  - Create
  - Edit
  - Delete

**Priority:** High

### US-014: Manage Gallery

**User Story**

As a teacher, I want to upload photos and videos.

**Acceptance Criteria**

- Supports:
  - Images
  - YouTube URLs

**Priority:** Medium

### US-015: Manage Testimonials

**User Story**

As a teacher, I want to add or remove testimonials.

**Acceptance Criteria**

- CRUD is supported.

**Priority:** Medium

---

## Epic 5 - Notifications

### US-016: Email Notification

**User Story**

As a teacher, I want to receive an email whenever a new enquiry is submitted.

**Acceptance Criteria**

- Triggered asynchronously using Celery.

**Priority:** Medium

---

## Epic 6 - Performance

### US-017: Fast Website

**User Story**

As a visitor, I expect pages to load quickly.

**Acceptance Criteria**

- Homepage loads in less than 2 seconds.
- API responds in less than 500 ms, excluding AI requests.

**Priority:** High

---

## Epic 7 - Security

### US-018: Secure APIs

**User Story**

As a developer, I want unauthorized users to be prevented from accessing admin APIs.

**Acceptance Criteria**

- JWT is required.
- `401` is returned for unauthorized access.

**Priority:** Critical

---

## MVP Definition of Done (DoD)

A feature is considered complete only if:

- Functional requirements are implemented.
- API is documented in Swagger/OpenAPI.
- Unit tests are written where practical.
- Validation is completed.
- Feature is Dockerized.
- Code is reviewed.
- API is tested with Postman.
- UI is responsive.
- No critical bugs remain.

