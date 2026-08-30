# 🎉 Festive Flow — Event Management System

A full-stack Event Management System built with **Oracle APEX** and **SQL** for the course **CSE302: Database Systems (Section 06), Fall 2024**, East West University.

> ⚠️ **Security note:** Login credentials, workspace passwords, and other sensitive details have been redacted from the source report and are **not included** in this README. 
---

## 📌 Project Info

| | |
|---|---|
| **Course** | CSE302: Database Systems (Section 06) |
| **Semester** | Fall 2024 |
| **Group** | 9 (Pandas) |
| **Project Name** | Festive Flow |
| **Platform** | Oracle APEX |

---

## 📖 Overview

**Festive Flow** is a database-driven event management platform that lets organizers create and manage events, sell tickets (Regular & VIP), register attendees, collect payments, gather feedback, and coordinate staff (employees, volunteers, admins) and sponsors — all through a role-based Oracle APEX web application backed by a relational SQL database.

### ✨ Key Features

- **Role-based access control** — Admins can view and manage all data (including the Admin table); regular users (Organizers, Attendees, Volunteers, Sponsors) are blocked from admin-only pages via APEX page-level authorization — attempting access returns an **Access Denied** page.
- **Automated trigger** — A database trigger calculates `DaysUntilEvent` dynamically at insert time by comparing the event date to the current date. If the event has already happened, the value goes negative, indicating how many days have passed.
- **20 CRUD interfaces** — Full Report + Form pages for every core table (Users, Event, Organizer, OrganizerPhone, OrganizerAddress, Attendee, Ticket, RegularTicket, VIPTicket, Registration, Activity, Feedback, Payment, Venue, Hosted, Equipment, Employee, Volunteer, Admin, Sponsor).
- **6 analytical reports** — Multi-table and aggregate SQL queries summarizing event activities, sponsors, ticket sales, payments, and VIP attendee details.

---

## 🗂️ Database Design

### 1. Entity-Relationship (E-R) Model
The system models core entities including `Event`, `Organizer` (with `OrganizerPhone`/`OrganizerAddress`), `Venue`, `Attendee`, `Ticket` (with `VIPTicket`/`RegularTicket` subtypes via ISA), `Registration`, `Payment`, `Activity`, `Feedback`, `Sponsor`, `Equipment`, and `Employee` (with `Volunteer`/`Admin` subtypes via ISA), connected through relationships such as `Organizes`, `Hosted`, `Registered`, `Participates`, `Paid`, `Needs`, `Sponsored by`, and `Rating`.

### 2. Relational Schema
The E-R model was mapped into normalized relational tables — `Event`, `Organizer`, `OrganizerPhone`, `OrganizerAddress`, `Venue`, `Attendee`, `Ticket`, `VIPTicket`, `RegularTicket`, `Registration`, `Activity`, `Feedback`, `Payment`, `Employee`, `Volunteer`, `Admin`, `Sponsor`, `Equipment`, and `Users` — with primary/foreign key constraints enforcing referential integrity across the system.

### 3. Notable Trigger
```sql
-- Conceptual logic (see the APEX app for the actual PL/SQL trigger)
-- On INSERT INTO Event:
-- DaysUntilEvent := EventDate - SYSDATE;
-- (a negative value means the event has already passed)
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
- **Non-admin roles** (Organizer, Attendee, Volunteer, Sponsor) are denied access to admin-only pages — attempting to access them returns an **Access Denied** page via APEX's built-in page security check.

> All usernames, passwords, and workspace secrets from the original coursework submission have been **redacted and are not reproduced here** 

---

## 🛠️ Tech Stack

- **Database & Backend:** Oracle Database, PL/SQL (triggers, constraints)
- **Application Layer:** Oracle APEX (low-code report/form generation, page-level authorization schemes)
- **Query Types:** Multi-table joins, aggregate functions (`COUNT`, `SUM`), foreign-key relationships across 15+ tables

---

## 🔒 Note

All credentials, workspace secrets, and session URLs from the original submission have been redacted from this repo.

---

## 📝 Concluding Remarks

Completing this Event Management System project in SQL on Oracle APEX was a valuable exercise in database design, query writing, and building a role-secured application — from a conceptual E-R model through to a working multi-user system with triggers, authorization schemes, and aggregate reporting.

---

## 📄 License

This project was created for academic purposes as part of CSE302 coursework at East West University. All rights reserved by the project authors unless otherwise stated.