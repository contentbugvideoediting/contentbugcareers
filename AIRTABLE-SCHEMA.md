# Airtable Careers Base — Schema & Setup

## Base Setup

Create a new Airtable Base named: **Content Bug Careers**

---

## Table: Applications

Create one table with the following fields:

| Field Name | Field Type | Notes |
|---|---|---|
| Role | Single line text | "Professional Editor", "Project Manager", or "Sales Closer" |
| First Name | Single line text | |
| Last Name | Single line text | |
| Email | Email | |
| Phone | Phone number | |
| Location (Philippines) | Single line text | City / Province |
| Years of Experience | Single line text | Dropdown value |
| Previous Employers | Long text | |
| LinkedIn | URL | Optional |
| Earliest Start Date | Date | |
| Can Work PST | Single line text | "Yes" or "No" |
| Local Hours (PH) | Single line text | If Yes |
| CPU | Single line text | |
| RAM | Single line text | |
| GPU | Single line text | |
| Storage Type | Single line text | SSD / HDD / Both |
| Operating System | Single line text | |
| Software Experience | Long text | Comma-separated list |
| Critical Thinking Q1 | Long text | |
| Critical Thinking Q2 | Long text | |
| Critical Thinking Q3 | Long text | |
| Video Introduction URL | URL | From VideoTiny |
| Reference Name | Single line text | |
| Reference Role/Company | Single line text | |
| Reference Email | Email | |
| Reference Phone | Phone number | |
| Reference Relationship | Single line text | |
| Best Edit URL | URL | Editor only |
| Edit Verification URL | URL | Editor only |
| Editing Workflow | Long text | Editor only |
| PM Question 1 | Long text | PM only |
| PM Question 2 | Long text | PM only |
| Sales Question 1 | Long text | Sales only |
| Sales Question 2 | Long text | Sales only |
| Uploaded Files | Long text | JSON list of uploaded filenames (fallback) |
| Submitted At | Date (with time) | ISO timestamp |

---

## Views

Create 3 filtered views:

### 1. Editor Applicants
- Filter: Role = "Professional Editor"

### 2. Project Manager Applicants
- Filter: Role = "Project Manager"

### 3. Sales Applicants
- Filter: Role = "Sales Closer"

---

## After Creating the Base

1. Copy the Base ID from the Airtable URL: `airtable.com/BASE_ID/...`
2. Open `careers.html` and update line ~6 of the `<script>`:

```js
AIRTABLE_BASE_ID: 'appXXXXXXXXXXXXXX',   // ← paste your base ID here
```

---

## Portal Backend Route (Recommended)

For proper file uploads, add these two routes to `server.js`:

```js
// POST /api/careers/upload — handles file uploads to Google Drive
// POST /api/careers/apply  — creates Airtable record with file URLs
```

The careers.html will try the portal endpoint first, then fall back to direct
Airtable API (text fields only, no files) if the backend is unavailable.

---

## VideoTiny Setup

1. Create a project at videotiny.com
2. Copy your Project ID
3. Update `careers.html`:

```js
VIDEOTINY_ID: 'your_project_id_here',
```
