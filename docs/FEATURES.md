# Feature Specifications

## 1. AI Facial Recognition Attendance

**What it does:**
Employees check in and out by simply looking at a camera. The system identifies them in real-time without any physical contact or manual input.

**How it works:**
1. Camera captures a live frame
2. OpenCV detects and isolates the face region
3. TensorFlow model generates a 128-dimensional face embedding
4. Embedding is compared against all registered employee embeddings using cosine similarity
5. If confidence score exceeds threshold (≥ 0.92), the employee is identified and attendance is logged
6. If no match or low confidence, the system prompts for retry or flags for manual review

**Accuracy:** 99.9% under standard conditions

---

## 2. Anti-Spoofing & Liveness Detection

**What it does:**
Prevents employees from clocking in using a photo, video, or 3D mask of another person.

**How it works:**
- Analyzes eye blink frequency and natural micro-movements
- Texture analysis detects printed photos vs. real skin
- Screen reflection detection identifies digital displays
- If spoofing is detected: check-in is blocked, event is flagged, and HR is notified

---

## 3. Mask Detection

**What it does:**
Recognizes employees even when wearing face masks — critical for healthcare and post-pandemic workplaces.

**How it works:**
- Separate TensorFlow model trained on masked face datasets
- Identifies upper facial features (eyes, forehead, nose bridge) when lower face is covered
- Seamlessly switches between masked and unmasked recognition pipelines

---

## 4. Low-Light Support

**What it does:**
Maintains recognition accuracy in poorly lit environments (warehouses, early morning shifts, night shifts).

**How it works:**
- Pre-processing pipeline applies adaptive histogram equalization (CLAHE) to normalize brightness
- Model trained on augmented low-light datasets
- Works in environments as dim as 50 lux

---

## 5. Real-Time Attendance Dashboard

**What it does:**
HR managers and supervisors see a live view of who is present, absent, or late — updated instantly as employees check in.

**Features:**
- Live employee status cards (present / absent / late / on leave)
- Filter by department, location, or shift
- Color-coded status indicators
- Instant notifications when an employee is flagged (spoofing, unrecognized face)
- Historical view by date

---

## 6. GPS Location Verification

**What it does:**
Confirms the employee is physically at the designated office location when checking in, preventing remote or fraudulent check-ins.

**How it works:**
- Device GPS coordinates captured at check-in time
- Compared against the registered office location coordinates
- If outside the allowed radius (configurable per location), check-in is flagged or blocked
- GPS data stored with every attendance log for audit purposes

---

## 7. Leave & Absence Management

**What it does:**
Complete digital leave workflow — from employee application to manager approval — with automatic balance tracking.

**Features:**
- Employees apply for leave (annual, sick, casual, unpaid) via dashboard
- Manager/HR receives notification and approves or rejects with notes
- Leave balance automatically deducted upon approval
- Calendar view of team leaves to avoid scheduling conflicts
- Automatic absence marking if employee doesn't check in and has no approved leave
- Leave history and balance visible to employee at all times

---

## 8. Shift Scheduling

**What it does:**
HR creates and manages work shifts, assigns employees, and detects scheduling conflicts automatically.

**Features:**
- Create named shifts with start/end times and grace periods
- Assign individual employees or entire departments to shifts
- Conflict detection prevents double-assignment
- Shift calendar view per employee and per department
- Shift change requests by employees, approved by supervisors
- Attendance late/early-leave status calculated relative to assigned shift

---

## 9. Employee Database

**What it does:**
Centralized repository of all employee information, accessible based on role permissions.

**Features:**
- Full employee profiles (personal info, job details, department, location)
- Face enrollment — capture and register employee face during onboarding
- Document storage (contracts, IDs) via Firebase Storage
- Employment history and status tracking
- Bulk import via CSV for large organizations
- Search, filter, and export employee lists

---

## 10. Reports & Analytics

**What it does:**
Generates detailed attendance reports for payroll, compliance, and management decision-making.

**Report Types:**
- Daily attendance summary (present / absent / late counts)
- Individual employee attendance history
- Department-level attendance trends
- Late arrival and early departure reports
- Leave utilization reports
- Monthly payroll-ready attendance export (CSV / PDF)
- Custom date range reports

**Analytics:**
- Attendance rate trends over time (charts)
- Department comparison dashboards
- Peak absence period identification
- Overtime tracking

---

## 11. Role-Based Access Control

| Role | Permissions |
|---|---|
| Admin | Full system access, organization settings, billing |
| HR Manager | Employee management, leave approvals, all reports |
| Supervisor | View team attendance, approve team leaves, shift management |
| Employee | Own attendance history, leave applications, own profile |

---

## 12. Notifications & Alerts

- Check-in/check-out confirmation (push notification to employee)
- Late arrival alert (to supervisor)
- Absent employee alert (to HR)
- Leave approval/rejection notification (to employee)
- Spoofing attempt alert (to HR and admin)
- Shift reminder (to employee, 30 minutes before shift)
- Low leave balance warning (to employee)
