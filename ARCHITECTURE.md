# Instagram Leads AI Automation - Secure Production Demo

## Overview
This document describes the architecture of the **Instagram Leads Automation workflow** built in **n8n**, including security, data flow, and node responsibilities.

This workflow is **production-style**, but uses **mock/demo endpoints** for safety during testing.

---

## Architecture Flow

The workflow consists of the following steps:

1. **Secure Webhook**
   - Receives incoming Instagram leads.
   - Path: `/ig-leads-secure`
   - Method: POST
   - Security: Requires `x-webhook-secret` header.

2. **Verify Webhook Secret**
   - Checks that the secret header matches the expected value.
   - Invalid requests are rejected immediately.

3. **Normalize Lead Data**
   - Extracts relevant fields (`username`, `message`) from incoming JSON.
   - Ensures consistent structure for downstream nodes.

4. **Validate Lead**
   - Ensures required fields (e.g., username) are present.
   - Prevents empty or malformed payloads from continuing.

5. **Save Lead (Demo DB)**
   - Sends normalized data to `jsonplaceholder.typicode.com` (mock database API).
   - Demonstrates integration with external APIs without storing real data.

6. **AI Qualification (Mock Logic)**
   - Applies simple AI rules:
     - If `message` contains "price" → `HOT`
     - Else → `COLD`
   - Mocked for demo purposes; can be replaced with Gemini / OpenAI API in production.

7. **Send Audit Log**
   - Sends full payload to `webhook.site` for logging and demonstration.
   - Shows complete workflow execution and can be used for debugging.

---

## ASCII Diagram of Workflow

pgsql
نسخ الكود
      +----------------------+
      |  Instagram / Client  |
      +----------+-----------+
                 |
                 v
      +----------------------+
      |   Secure Webhook     |
      |  (/ig-leads-secure) |
      +----------+-----------+
                 |
                 v
      +----------------------+
      | Verify Webhook Secret|
      |  (Header check)     |
      +----------+-----------+
                 |
                 v
      +----------------------+
      | Normalize Lead Data  |
      |  (username, message)|
      +----------+-----------+
                 |
                 v
      +----------------------+
      |  Validate Lead       |
      | (username not empty) |
      +----------+-----------+
                 |
                 v
      +----------------------+
      | Save Lead (Demo DB)  |
      |  jsonplaceholder     |
      +----------+-----------+
                 |
                 v
      +----------------------+
      | AI Qualification     |
      |  (Mock Logic HOT/COLD)|
      +----------+-----------+
                 |
                 v
      +----------------------+
      | Send Audit Log       |
      |  webhook.site        |
      +----------------------+
yaml
نسخ الكود

---

## Security Highlights

- **Header Secret Validation**: Requests must include `x-webhook-secret`.
- **No Hardcoded Secrets**: All sensitive values intended for environment variables.
- **Fail-Safe Design**: Invalid requests are rejected early.
- **Demo Endpoints Only**: External APIs used are strictly for testing (safe, non-production data).

---

## Extensibility

- **DB Replacement**: Switch `jsonplaceholder` with real database/CRM API.
- **AI Replacement**: Replace mock AI logic with Gemini or OpenAI endpoint.
- **Logging Replacement**: Use internal logging system instead of `webhook.site`.
- **HTTPS**: Add reverse proxy or SSL termination for secure production deployment.

---

## Summary

This architecture ensures:

- **Security-first design**
- **Clear data flow**
- **Production-ready structure**
- **Safe demonstration for portfolio or interviews**
