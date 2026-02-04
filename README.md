---


```markdown
# 🚨 n8n SOS Alert Workflow

This repository documents the deployment of **n8n** on Render and the custom workflow built for Telegram‑based SOS alerts, HTTP requests, and scheduled triggers.

---

## 📦 Project Overview

- **Platform:** n8n (workflow automation tool)
- **Hosting:** Render (Docker deployment)
- **Workflow Features:**
  - Telegram trigger (listens for incoming messages)
  - Conditional logic (If blocks)
  - HTTP requests to external API (`http://rp-api.com/json/`)
  - Wait nodes for controlled execution
  - Telegram actions (send text, send location)
  - Data operations (insert row, get rows, loop over items)
  - Scheduled triggers for repeated checks

---

## 🚀 Deployment Steps

### 1. GitHub Repo

- Create a repo (e.g., `n8n-sos-alert`)
- Add a `Dockerfile`:
  ```dockerfile
  FROM n8nio/n8n:latest
  ```
- Push to GitHub.

### 2. Render Setup

- Create **New Web Service** on Render.
- Source: GitHub repo.
- Environment: Docker.
- Port: `5678`.

### 3. Environment Variables

Set the following in Render → Service → Environment:

```
N8N_BASIC_AUTH_ACTIVE=true
N8N_BASIC_AUTH_USER=aakiltayyab
N8N_BASIC_AUTH_PASSWORD=Aakil@8810
N8N_ENCRYPTION_KEY=aakiltayyab8810449027aakiltayyab
```

### 4. Access Service

- URL: `https://n8n-sos-alert.onrender.com`
- Login with username/password above.

### 5. Workflow Import

- Export workflow JSON from local n8n.
- Import into Render n8n UI.
- Activate workflow.

---

## ⚠️ Notes

- Do not commit secrets (API keys, tokens) into GitHub repo.
- Keep `N8N_ENCRYPTION_KEY` safe; changing it will break old credentials.
- SSL certificate may take 30–60 minutes to verify after first deploy.

---

## 🛠 Workflow Architecture

```
Telegram Trigger → If Condition → HTTP Request → Wait → Telegram Send Message
       ↓
   Loop Over Items → Insert Row → Get Rows → If Condition → Telegram Send Location
       ↓
   Schedule Trigger → HTTP Request → Edit Fields → Replace Me (future actions)
```

---
