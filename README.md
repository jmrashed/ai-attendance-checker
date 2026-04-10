# AI Attendance Checker
### AI-Powered Human Resource Management with Facial Recognition

> **Category:** HR Technology · Human Resources
> **Industry:** Human Resources
> **Status:** Completed
> **Development Period:** 5 months (2024)

---

## Overview

AI Attendance Checker is a full-stack enterprise HR management system that automates employee attendance tracking using real-time facial recognition. The system eliminates manual check-in processes, reduces buddy punching, and provides organizations with accurate, real-time workforce data — all accessible through a web and mobile-friendly dashboard.

The platform targets **SMEs, corporate offices, educational institutions, and healthcare facilities** that need a reliable, scalable, and intelligent attendance solution without heavy infrastructure investment.

---

## Why This Was Built

Traditional attendance systems — punch cards, PIN-based check-ins, manual registers — are prone to fraud, human error, and administrative overhead. Large organizations with hundreds of employees waste significant HR hours on attendance reconciliation and leave management.

This system was built to:
- Eliminate time theft and buddy punching through biometric verification
- Automate attendance workflows and reduce HR manual workload
- Provide real-time visibility into workforce presence across multiple locations
- Integrate leave, shift, and reporting into a single unified platform
- Serve organizations in markets where HR digitization is rapidly growing ($54.64B market, 2025)

---

## Key Features

| Feature | Description |
|---|---|
| AI Facial Recognition | Identifies employees in real-time using deep learning models |
| Anti-Spoofing | Detects photo/video spoofing attempts using liveness detection |
| Mask Detection | Recognizes employees even when wearing face masks |
| Low-Light Support | Works accurately in poor lighting conditions |
| Real-Time Tracking | Live attendance dashboard with instant check-in/out updates |
| Leave Management | Apply, approve, and track leaves with automated balance calculation |
| Shift Scheduling | Assign and manage employee shifts with conflict detection |
| GPS Location Tracking | Verifies employee location at time of check-in |
| Employee Database | Centralized employee profiles, documents, and history |
| Reports & Analytics | Automated attendance reports, trends, and exportable data |
| Role-Based Access | Admin, HR Manager, Supervisor, and Employee access levels |
| Multi-Branch Support | Manage attendance across multiple office locations |

---

## Target Audience

- **SMEs** — Small and medium businesses needing affordable, scalable HR automation
- **Corporate Offices** — Large enterprises requiring multi-branch attendance management
- **Educational Institutions** — Schools and universities tracking staff and faculty attendance
- **Healthcare Facilities** — Hospitals and clinics managing shift-based workforce

---

## Pricing Model

| Plan | Price | Includes |
|---|---|---|
| Starter | $5/employee/month | Core attendance + basic reports |
| Professional | $10/employee/month | Full features + GPS + leave management |
| Enterprise | $15/employee/month | Custom integrations + dedicated support + SLA |
| Setup Fee | One-time | Hardware setup, onboarding, training |

---

## System Architecture

See [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) for the full architecture breakdown.

**High-Level Overview:**

```
[Camera / Mobile Device]
        ↓
[Face Capture Module]
        ↓
[AI Recognition Engine] ← TensorFlow + OpenCV
        ↓
[Anti-Spoofing & Liveness Check]
        ↓
[REST API Backend] ← Node.js + Express
        ↓
[Firebase Realtime Database + Firestore]
        ↓
[React Dashboard] ← HR Admin / Manager / Employee
```

---

## Database Design

See [`docs/DATABASE.md`](docs/DATABASE.md) for full schema and entity relationships.

Core collections: `employees`, `attendance_logs`, `leaves`, `shifts`, `departments`, `locations`, `users`, `audit_logs`

---

## Team & Roles

See [`docs/TEAM.md`](docs/TEAM.md) for detailed role breakdown.

| Role | Count |
|---|---|
| Full-Stack Developers | 3 |
| AI / ML Specialist | 1 |
| Backend / DevOps | 1 |
| Total | 5 |

---

## Development Timeline

See [`docs/TIMELINE.md`](docs/TIMELINE.md) for full sprint breakdown.

| Phase | Duration |
|---|---|
| Planning & Architecture | 2 weeks |
| AI Model Training & Integration | 5 weeks |
| Backend API Development | 4 weeks |
| Frontend Dashboard | 4 weeks |
| Testing & QA | 3 weeks |
| Deployment & Handover | 2 weeks |
| **Total** | **~5 months** |

---

## Impact & Results

- **99.9% facial recognition accuracy** achieved in production
- Reduced manual attendance processing time by **~80%**
- Automated leave and shift workflows eliminated daily HR reconciliation tasks
- Successfully deployed for organizations with **500+ employees**
- Works in **low-light environments** and with **masked faces**

---

## Documentation Index

| Document | Description |
|---|---|
| [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) | Full system architecture, tech stack, component breakdown |
| [`docs/DATABASE.md`](docs/DATABASE.md) | Database schema, collections, relationships |
| [`docs/FEATURES.md`](docs/FEATURES.md) | Detailed feature specifications |
| [`docs/TEAM.md`](docs/TEAM.md) | Team structure, roles, and responsibilities |
| [`docs/TIMELINE.md`](docs/TIMELINE.md) | Development phases and sprint breakdown |
| [`docs/MARKET.md`](docs/MARKET.md) | Market analysis, USPs, competitive positioning |

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React.js, Tailwind CSS |
| Backend | Node.js, Express.js |
| AI / ML | TensorFlow, OpenCV, face-api.js |
| Database | Firebase Firestore, Firebase Realtime DB |
| Authentication | Firebase Auth, JWT |
| Storage | Firebase Storage |
| Hosting | Firebase Hosting, Cloud Functions |
| GPS | Google Maps API |
| Notifications | Firebase Cloud Messaging (FCM) |

---

## License

This project is proprietary. All rights reserved.
