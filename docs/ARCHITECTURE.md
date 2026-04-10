# System Architecture

## Overview

AI Attendance Checker is built on a **3-tier architecture**: a React-based frontend, a Node.js REST API backend, and Firebase as the cloud data and infrastructure layer. The AI engine runs as a separate processing module integrated into the backend pipeline.

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                        CLIENT LAYER                         │
│                                                             │
│   ┌──────────────┐        ┌──────────────────────────┐     │
│   │  Web Browser │        │  Mobile Browser / PWA    │     │
│   │  React App   │        │  React (Responsive)      │     │
│   └──────┬───────┘        └────────────┬─────────────┘     │
└──────────┼──────────────────────────────┼───────────────────┘
           │  HTTPS / REST API            │
┌──────────▼──────────────────────────────▼───────────────────┐
│                       API LAYER                             │
│                                                             │
│   ┌─────────────────────────────────────────────────────┐   │
│   │              Node.js + Express REST API             │   │
│   │                                                     │   │
│   │  /auth      /employees    /attendance               │   │
│   │  /leaves    /shifts       /reports                  │   │
│   │  /locations /departments  /notifications            │   │
│   └──────────────────────┬──────────────────────────────┘   │
│                          │                                  │
│   ┌──────────────────────▼──────────────────────────────┐   │
│   │              AI Recognition Engine                  │   │
│   │                                                     │   │
│   │   OpenCV (Face Detection) → TensorFlow (Recognition)│   │
│   │   Liveness Detection → Anti-Spoofing Module         │   │
│   │   Mask Detection → Low-Light Enhancement            │   │
│   └──────────────────────┬──────────────────────────────┘   │
└─────────────────────────┼───────────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────────┐
│                      DATA LAYER                             │
│                                                             │
│   ┌──────────────┐  ┌──────────────┐  ┌─────────────────┐  │
│   │  Firestore   │  │  Realtime DB │  │ Firebase Storage │  │
│   │  (Main Data) │  │  (Live Feed) │  │ (Face Images)    │  │
│   └──────────────┘  └──────────────┘  └─────────────────┘  │
│                                                             │
│   ┌──────────────┐  ┌──────────────┐                        │
│   │ Firebase Auth│  │  FCM Push    │                        │
│   │ (Identity)   │  │ (Alerts)     │                        │
│   └──────────────┘  └──────────────┘                        │
└─────────────────────────────────────────────────────────────┘
```

---

## Component Breakdown

### 1. Face Capture Module
- Accesses device camera via browser WebRTC API or IP camera feed
- Captures frames at configurable intervals
- Sends frames to the AI engine for processing
- Handles camera permission management and fallback states

### 2. AI Recognition Engine
- **Face Detection:** OpenCV detects and crops face regions from captured frames
- **Feature Extraction:** TensorFlow model converts face to a 128-dimensional embedding vector
- **Identity Matching:** Compares embedding against stored employee face vectors using cosine similarity
- **Liveness Detection:** Analyzes eye blink patterns and micro-movements to reject static photos
- **Anti-Spoofing:** Detects screen/print attacks using texture analysis
- **Mask Detection:** Separate model trained to recognize masked faces
- **Low-Light Enhancement:** Pre-processing pipeline normalizes brightness before recognition

### 3. REST API Backend (Node.js + Express)
- Stateless API with JWT-based authentication
- Role-based middleware (Admin, HR Manager, Supervisor, Employee)
- Handles all business logic: attendance rules, leave policies, shift conflicts
- Integrates with Google Maps API for GPS verification
- Sends real-time updates to Firebase Realtime Database
- Triggers FCM push notifications for alerts and approvals

### 4. React Frontend Dashboard
- Role-specific dashboards (Admin sees everything, Employee sees own data)
- Real-time attendance feed using Firebase Realtime DB listeners
- Leave application and approval workflow UI
- Shift scheduling calendar interface
- Report generation with chart visualizations and CSV/PDF export
- Fully responsive — works on desktop and mobile browsers

### 5. Firebase Infrastructure
- **Firestore:** Primary database for structured data (employees, leaves, shifts, reports)
- **Realtime Database:** Live attendance feed and online status tracking
- **Firebase Storage:** Stores employee face images and documents
- **Firebase Auth:** Manages user identity, sessions, and password resets
- **Cloud Functions:** Serverless triggers for automated tasks (daily reports, leave balance resets)
- **FCM:** Push notifications for check-in confirmations, leave approvals, shift reminders

---

## Security Architecture

- All API endpoints protected with JWT tokens (15-minute expiry + refresh tokens)
- Face images stored encrypted in Firebase Storage with private access rules
- Role-based access control (RBAC) enforced at both API and Firestore rules level
- Anti-spoofing prevents biometric fraud
- GPS verification prevents remote check-in fraud
- All data transmitted over HTTPS/TLS
- Audit logs maintained for all sensitive actions (check-ins, approvals, data changes)

---

## Scalability Design

- Stateless API allows horizontal scaling behind a load balancer
- Firebase auto-scales with usage — no manual server provisioning
- Face embeddings stored as vectors, enabling fast similarity search even at scale
- Multi-branch support via location-scoped data partitioning
- Cloud Functions handle background jobs without blocking the main API

---

## Tech Stack Summary

| Layer | Technology | Purpose |
|---|---|---|
| Frontend | React.js | User interface |
| Styling | Tailwind CSS | Responsive design |
| Backend | Node.js + Express | REST API server |
| AI - Detection | OpenCV | Face detection and preprocessing |
| AI - Recognition | TensorFlow | Face embedding and identity matching |
| Database | Firebase Firestore | Structured data storage |
| Realtime | Firebase Realtime DB | Live attendance feed |
| Storage | Firebase Storage | Face images, documents |
| Auth | Firebase Auth + JWT | Identity and session management |
| Notifications | Firebase FCM | Push alerts |
| Location | Google Maps API | GPS check-in verification |
| Serverless | Firebase Cloud Functions | Automated background tasks |
