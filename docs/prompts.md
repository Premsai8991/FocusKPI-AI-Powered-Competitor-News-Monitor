# AI Prompts Used During Development

## Overview

This document contains representative prompts used during the design and implementation of the AI-Powered Competitor News Monitor & Executive Weekly Digest.

Development primarily used **ChatGPT (GPT-5.5)** as an engineering assistant for workflow architecture, prompt engineering, debugging, documentation, and design review.

Google Gemini was used inside the workflow itself as the AI summarization engine.

---

# AI Model Used

| Tool | Purpose |
|------|---------|
| ChatGPT (GPT-5.5) | Architecture, workflow design, prompt engineering, debugging, documentation |
| Google Gemini 3 Flash Preview | Executive news summarization inside n8n |

---

# Representative Prompts

## 1. Workflow Architecture

### Prompt

> Design an n8n workflow that collects AI news from official RSS feeds, summarizes the most important stories using Google Gemini, and emails an executive weekly digest.

### Purpose

Initial workflow architecture.

---

## 2. Workflow Design Review

### Prompt

> Explain why deterministic workflow logic should be separated from AI reasoning instead of letting the AI perform every task.

### Purpose

Architecture validation.

---

## 3. RSS Feed Evaluation

### Prompt

> Compare several AI-related RSS feeds based on reliability, update frequency, signal-to-noise ratio, and suitability for executive weekly summaries.

### Purpose

Selecting reliable news sources.

---

## 4. Prompt Engineering

### Prompt

> Design a prompt that minimizes hallucinations, removes duplicate news stories, preserves article attribution, and produces executive-level summaries.

### Purpose

Google Gemini prompt design.

---

## 5. AI Summarization Strategy

### Prompt

> How should an executive weekly AI news digest be structured for software engineers and engineering managers?

### Purpose

Summary formatting.

---

## 6. HTML Email Design

### Prompt

> Design a responsive HTML email newsletter suitable for Gmail with a professional executive report layout.

### Purpose

Newsletter formatting.

---

## 7. Workflow Debugging

### Prompt

> Help debug JavaScript expressions and data flow between n8n nodes while preserving modular workflow design.

### Purpose

Workflow implementation.

---

## 8. Repository Documentation

### Prompt

> Generate professional GitHub documentation including README, architecture documentation, and implementation details.

### Purpose

Project documentation.

---

## 9. Architecture Documentation

### Prompt

> Explain the workflow architecture in terms of orchestration, ingestion, normalization, AI intelligence, and delivery.

### Purpose

Technical documentation.

---

## 10. Engineering Review

### Prompt

> Review the workflow as a senior automation architect and recommend improvements before production deployment.

### Purpose

Architecture review.

---

## 11. Project Presentation

### Prompt

> Help organize the GitHub repository with diagrams, screenshots, workflow demonstrations, documentation, and supporting materials suitable for technical review.

### Purpose

Repository organization.

---

## AI Usage Philosophy

AI was used as an engineering assistant throughout the project rather than as an autonomous developer.

Every workflow decision, implementation detail, prompt refinement, and architectural choice was reviewed before being incorporated into the final solution.

Human judgment guided:

- Workflow architecture
- Node organization
- RSS source selection
- Prompt refinement
- Testing
- Documentation
- Final implementation

---

# Development Workflow

The overall development process followed these stages:

1. Workflow planning
2. Architecture review
3. RSS source selection
4. Prompt engineering
5. Workflow implementation
6. Testing and debugging
7. HTML email design
8. Documentation
9. GitHub repository preparation

---

# Summary

ChatGPT accelerated brainstorming, architecture review, debugging, prompt engineering, and documentation while the workflow implementation, testing, and final design decisions remained intentionally engineered and validated throughout development.