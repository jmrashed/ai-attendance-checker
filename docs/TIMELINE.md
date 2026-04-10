# Development Timeline

## Total Duration: ~5 Months

---

## Phase Breakdown

| Phase | Duration | Weeks |
|---|---|---|
| Phase 1: Planning & Architecture | 2 weeks | Week 1–2 |
| Phase 2: AI Model Development | 5 weeks | Week 3–7 |
| Phase 3: Backend API Development | 4 weeks | Week 5–8 |
| Phase 4: Frontend Development | 4 weeks | Week 7–10 |
| Phase 5: Integration & Testing | 3 weeks | Week 11–13 |
| Phase 6: Deployment & Handover | 2 weeks | Week 19–20 |

> Note: Phases 3 and 4 ran in parallel with Phase 2 after the AI pipeline interface was defined.

---

## Phase 1 — Planning & Architecture (Weeks 1–2)

**Goals:**
- Define project scope, features, and priorities
- Finalize tech stack decisions
- Design system architecture
- Design database schema
- Set up development environments and Firebase project
- Break down work into sprints and assign responsibilities

**Deliverables:**
- Architecture diagram
- Database schema document
- Feature specification list
- Sprint plan for all phases
- Firebase project initialized with dev/staging/prod environments

---

## Phase 2 — AI Model Development (Weeks 3–7)

**Goals:**
- Set up OpenCV face detection pipeline
- Fine-tune TensorFlow FaceNet model for face recognition
- Build and train anti-spoofing liveness detection module
- Build mask detection model
- Implement low-light preprocessing pipeline
- Define and expose the AI engine API interface for backend integration

**Deliverables:**
- Working face detection and recognition pipeline
- Anti-spoofing module with test results
- Mask detection model
- Accuracy benchmarks (target: ≥ 99%)
- AI engine HTTP interface for backend consumption

---

## Phase 3 — Backend API Development (Weeks 5–8)

**Goals:**
- Build all REST API endpoints
- Implement Firebase Auth + JWT middleware
- Implement RBAC middleware
- Integrate AI engine into attendance check-in flow
- Build leave management business logic
- Build shift scheduling logic with conflict detection
- Implement GPS verification logic
- Set up Firebase Cloud Functions for background tasks
- Implement audit logging

**Deliverables:**
- Fully functional REST API (all endpoints)
- Firebase Cloud Functions (daily absent marking, leave balance reset, report generation)
- API documentation (endpoint list, request/response formats)

---

## Phase 4 — Frontend Development (Weeks 7–10)

**Goals:**
- Build React application with role-based routing
- Build Admin and HR Manager dashboard
- Build real-time attendance live feed
- Build employee management module (CRUD, face enrollment)
- Build leave application and approval workflow UI
- Build shift scheduling calendar
- Build reports and analytics module
- Build employee self-service dashboard
- Integrate FCM push notifications

**Deliverables:**
- Fully functional React application
- All role-based dashboards
- Responsive design (desktop + mobile browser)

---

## Phase 5 — Integration & Testing (Weeks 11–13)

**Goals:**
- End-to-end integration testing of all modules
- AI recognition accuracy testing under various conditions (low light, masks, spoofing attempts)
- Performance testing (response times, concurrent users)
- Security testing (auth bypass attempts, RBAC enforcement)
- Bug fixing and edge case handling
- User acceptance testing (UAT) with a pilot group

**Deliverables:**
- Test results report
- Bug fix log
- UAT sign-off
- Performance benchmarks

---

## Phase 6 — Deployment & Handover (Weeks 19–20)

**Goals:**
- Deploy to Firebase Hosting (production)
- Deploy Cloud Functions to production
- Configure production Firebase security rules
- Set up monitoring and error alerting
- Onboard initial client organizations
- Conduct admin and HR manager training sessions
- Deliver documentation package

**Deliverables:**
- Live production system
- Deployment documentation
- Admin training materials
- Handover documentation

---

## Key Milestones

| Milestone | Target Week | Status |
|---|---|---|
| Architecture finalized | Week 2 | ✅ Completed |
| AI pipeline working (basic recognition) | Week 5 | ✅ Completed |
| Anti-spoofing + mask detection ready | Week 7 | ✅ Completed |
| Backend API complete | Week 8 | ✅ Completed |
| Frontend MVP ready | Week 10 | ✅ Completed |
| Integration testing complete | Week 13 | ✅ Completed |
| Production deployment | Week 20 | ✅ Completed |

---

## Challenges & How They Were Resolved

| Challenge | Resolution |
|---|---|
| AI model accuracy dropped with masks | Trained a separate masked-face model and built a detection switch |
| Low-light recognition failures | Added CLAHE preprocessing before embedding generation |
| Real-time dashboard latency | Moved live feed to Firebase Realtime DB instead of polling Firestore |
| GPS spoofing attempts | Added server-side GPS validation and flagging logic |
| Firebase cold start delays on Cloud Functions | Implemented minimum instance configuration for critical functions |
