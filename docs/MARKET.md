# Market Analysis & Positioning

## Market Overview

| Metric | Value |
|---|---|
| Global HR Technology Market Size (2025) | $54.64 billion |
| Biometric Attendance Market Growth | ~12% CAGR |
| Key Driver | Digital HR transformation in SMEs and enterprises |
| Opportunity | Majority of SMEs still use manual or PIN-based attendance |

---

## Problem Being Solved

Most organizations — especially SMEs and mid-size companies — still rely on:
- Manual attendance registers (error-prone, easy to falsify)
- PIN or card-based systems (buddy punching, card sharing)
- Basic fingerprint scanners (hygiene concerns, hardware dependency)
- Spreadsheet-based leave tracking (no automation, high HR overhead)

These systems result in:
- Time theft costing organizations 4–5% of payroll annually
- HR teams spending 5–10 hours/week on attendance reconciliation
- Inaccurate payroll due to attendance errors
- No real-time visibility into workforce presence

---

## Target Audience

### Primary Markets

**SMEs (50–500 employees)**
- Need affordable, cloud-based solution without heavy IT infrastructure
- Benefit most from automation replacing manual HR processes
- Price-sensitive — per-employee pricing model fits their budget

**Corporate Offices (500+ employees)**
- Multi-branch operations need centralized attendance management
- Require detailed analytics and payroll-ready reports
- Need role-based access for large HR teams

### Secondary Markets

**Educational Institutions**
- Track staff and faculty attendance across departments
- Manage academic calendar-based leave policies
- Shift scheduling for administrative staff

**Healthcare Facilities**
- Critical shift-based workforce management
- Mask detection is essential in clinical environments
- Compliance requirements for accurate attendance records

---

## Unique Selling Points

### 1. 99.9% Recognition Accuracy
Most competitors achieve 95–97% accuracy. The combination of FaceNet embeddings, fine-tuned models, and preprocessing pipelines pushes this system to 99.9% — reducing false rejections that frustrate employees.

### 2. Works in Low Light
Standard facial recognition systems fail in dim environments. The CLAHE preprocessing pipeline maintains accuracy in environments as dim as 50 lux — covering warehouses, early morning shifts, and poorly lit offices.

### 3. Mask Detection
Post-pandemic workplaces and healthcare facilities require recognition with masks. This is a differentiator that most attendance systems do not offer.

### 4. Anti-Spoofing
Liveness detection prevents photo and video spoofing — a common attack vector in biometric systems. This is critical for organizations where attendance directly ties to payroll.

### 5. No Hardware Lock-In
Works with any standard IP camera or device camera via browser. No proprietary hardware required — significantly reducing deployment cost compared to fingerprint or iris scanner systems.

### 6. All-in-One Platform
Most competitors offer attendance OR leave management OR scheduling as separate products. This system integrates all three with a unified dashboard, eliminating the need for multiple HR tools.

### 7. Real-Time Visibility
Live attendance dashboard gives managers instant visibility — not end-of-day reports. This enables proactive management of absences and late arrivals.

---

## Competitive Comparison

| Feature | AI Attendance Checker | Typical Biometric System | Basic HR Software |
|---|---|---|---|
| Facial Recognition | ✅ | ✅ (lower accuracy) | ❌ |
| Mask Detection | ✅ | ❌ | ❌ |
| Low-Light Support | ✅ | ❌ | ❌ |
| Anti-Spoofing | ✅ | Partial | ❌ |
| Real-Time Dashboard | ✅ | ❌ | Partial |
| Leave Management | ✅ | ❌ | ✅ |
| Shift Scheduling | ✅ | ❌ | Partial |
| GPS Verification | ✅ | ❌ | ❌ |
| No Hardware Required | ✅ | ❌ | ✅ |
| Cloud-Based | ✅ | Partial | ✅ |
| Per-Employee Pricing | ✅ | ❌ (hardware cost) | ✅ |

---

## Pricing Strategy

| Plan | Price | Target |
|---|---|---|
| Starter | $5/employee/month | SMEs, startups |
| Professional | $10/employee/month | Mid-size companies |
| Enterprise | $15/employee/month | Large organizations, multi-branch |
| Setup Fee | One-time | Hardware setup, onboarding, training |

**Revenue Example:**
- 100-employee company on Professional plan = $1,000/month recurring
- 500-employee enterprise = $7,500/month recurring

---

## Impact Achieved

- 99.9% facial recognition accuracy in production
- ~80% reduction in manual attendance processing time
- Eliminated buddy punching for all deployed organizations
- Successfully handling 500+ employee organizations
- Zero downtime since production deployment (Firebase SLA)
- Positive feedback from HR teams on leave workflow automation
