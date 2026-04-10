# Team Structure & Roles

## Team Overview

| # | Role | Count |
|---|---|---|
| 1 | Full-Stack Developer (Lead) | 1 |
| 2 | Full-Stack Developer | 2 |
| 3 | AI / ML Specialist | 1 |
| 4 | Backend Developer / DevOps | 1 |
| **Total** | | **5** |

---

## Role Breakdown

### Full-Stack Developer — Lead (My Role)

**Responsibilities:**
- Led overall technical architecture design and decision-making
- Designed the complete system architecture (3-tier: frontend, API, Firebase)
- Designed the Firestore database schema and data relationships
- Built the core React dashboard — attendance feed, leave management UI, shift scheduling calendar, and reports module
- Developed the Node.js REST API — all core endpoints (employees, attendance, leaves, shifts, reports)
- Integrated the AI recognition engine output into the attendance logging pipeline
- Implemented role-based access control (RBAC) across frontend and backend
- Integrated Firebase Auth, Firestore, Realtime DB, Storage, and FCM
- Integrated Google Maps API for GPS location verification
- Coordinated with the AI specialist on the recognition pipeline interface
- Conducted code reviews for the team
- Led sprint planning and task breakdown
- Managed deployment to Firebase Hosting and Cloud Functions

**Key Contributions:**
- Designed the face embedding storage and matching strategy within Firestore
- Built the real-time attendance dashboard using Firebase Realtime DB listeners
- Designed the leave approval workflow and automated balance deduction logic
- Built the report generation module with CSV and PDF export

---

### Full-Stack Developer × 2

**Responsibilities:**
- Built employee management module (CRUD, face enrollment UI, bulk import)
- Developed the employee-facing dashboard (own attendance, leave application, profile)
- Built notification system integration (FCM push notifications)
- Implemented the shift scheduling UI and conflict detection logic
- Developed the admin settings panel (organization config, location management)
- Wrote API integration layer on the frontend (Axios, error handling, loading states)
- Assisted with testing and bug fixing across modules

---

### AI / ML Specialist

**Responsibilities:**
- Selected and fine-tuned the TensorFlow face recognition model (FaceNet architecture)
- Integrated OpenCV for face detection and preprocessing pipeline
- Developed and trained the anti-spoofing liveness detection module
- Developed the mask detection model using augmented masked face datasets
- Built the low-light preprocessing pipeline (CLAHE normalization)
- Optimized model inference speed for real-time performance
- Defined the face embedding generation and cosine similarity matching logic
- Documented model accuracy benchmarks and threshold tuning

---

### Backend Developer / DevOps

**Responsibilities:**
- Set up Firebase project, security rules, and environment configurations
- Configured Firebase Cloud Functions for automated background tasks (daily reports, leave balance resets, absent marking)
- Set up CI/CD pipeline for automated deployment
- Managed Firebase Storage structure and access rules
- Implemented audit logging middleware on the API
- Handled environment management (development, staging, production)
- Monitored system performance and Firebase usage quotas
- Set up error logging and alerting

---

## Why I Was the Right Person to Lead This

- I had prior experience with both React and Node.js, making me the natural choice to own the full-stack architecture
- My understanding of Firebase's real-time capabilities allowed me to design the live attendance feed efficiently
- I bridged the gap between the AI specialist's output (face embeddings) and the product's business logic (attendance rules, leave policies)
- I made the key architectural decision to use Firebase as the infrastructure backbone, which eliminated the need for a dedicated server and reduced operational costs significantly
- I drove the project from a rough concept to a deployed, production-ready system within 5 months
