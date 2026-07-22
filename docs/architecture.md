# System Architecture

## Overview

The **AI-Powered Competitor News Monitor & Executive Weekly Digest** is designed as a staged automation pipeline in n8n. The architecture separates deterministic workflow operations from probabilistic AI reasoning so that each part of the system remains easier to understand, test, maintain, and troubleshoot.

The workflow is organized into five logical stages:

1. Orchestration
2. Ingestion
3. Normalization
4. AI Intelligence
5. Delivery

---

## Architecture Diagram

```text
┌──────────────────────┐
│  Schedule Trigger    │
│  Monday at 9:00 AM   │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐       ┌──────────────────────┐
│ Fetch OpenAI RSS     │       │ Fetch Google AI RSS  │
└──────────┬───────────┘       └──────────┬───────────┘
           │                              │
           └──────────────┬───────────────┘
                          ▼
               ┌──────────────────────┐
               │ Merge RSS Feeds      │
               └──────────┬───────────┘
                          ▼
               ┌──────────────────────┐
               │ Combine RSS Content  │
               │ and label sources    │
               └──────────┬───────────┘
                          ▼
               ┌──────────────────────┐
               │ Google Gemini        │
               │ Weekly synthesis     │
               └──────────┬───────────┘
                          ▼
               ┌──────────────────────┐
               │ Format HTML Digest   │
               └──────────┬───────────┘
                          ▼
               ┌──────────────────────┐
               │ Gmail Delivery       │
               └──────────────────────┘
```

---

# Architecture Components

## 1. Orchestration

The workflow begins with an **n8n Schedule Trigger** configured to execute automatically every **Monday at 9:00 AM (America/New_York)**.

### Responsibilities

- Starts the workflow automatically
- Provides a predictable weekly execution schedule
- Eliminates manual intervention
- Enables repeatable workflow executions

This node serves as the orchestration layer and initiates the complete automation pipeline.

---

## 2. Ingestion

Two independent HTTP Request nodes retrieve the latest AI-related announcements from official publisher RSS feeds.

### Data Sources

- OpenAI News RSS
- Google AI Blog RSS

### Responsibilities

- Retrieve the latest articles
- Keep source feeds isolated
- Support independent validation
- Allow easy addition of future RSS sources

Using official publisher feeds ensures higher reliability and reduces unnecessary noise compared to third-party news aggregators.

---

## 3. Normalization

After retrieval, both RSS feeds are merged and transformed into a standardized structure before being sent to the AI model.

### Responsibilities

- Merge RSS responses
- Preserve article source information
- Standardize input structure
- Generate metadata
- Produce a single payload for AI processing

Example output:

```json
{
  "combinedFeeds": "...",
  "sourceCount": 2,
  "generatedAt": "2026-07-21T22:05:04.901Z"
}
```

This deterministic transformation keeps preprocessing outside the AI model, improving consistency and reducing unnecessary token usage.

---

## 4. AI Intelligence

Google Gemini receives the normalized RSS content and generates a concise executive weekly digest.

### AI Responsibilities

- Analyze supplied RSS articles
- Remove duplicate stories
- Rank the most important announcements
- Generate executive summaries
- Explain business impact
- Preserve original article URLs

The AI prompt explicitly instructs Gemini to use only the supplied RSS content and avoid generating unsupported information.

---

## 5. Delivery

The AI-generated digest is converted into a responsive HTML newsletter before being delivered through Gmail.

### Responsibilities

- Generate HTML email
- Create dynamic subject line
- Format executive newsletter
- Deliver automatically using Gmail OAuth

The HTML formatter separates presentation from AI generation, making it easy to change the output format without modifying the summarization logic.

---

# Design Principles

This workflow follows several software engineering best practices.

## Separation of Concerns

Each workflow stage has a single responsibility.

| Stage | Responsibility |
|--------|----------------|
| Schedule Trigger | Workflow orchestration |
| HTTP Request | Data retrieval |
| Merge + Code | Data normalization |
| Gemini | AI reasoning |
| HTML Formatter | Presentation |
| Gmail | Delivery |

---

## Deterministic Before AI

Deterministic workflow logic is executed before invoking the AI model.

Deterministic tasks include:

- Scheduling
- RSS retrieval
- Feed merging
- Data normalization
- HTML generation
- Email delivery

The AI model is only responsible for:

- Summarization
- Story prioritization
- Insight generation
- Business impact analysis

This architecture improves reliability, debugging, maintainability, and operational cost.

---

## Grounded AI

The prompt instructs Gemini to rely exclusively on the supplied RSS feeds.

The model is instructed not to:

- Invent announcements
- Generate unsupported claims
- Fabricate dates
- Create fake URLs
- Introduce external knowledge

This significantly reduces hallucination risk.

---

# Scalability

The workflow can easily support additional RSS sources by adding more HTTP Request nodes before the merge stage.

Future enhancements may include:

- Additional competitor feeds
- Article deduplication
- Date filtering
- Priority scoring
- Slack notifications
- Microsoft Teams delivery
- Notion integration
- Database storage
- Dashboard reporting

---

# Security

The repository does not store credentials.

Sensitive information is managed using n8n Credentials.

Protected resources include:

- Google Gemini API
- Gmail OAuth

Users importing the workflow must configure their own credentials before execution.

---

# Technology Stack

- n8n Cloud
- Google Gemini
- Gmail API
- JavaScript
- HTML
- RSS
- OAuth 2.0

---

# Architectural Summary

The workflow intentionally separates deterministic automation from AI reasoning.

Traditional workflow components handle scheduling, data collection, normalization, formatting, and delivery, while Google Gemini focuses exclusively on reasoning, summarization, and insight generation.

This hybrid architecture produces a reliable, maintainable, and scalable automation pipeline suitable for executive AI news monitoring.