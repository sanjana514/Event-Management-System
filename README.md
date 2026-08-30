# 🎉 Festive Flow — Event Management System

A full-stack Event Management System built with **Oracle APEX** and **SQL** for the course **CSE302: Database Systems (Section 06), Fall 2024**, East West University.

> ⚠️ **Security note:** All login credentials, workspace passwords, and session URLs originally included in the project report have been **redacted** from this README before publishing. See [Security](#-security-notes) below before sharing this repo or the live app link publicly.

---

## 📌 Project Info

| | |
|---|---|
| **Course** | CSE302: Database Systems (Section 06) |
| **Semester** | Fall 2024 |
| **Group** | 9 (Pandas) |
| **Project Name** | Festive Flow |
| **Platform** | Oracle APEX |


## 📖 Overview

**Festive Flow** is a database-driven event management platform that lets organizers create and manage events, sell tickets (Regular & VIP), register attendees, collect payments, gather feedback, and coordinate staff (employees, volunteers, admins) and sponsors — all through a role-based Oracle APEX web application backed by a relational SQL database.

### ✨ Key Features

- **Role-based access control** — Admins can view and manage all data (including admin-only tables); regular users (Organizers, Attendees, Volunteers, Sponsors) are restricted from sensitive tables via APEX page-level authorization.
- **Automated trigger** — A database trigger calculates `DaysUntilEvent` dynamically at insert time by comparing the event date to the current date. If the event has already happened, the value goes negative, indicating how many days have passed.
- **20 CRUD interfaces** — Full Report + Form pages for every core table (Users, Event, Organizer, Attendee, Ticket, Registration, Activity, Feedback, Payment, Venue, Employee, Volunteer, Admin, Sponsor, and related lookup tables).
- **6 analytical reports** — Multi-table and aggregate SQL queries summarizing event activities, sponsors, ticket sales, payments, and VIP attendee details.

---

## 🗂️ Database Design

### 1. Entity-Relationship (E-R) Model
The system models core entities including `Event`, `Organizer`, `Venue`, `Attendee`, `Ticket` (with `VIPTicket`/`RegularTicket` subtypes via ISA), `Registration`, `Payment`, `Activity`, `Feedback`, `Sponsor`, `Equipment`, and `Employee` (with `Volunteer`/`Admin` subtypes via ISA).

*See the full E-R diagram in the project report (`Section 1`).*

### 2. Relational Schema
The E-R model was mapped into normalized relational tables — e.g. `Event`, `Organizer`, `OrganizerPhone`, `OrganizerAddress`, `Venue`, `Attendee`, `Ticket`, `VIPTicket`, `RegularTicket`, `Registration`, `Activity`, `Feedback`, `Payment`, `Employee`, `Volunteer`, `Admin`, `Sponsor`, and `Users` — with primary/foreign key constraints enforcing referential integrity.

*See the full schema diagram in the project report (`Section 2`).*

### 3. Notable Trigger
```sql
-- Conceptual logic (see APEX app for the actual PL/SQL trigger)
-- On INSERT INTO Event:
--   DaysUntilEvent := EventDate - SYSDATE;
--   (negative value => the event has already passed)
```

---

## 🧩 Application Structure

### Core CRUD Modules (Report + Form pages)
Users · Event · Organizer · OrganizerPhone · OrganizerAddress · Attendee · Ticket · RegularTicket · VIPTicket · Registration · Activity · Feedback · Payment · Venue · Hosted · Equipment · Employee · Volunteer · Admin · Sponsor

### Analytical Reports (Multi-table / Aggregate Queries)
| Report | Type | Description |
|---|---|---|
| EventActivityDetails | Aggregate | Event + activity info, with total activities per event |
| EventSponsorDetails | Multi-table | Event and their sponsor details |
| EventFullDetails | Multi-table | Event, organizer, and venue information combined |
| TicketDetails | Multi-table | Ticket, attendee, and ticket-type information |
| EventPaymentSummary | Aggregate | Total payment collected per event |
| VIPAttendeeDetails | Multi-table | VIP attendees, their events, ticket prices, and facilities |

---

## 🔐 Authorization & Roles

Access is controlled through Oracle APEX's page-level authorization schemes:

- **Admin roles** (e.g. Supervisor, CEO, Manager, Proctor) can view and manage the `Admin` table and all other data.
- **Non-admin roles** (Organizer, Attendee, Volunteer, Sponsor) are denied access to admin-only pages — attempting to access them returns an **Access Denied** page via APEX's built-in security check.

> Credential tables (usernames/passwords/workspace secrets) that were part of the original coursework submission are **intentionally omitted here** — see [Security Notes](#-security-notes).

---

## 🛠️ Tech Stack

- **Database & Backend:** Oracle Database, PL/SQL (triggers, constraints)
- **Application Layer:** Oracle APEX (low-code report/form generation, page-level authorization schemes)
- **Query Types:** Multi-table joins, aggregate functions (`COUNT`, `SUM`), foreign-key relationships across 15+ tables

---

## 🔒 Security Notes

This project was originally submitted as academic coursework with real Oracle APEX workspace credentials, admin usernames/passwords, and a session-based app URL included in the report. Before publishing or sharing this project publicly:

- [ ] **Rotate/change all passwords** for every user in the `Users`/`Admin` tables (especially admin-role accounts) in the live APEX workspace.
- [ ] **Do not commit** the original PDF/DOCX report as-is if it still contains the credential table or workspace password — redact those sections first.
- [ ] Treat the `session=...` query string in any shared APEX URL as **not a secret on its own**, but avoid sharing live admin URLs regardless.
- [ ] Consider deactivating or deleting the APEX app/workspace once grading is complete if it's no longer needed, to remove the exposure entirely.

---

## 📝 Concluding Remarks

Completing this Event Management System project in SQL on Oracle APEX was a valuable exercise in database design, query writing, and building a role-secured application from a conceptual E-R model through to a working multi-user system — from schema normalization to implementing triggers, authorization schemes, and aggregate reporting.

---

## 📄 License

This project was created for academic purposes as part of CSE302 coursework at East West University. All rights reserved by the project authors unless otherwise stated.