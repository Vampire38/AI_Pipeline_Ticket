# AI Automation Intern Assessment — n8n Workflows

## Candidate
Thilak

---

# 📌 Overview

This project contains two AI-powered automation workflows built using **n8n**:

### 1. AI Support Ticket Triage System
Automatically classifies incoming support tickets into categories, assigns priority, generates summaries, and drafts responses.

### 2. AI Lead Intelligence Pipeline
Processes raw lead data from multiple sources, cleans and deduplicates it, enriches it with external data, applies AI-based scoring, and generates executive-level insights and reports.

---

# 🧠 Technologies Used

- n8n (Workflow Automation)
- OpenAI / Groq / OpenRouter (AI Processing)
- Google Sheets (Data Storage)
- HTTP Requests (Data Enrichment)
- Gmail / Telegram (Notifications)
- JavaScript (Function Nodes)

---

# ⚙️ Workflow 1 — AI Support Ticket Triage

## 🎯 Objective
To automatically analyze incoming support tickets and categorize them for faster resolution.

## 🔄 Workflow Steps

1. **Trigger**
   - Webhook / Manual Trigger / Google Sheets input

2. **Validation**
   - Ensures required fields exist:
     - name
     - email
     - subject
     - message

3. **Text Normalization**
   - Combines subject + message into a single input

4. **Rule-Based Pre-Detection**
   - Detects keywords:
     - billing → billing category
     - login/password → account_access
     - bug/error → technical_issue

5. **AI Processing**
   - Generates:
     - category
     - priority
     - summary
     - draft_reply

6. **Storage**
   - Saves structured output to Google Sheets

7. **Notification**
   - Sends formatted email via Gmail/Telegram

8. **Error Handling**
   - Invalid input branch
   - AI failure fallback response
   - Logging of failed executions

## 📤 Output Fields

- category (billing / technical_issue / account_access / feature_request / general_question)
- priority (low / medium / high)
- summary
- draft_reply
- timestamp

---

# ⚙️ Workflow 2 — AI Lead Intelligence Pipeline

## 🎯 Objective
To analyze, enrich, and score leads using AI and external data sources.

## 🔄 Workflow Architecture

### Stage 1 — Ingestion
- Sources:
  - Google Sheets
  - Webhook / CSV input
- Adds metadata:
  - source
  - ingestion_time

---

### Stage 2 — Validation & Deduplication
- Rejects invalid leads:
  - missing company
  - missing website
- Deduplication logic:
  - company + contact_name OR website domain
- Duplicates stored separately

---

### Stage 3 — Data Enrichment
- Uses HTTP requests to:
  - fetch website metadata
  - extract descriptions
  - infer industry keywords
  - parse domain data

---

### Stage 4 — AI Analysis

#### Lead Scoring
- lead_score (1–100)
- confidence_score
- reasoning

#### Outreach Generation
- value_proposition
- opening_line
- objection_prediction
- next_best_action

---

### Stage 5 — Reporting

Generates:

#### Structured Lead Record
- company
- lead_score
- segment (Hot / Warm / Cold)
- insights
- source

#### Executive Summary
- total leads processed
- duplicates detected
- average lead score
- top performing leads
- segment distribution
- failure cases

---

### Stage 6 — Notifications
- Sends report via:
  - Gmail / Slack / Telegram / Discord

---

### Stage 7 — Reliability & Error Handling
- Retry logic for API calls
- Partial failure handling
- Logging of failed leads
- Duplicate prevention system

---

# 🧾 AI Prompt Design

The AI prompts were designed with:

- Strict JSON output format
- Controlled schema generation
- Minimal hallucination risk
- Structured fields for easy parsing in n8n

Example structure enforced:

```json
{
  "lead_score": 85,
  "confidence_score": 0.9,
  "reasoning": "...",
  "segment": "Hot"
}