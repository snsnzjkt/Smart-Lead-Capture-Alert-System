# 🧩 Smart Lead Capture & Alert System (Tally → Supabase + Slack/Gmail)

This make.com automation captures form submissions from **Tally**, checks for duplicates in **Supabase**, logs them in a CRM table, and sends a notification via **Slack**. If Slack fails, it sends a fallback email using **Gmail** — ensuring no lead is missed.

---

## 🛠 Tech Stack

* **make.com** (workflow orchestration)
* **Tally** (form input via webhook)
* **Supabase** (PostgreSQL database & API)
* **Slack** (notifications)
* **Gmail** (fallback email alerts)

---

## 📌 Workflow Overview

1. **Webhook Trigger**
   Listens for POST submissions from a Tally form.

2. **Field Parser**
   Extracts and maps form fields: First Name, Last Name, Email, Phone, and Notes.

3. **Duplicate Check**
   Queries Supabase for existing entries based on email.

4. **Insert Record**
   Adds new submissions to the `form_submissions` table if not a duplicate.

5. **Send Slack Notification**
   Sends a formatted message to a designated Slack channel.

6. **Fallback Logic**
   If Slack fails or returns an error, sends the notification via Gmail.

---

## 📁 Data Structure (Supabase)

Table: `form_submissions`

| Column        | Type                     |
| ------------- | ------------------------ |
| first\_name   | text                     |
| last\_name    | text                     |
| email         | text                     |
| phone\_number | text                     |
| notes         | text                     |
| created\_at   | timestamp (default: now) |

---

## ⚠️ Error Handling

* Slack errors (e.g., channel not found, downtime) are caught by a conditional `IF` node.
* If triggered, the fallback route sends a Gmail notification to a predefined address.
* Duplicate form entries (same email) are silently dropped to avoid re-entry.

---

## ✅ Use Cases

* Automated lead capture for landing pages
* Contact form intake with redundancy
* CRM population with notification logic
* Simple client onboarding intake system

---

## 🧪 Sample Input

```json
{
  "fields": [
    { "name": "First Name", "value": "Jane" },
    { "name": "Last Name", "value": "Doe" },
    { "name": "Email", "value": "jane.doe@example.com" },
    { "name": "Phone", "value": "+639171234567" },
    { "name": "Notes", "value": "Interested in website redesign." }
  ]
}
```

---

## 📂 Files

* `Test Task - Edrine.json`: Full export of the make.com workflow (importable).
* `.env` or credentials must be configured inside make.com for:

  * Supabase API
  * Slack OAuth2
  * Gmail OAuth2

---

## 🧠 Author

**Edrine Frances A. Esguerra**
[LinkedIn](https://www.linkedin.com/in/edrineesguerra/) | `edrineesguerra4@gmail.com`

---

Let me know if you'd like a Markdown version or want to tweak this for a Notion page or portfolio post.
