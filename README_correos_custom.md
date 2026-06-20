# Cold Outreach Email Generator

An n8n workflow that reads a list of leads from Google Sheets and generates fully personalized cold outreach emails using AI — at scale, without writing a single one by hand.

Built by [Juan Pedro Torres](https://www.linkedin.com/in/juanpedrotorressefiraai) · [Sefira AI](https://sefiraai.com) — AI automation for SMEs and IT teams.

## What it does

1. **Reads leads** from a Google Sheets database (name, company, role, sector, country)
2. **Generates a personalized email** for each lead using GPT, following a structured cold-email framework:
   - Personalized greeting with the real recipient's name
   - Natural mention of their company and sector
   - A specific pain point related to their industry
   - A no-commitment solution offer
   - A simple call to action (reply to coordinate a 15-min call)
3. **Outputs structured JSON** (subject + body) via a Structured Output Parser — no inconsistent formatting, no manual cleanup
4. **Writes the results** back to a separate Google Sheet, ready to be sent through your email tool of choice

## Architecture

```
Manual Trigger
      │
      ▼
  Read Leads (Google Sheets)
      │
      ▼
  Limit (batch control)
      │
      ▼
  AI Email Generator (GPT + Structured Output Parser)
      │
      ▼
  Write to cold_outreach (Google Sheets)
```

## Why structured output matters

A common failure mode in AI-generated cold email workflows is inconsistent formatting — the model sometimes returns plain text, sometimes JSON, sometimes a mix. This workflow uses a **Structured Output Parser** with a strict schema (`asunto`, `cuerpo`) to guarantee clean, predictable output every single time, regardless of how creative the model gets with the email copy itself.

## Stack

- **n8n** — workflow orchestration
- **OpenAI API** (gpt-4.1-nano) — email generation, optimized for cost/quality balance at scale
- **Google Sheets** — lead source and output storage

## Setup

1. Import `workflow.json` into your n8n instance
2. Connect your own credentials:
   - OpenAI API key
   - Google Sheets OAuth2 (two connections: one for reading leads, one for writing output)
3. Point the `leads` node to your own lead spreadsheet
4. Point the `cold_outreach` node to your output spreadsheet
5. Adjust the prompt's sender context (agency name, value proposition, offer) to match your business
6. Run manually or trigger on a schedule

> Credentials are **not** included in the exported JSON — you'll need to reconnect your own.

## About

I'm Juan Pedro, founder of **Sefira AI**, an automation agency helping SMEs and IT teams implement practical AI solutions for sales, support and internal operations.

📧 jtorres@sefiraai.com
🔗 [sefiraai.com](https://sefiraai.com)
