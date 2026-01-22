# Instagram Leads AI Automation (Secure Production Demo)

## Overview
This repository contains a **secure, production-style automation workflow** built with **n8n** to demonstrate how Instagram leads can be received, validated, stored, analyzed, and logged using modern automation practices.

This project is designed as a **portfolio and demonstration project**, following real-world production architecture without exposing any real credentials.

---

## Use Case
Businesses and agencies often receive large volumes of Instagram messages and leads, which leads to:
- Manual processing
- Slow response times
- No prioritization of high-value leads

This workflow demonstrates how to automate that process securely and intelligently.

---

## Architecture Flow

1. Secure Webhook receives incoming lead data
2. Request is authenticated using a shared secret
3. Payload is normalized and validated
4. Lead is stored in a database (demo API)
5. Lead is qualified using AI logic (mocked)
6. Full execution is logged externally for audit/debugging

Instagram / Client
↓
Secure Webhook
↓
Secret Validation
↓
Data Normalization
↓
Input Validation
↓
Demo Database API
↓
AI Qualification (Mock)
↓
Audit Logging

yaml
نسخ الكود

---

## External Services Used (Demo Only)

⚠️ **Important:**  
The following external services are used **strictly for testing and demonstration purposes**:

| Service | Purpose |
|------|------|
| jsonplaceholder.typicode.com | Simulated database API |
| webhook.site | Request logging & debugging |
| curl / CLI | Manual request testing |

These services **can be replaced in production** with:
- Real databases (PostgreSQL, Supabase, CRM APIs)
- Logging systems (Datadog, ELK, CloudWatch)
- AI providers (Gemini, OpenAI, Claude)

---

## Security Design
- No API keys or tokens are stored in the workflow
- Authentication is enforced using HTTP headers
- All sensitive values are designed to be injected via environment variables
- Invalid or malformed requests are rejected early
- No destructive operations are performed

---

## Testing the Workflow

Example request using `curl`:

curl -X POST http://localhost:5678/webhook-test/ig-leads-secure ^
  -H "Content-Type: application/json" ^
  -H "x-webhook-secret: DEMO_SECRET_123" ^
  -d "{\"username\": \"test_user\", \"message\": \"Hi, I want to know the price\"}"

Expected behavior:

Request passes security validation

Lead is processed through all workflow nodes

Execution log appears in webhook.site

Production Readiness
This workflow represents a production-ready architecture, meaning:

No code changes are required to deploy it live

Only configuration (credentials, environment variables) is needed

External demo services can be swapped without changing logic

Disclaimer
This repository does not contain real credentials.
All secrets, tokens, and endpoints are placeholders for demonstration purposes only.

yaml
نسخ الكود
