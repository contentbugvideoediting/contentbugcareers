# Content Bug Careers — Airtable Schema

## Base
- **Base ID:** `appUvZqaCBZ42r9Nl`
- **Base URL:** https://airtable.com/appUvZqaCBZ42r9Nl

## Table: Applications
- **Table ID:** `tblTu0xMDJmfWymey`

---

## Fields (Real IDs — Production)

| Field Name | Field ID | Type | Notes |
|---|---|---|---|
| Name | `fldGuCCrHJNhu3ZPK` | singleLineText | Primary field. Auto-set to "First Last — Role" |
| Role | `fld0Nxp0mO9yzduTV` | singleSelect | Professional Editor / Project Manager / Sales Closer |
| Application Status | `fldkN92KyIHvC5Ikt` | singleSelect | New → Reviewing → Interview → Hired → Rejected |
| Submitted At | `fldsqWvdErh0AWDCV` | dateTime | ISO timestamp, PST timezone |
| First Name | `fldER8Ol5pshvoOBw` | singleLineText | |
| Last Name | `fldSlj7j5H0KvEuUR` | singleLineText | |
| Email | `fldAxQ3EoEABvuxMt` | email | |
| Phone | `fld2EFJAuXLGBpgjl` | phoneNumber | |
| Location (Philippines) | `fld1DYW8HbFelINn1` | singleLineText | City / Province |
| Years of Experience | `fldO8RB0E1jYIbQf9` | singleSelect | Less than 1 year / 1–2 years / 3–5 years / 5–8 years / 8+ years |
| Earliest Start Date | `fldtcGm9Nl7r75NAo` | date | ISO format |
| Previous Employers | `fldw0aETx02nZq6cS` | multilineText | |
| LinkedIn | `fldUZonh7i52QO7AK` | url | Optional |
| Can Work PST Hours | `fldWddUr2bWpivd0X` | singleSelect | Yes / No |
| Local Hours (Philippines) | `fldoGG8nONCXzX5Jt` | singleLineText | e.g. "1:00 AM – 10:00 AM PHT" |
| CPU | `fld81LEMiSwLxy8dX` | singleLineText | |
| RAM | `fld9NSZi8UrkWp6fW` | singleSelect | 8 GB / 16 GB / 32 GB / 64 GB / 128 GB+ |
| GPU | `fldMY1iOmerRJQgsu` | singleLineText | |
| Storage Type | `fld21FyuwGSA4XEMZ` | singleSelect | SSD / HDD / SSD + HDD |
| Operating System | `fldlUw7Qks9AThqnv` | singleSelect | Windows 10/11, macOS 12–15, Linux |
| Speed Test Screenshot | `flddKATewzJzkBJuc` | multipleAttachments | Uploaded via portal backend |
| Software Experience | `fldCdXv27ZIH7vq14` | multilineText | Comma-separated list |
| Critical Thinking Q1 | `fldbBT0tAI826nDeA` | multilineText | Competing deadlines scenario |
| Critical Thinking Q2 | `fld96SxmrZlyjC8Xh` | multilineText | Undetected mistake scenario |
| Critical Thinking Q3 | `fldiAHNU1MTk6ILPI` | multilineText | Learning quickly scenario |
| Video Introduction URL | `fldMC2C0UGCneJJta` | url | From VideoTiny |
| Reference Name | `fldAikSAqmolySzYC` | singleLineText | |
| Reference Role/Company | `fldx0RDKuADk0hqFT` | singleLineText | |
| Reference Email | `fldVYtKQS3sxku0Jz` | email | |
| Reference Phone | `fld8UkzEkW0qKqqxC` | phoneNumber | |
| Reference Relationship | `flduXMjn7nRh2wHxV` | singleSelect | Former Manager / Supervisor / Colleague / Client / Mentor / Professor |
| Best Edit (URL/Link) | `fld3KXXVRGClkmlVf` | url | Editor only |
| Best Edit Upload | `fldmEyPu6mVtU3sQM` | multipleAttachments | Editor only — uploaded via portal backend |
| Edit Verification (URL/Link) | `fldTjKPDjmEAh8g47` | url | Editor only |
| Edit Verification Upload | `fldJCO3lQ1WdmVpq5` | multipleAttachments | Editor only — uploaded via portal backend |
| Editing Workflow | `fldDQXaDqxxHTJ94m` | multilineText | Editor only |
| PM Question 1 | `fldoOvNJj11TEOVDJ` | multilineText | PM only — managing multiple people/deadlines |
| PM Question 2 | `fldg5aLxaxuBXDNiM` | multilineText | PM only — editor misses deadline scenario |
| Sales Question 1 | `fldShnAAJBbdfPPwh` | multilineText | Sales only — experience closing deals |
| Sales Question 2 | `fldfE9v7UzWHjMciA` | multilineText | Sales only — objection handling |
| Reviewer Notes | `fldqpjpjidJxrQiF2` | multilineText | Internal use only |
| Contains Phrase (Sean is Cool) | `fldiPpMlfZhoOFpSr` | checkbox | Auto-checked by backend if phrase found in answers |

---

## Submit Endpoint

**All applications post to the portal backend — never direct to Airtable from the frontend.**

```
POST https://api.contentbug.io/api/careers/apply
Content-Type: multipart/form-data

fields       — JSON string of all text form data
speed        — File: speed test screenshot
bestEdit     — File: best edit video (editor only)
editVerify   — File: edit verification file (editor only)
```

The portal route (`server.js`) handles:
- Writing all fields to this Airtable base using the real field IDs above
- Uploading files to Airtable attachments
- Setting `Application Status` = "New" on every submission
- Auto-checking `Contains Phrase (Sean is Cool)` by scanning all text fields

---

## VideoTiny Setup

1. Create a project at videotiny.com
2. Update `careers.html` script config:

```js
VIDEOTINY_ID: 'your_project_id_here',
```

Video URLs are stored in the `Video Introduction URL` field after recording.

---

## Views to Create in Airtable

Go to the base and manually create 3 filtered views:

| View Name | Filter |
|---|---|
| Editor Applicants | Role = "Professional Editor" |
| Project Manager Applicants | Role = "Project Manager" |
| Sales Applicants | Role = "Sales Closer" |
