# Lead Capture Automation (n8n)

An end-to-end automation workflow that captures incoming lead data, cleans and standardizes it, and logs it automatically to Google Sheets — with no manual data entry.

Built with **n8n** (self-hosted on Docker), the **Google Sheets API**, and **Google Cloud OAuth 2.0**.

---

## What it does

When lead data is sent to a webhook (e.g. from a signup form), the workflow:

1. **Receives** the incoming data via an HTTP webhook (POST).
2. **Transforms** it — extracts and renames the fields, adds a `status` and a `received_at` timestamp.
3. **Stores** it — appends a new row to a Google Sheet automatically.

The result: every new lead is captured and organized in a spreadsheet in real time, with zero manual work.

---

## Workflow

| Node | Role |
|------|------|
| **Webhook** | Entry point — receives lead data over HTTP (POST) |
| **Edit Fields** | Cleans and standardizes the incoming JSON fields |
| **Google Sheets** | Appends the structured record as a new row |

---

## Tech stack

- **n8n** — workflow automation platform (self-hosted via Docker)
- **Docker** — containerized deployment
- **Google Sheets API** — data storage
- **Google Cloud OAuth 2.0** — secure authentication

---

## How to run it

1. **Import the workflow** — in n8n: *Workflows → Import from File → `lead-capture-workflow.json`*
2. **Set up Google Sheets credentials** — enable Google Sheets API + Google Drive API in Google Cloud, create an OAuth 2.0 Client ID, add the redirect URI `http://localhost:5678/rest/oauth2-credential/callback`, and add your account as a test user.
3. **Prepare the sheet** — create a Google Sheet named `leads` with columns: `full_name | email | company | status | received_at`
4. **Test it:**
```bash
   curl -X POST http://localhost:5678/webhook/test-lead \
     -H "Content-Type: application/json" \
     -d '{"name":"Ali","email":"ali@test.com","company":"Acme"}'
```
   A new row should appear in the `leads` sheet.

---

## What I learned

- Building and deploying n8n on Docker (self-hosted)
- Working with webhooks, triggers, and data-transformation expressions
- Configuring a full Google Cloud OAuth 2.0 flow from scratch
- Debugging automation workflows by validating live output at each step

---

## Author

**Abdalelah Elmahdi** — Electronics Engineer (Computer & Networks) | AI & Automation
[GitHub](https://github.com/abdalelah0) · [LinkedIn](https://linkedin.com/in/abdalelah-elmahdi)
