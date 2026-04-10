# Database Design

## Overview

The system uses **Firebase Firestore** as the primary database (NoSQL, document-based) and **Firebase Realtime Database** for live attendance streaming. This design supports real-time updates, offline capability, and horizontal scaling without schema migrations.

---

## Collections & Schema

### `organizations`
Stores top-level organization data. Supports multi-tenant deployment.

| Field | Type | Description |
|---|---|---|
| id | string | Auto-generated document ID |
| name | string | Organization name |
| logo_url | string | Logo image URL |
| subscription_plan | string | starter / professional / enterprise |
| employee_count | number | Total registered employees |
| created_at | timestamp | Account creation date |
| settings | map | Working hours, timezone, policies |

---

### `departments`
Organizational units within a company.

| Field | Type | Description |
|---|---|---|
| id | string | Auto-generated ID |
| org_id | string | Reference to organization |
| name | string | Department name |
| manager_id | string | Reference to employee (manager) |
| location_id | string | Primary office location |
| created_at | timestamp | — |

---

### `locations`
Physical office or branch locations.

| Field | Type | Description |
|---|---|---|
| id | string | Auto-generated ID |
| org_id | string | Reference to organization |
| name | string | Branch/office name |
| address | string | Full address |
| coordinates | geopoint | Latitude, longitude |
| radius_meters | number | Allowed GPS check-in radius |
| camera_ids | array | List of registered camera device IDs |

---

### `employees`
Core employee profiles.

| Field | Type | Description |
|---|---|---|
| id | string | Auto-generated ID |
| org_id | string | Reference to organization |
| employee_code | string | Unique HR code (e.g. EMP-0042) |
| full_name | string | Full legal name |
| email | string | Work email |
| phone | string | Contact number |
| department_id | string | Reference to department |
| location_id | string | Primary work location |
| role | string | admin / hr_manager / supervisor / employee |
| job_title | string | Designation |
| join_date | timestamp | Employment start date |
| face_embedding | array | 128-dim vector from TensorFlow model |
| face_image_url | string | Reference image stored in Firebase Storage |
| status | string | active / inactive / on_leave |
| leave_balance | map | annual: 15, sick: 10, casual: 5 |
| created_at | timestamp | — |

---

### `attendance_logs`
Every check-in and check-out event.

| Field | Type | Description |
|---|---|---|
| id | string | Auto-generated ID |
| employee_id | string | Reference to employee |
| org_id | string | Reference to organization |
| date | string | YYYY-MM-DD |
| check_in_time | timestamp | Exact check-in datetime |
| check_out_time | timestamp | Exact check-out datetime (null if still in) |
| duration_minutes | number | Total work duration |
| location_id | string | Office location of check-in |
| gps_coordinates | geopoint | Actual GPS at time of check-in |
| recognition_confidence | number | AI confidence score (0.0 – 1.0) |
| status | string | present / late / early_leave / absent / half_day |
| is_spoofing_detected | boolean | Anti-spoofing flag |
| device_id | string | Camera or device used |
| notes | string | HR override notes |

---

### `leaves`
Leave requests and approval workflow.

| Field | Type | Description |
|---|---|---|
| id | string | Auto-generated ID |
| employee_id | string | Reference to employee |
| org_id | string | Reference to organization |
| leave_type | string | annual / sick / casual / unpaid |
| start_date | timestamp | Leave start |
| end_date | timestamp | Leave end |
| total_days | number | Calculated working days |
| reason | string | Employee-provided reason |
| status | string | pending / approved / rejected / cancelled |
| applied_at | timestamp | Application datetime |
| reviewed_by | string | Reference to HR/manager who acted |
| reviewed_at | timestamp | Decision datetime |
| reviewer_notes | string | Optional rejection/approval note |

---

### `shifts`
Shift definitions and employee assignments.

| Field | Type | Description |
|---|---|---|
| id | string | Auto-generated ID |
| org_id | string | Reference to organization |
| name | string | e.g. "Morning Shift", "Night Shift" |
| start_time | string | HH:MM (24-hour) |
| end_time | string | HH:MM (24-hour) |
| grace_period_minutes | number | Late tolerance window |
| days | array | [Mon, Tue, Wed, Thu, Fri] |
| assigned_employees | array | List of employee IDs |
| location_id | string | Applicable location |

---

### `users`
Authentication and access control records.

| Field | Type | Description |
|---|---|---|
| id | string | Firebase Auth UID |
| employee_id | string | Reference to employee profile |
| org_id | string | Reference to organization |
| email | string | Login email |
| role | string | admin / hr_manager / supervisor / employee |
| last_login | timestamp | — |
| is_active | boolean | Account enabled/disabled |
| fcm_token | string | Device push notification token |

---

### `audit_logs`
Immutable log of all sensitive system actions.

| Field | Type | Description |
|---|---|---|
| id | string | Auto-generated ID |
| org_id | string | Reference to organization |
| performed_by | string | User ID who performed the action |
| action | string | e.g. EMPLOYEE_CREATED, LEAVE_APPROVED |
| target_id | string | ID of affected record |
| target_type | string | employee / leave / shift / attendance |
| details | map | Before/after values or action metadata |
| timestamp | timestamp | Exact action time |
| ip_address | string | Request origin IP |

---

## Firebase Realtime Database Structure

Used for live attendance feed only (low-latency streaming).

```
/live_attendance
  /{org_id}
    /{location_id}
      /{employee_id}
        status: "checked_in"
        check_in_time: 1718000000000
        name: "John Doe"
        department: "Engineering"
```

---

## Entity Relationship Summary

```
Organization
  ├── Departments (1:many)
  ├── Locations (1:many)
  └── Employees (1:many)
        ├── Attendance Logs (1:many)
        ├── Leaves (1:many)
        └── Shift Assignments (many:many via shifts.assigned_employees)

Users (1:1 with Employees)
Audit Logs (linked to any entity)
```

---

## Key Design Decisions

- **NoSQL over SQL:** Firestore's document model fits the hierarchical org → department → employee structure naturally and scales without joins
- **Face embeddings stored in employee document:** Enables fast in-memory comparison during recognition without a separate vector DB at this scale
- **Realtime DB for live feed only:** Firestore is used for persistent data; Realtime DB handles the low-latency live dashboard updates
- **Soft deletes:** Employees and records are marked inactive, never hard-deleted, to preserve audit history
- **Audit logs are append-only:** No updates or deletes allowed on audit_logs collection via Firestore security rules
