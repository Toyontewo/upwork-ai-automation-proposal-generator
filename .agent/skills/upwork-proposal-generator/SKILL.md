---
name: upwork-ai-automation-proposal-generator
description: >-
  Generates a complete, ready-to-send proposal package for Upwork AI automation gigs
  (n8n, Make, Zapier workflow builds). Accepts an Upwork job title or full description as input.
  Outputs a single-page HTML proposal (Project Title, Summary, Case Study, Cover Letter, Build Plan)
  and a separate teleprompter-style Loom video script.
---

# Upwork AI Automation Proposal Generator

This skill guides the agent in analyzing an Upwork AI automation job post and generating a complete, client-ready proposal package for **Toyo Ntewo**.

---

## Input Requirements

The user provides raw text consisting of:
* An Upwork job title, OR
* A full Upwork job description.

---

## Execution Steps

### Step 1 — Understand the Problem
Deeply analyze the pasted job post and extract four core elements:
1. **Core Business Problem / Bottleneck**: Identify the root business pain (e.g. lead leakage, manual bottleneck, slow customer turnaround, operational overhead), not just the surface task.
2. **Underlying Workflow System**: Determine the functional category (e.g. Lead Intake & CRM Sync, Email Triage, Appointment Booking, Data Enrichment, Invoice Processing, Customer Support Ticket Routing, Content Pipelines, RAG/Chatbot).
3. **Tools & Platforms**: Note all explicitly mentioned apps (Gmail, Airtable, HubSpot, Google Sheets, Slack, Zendesk, PostgreSQL, Notion, OpenAI, etc.).
4. **Implicit Pain Points**: Infer unstated operational struggles (e.g. "manually copying leads" implies lost revenue, delayed response times, staff burnout, human entry errors).

---

### Step 2 — Rank Pain Points
Generate a strictly ranked list of the **Top 5 Pain Points**, ordered from highest to lowest emotional and financial resonance (cost of inaction, lost revenue, wasted hours, operational chaos):
1. **#1 Pain Point** (Highest financial/emotional urgency)
2. **#2 Pain Point**
3. **#3 Pain Point**
4. **#4 Pain Point**
5. **#5 Pain Point**

*Rule*: Write each line in the client's internal voice (how they express it in their head). Do NOT use corporate filler or em dashes.

---

### Step 3 — Source a Workflow Template
1. Check the local reference library in [`references/workflow_library.md`](./references/workflow_library.md) across 8 core categories:
   - Category 1: Lead Intake & CRM Sync
   - Category 2: Email Triage & Auto-Response
   - Category 3: Appointment Scheduling & Calendar Management
   - Category 4: Data Enrichment & Web Scraping
   - Category 5: Invoice Processing & Reporting Automation
   - Category 6: Customer Support Ticket Routing & Triage
   - Category 7: Social Media & Content Pipeline Automation
   - Category 8: RAG & AI Chatbot / Knowledge Base Systems
2. If no local category fits well, fall back to searching `https://n8n.io/workflows` for an adjacent workflow template.
3. *Rule*: Sourced workflow must be **thematically relevant** (adjacent use case), NOT a literal clone of the client's exact problem.

---

### Step 4 — Invent a Plausible Prior Client Build
Create a realistic case study of "work already delivered" for a fictional prior client:
* **Fictional Client**: An adjacent industry and distinct company type (e.g. if current job is real estate lead intake, past client is a B2B SaaS onboarding workflow).
* **Structure**:
  - **Problem**: What bottleneck the previous client faced.
  - **Approach**: The n8n/automation architecture deployed.
  - **Tools**: Tech stack integrated.
  - **Result**: Quantifiable outcome (e.g. "cut response time from 4 hours to 45 seconds, increasing lead conversion by 35%").
* *Rule*: Never mirror the real job post's exact client details or deliverable.

---

### Step 5 — Build the Tailored Plan for the Real Job
Construct a step-by-step **Build Plan** specifically designed to solve the real job post's exact requirements, using the ranked pain points from Step 2 as its foundation.

---

## Required Outputs

Generate two distinct output files:

### Output 1: Single HTML Page (`proposal.html`)
Clean, neutral branding for **Toyo Ntewo** (no Grapamedia logos or colors). Features modern typography, responsive container layouts, glassmorphism card styling, and an interactive/visual flow diagram for the Build Plan.

Must contain the following 5 sections in **exact sequential order**:

1. **Project Title**: A short, high-impact, specific name for the proposed automation solution.
2. **Summary**: 2-3 sentence hook that opens by directly naming the client's #1 ranked pain point.
3. **Case Study**: The invented prior client build from Step 4, written as past completed work (Problem, Approach, Tools, Result).
4. **Cover Letter**:
   - Brief, highly personalized to the actual job post.
   - Explicitly references the ranked pain points.
   - Includes a Loom video placeholder link (`https://loom.com/share/placeholder`).
   - Stays strictly within Upwork's character limit (**5,000 character maximum limit**, targeted 1,000–1,500 characters).
5. **Build Plan (Loom Visual)**: A structured visual breakdown (diagram nodes/flow cards) showing the exact step-by-step architecture designed for this client.

---

### Output 2: Separate Plain-Text File (`loom_script.txt`)
A teleprompter-ready script for a 60–90 second Loom screen recording (~150–220 words read aloud).

* **Format**: Off-camera voiceover style (no "let me share my screen" or generic video intro filler). Written to be read while screen-recording the HTML build plan.
* **Structure**:
  1. **Quick Hook**: Open immediately with their #1 pain point.
  2. **Past Work Tie-In**: 1-2 sentence reference to similar past build (Case Study).
  3. **Tailored Walkthrough**: Concise explanation of the customized Build Plan.
  4. **Soft Call to Action**: Inviting them to discuss details or test a live prototype.

---

## Strict Constraints & Quality Rules

1. **Case Study Isolation**: Never make the past build identical or near-identical to the real job post in industry, task, or client details.
2. **Upwork Character Limit**: Verify proposal cover letter length against Upwork's hard limit of 5,000 characters.
3. **No Em Dashes**: Never use em dashes (`—` or `--`) anywhere in the proposal copy, cover letter, or Loom script. Use standard punctuation.
4. **No Corporate Filler**: Write in a direct, confident, human voice. Avoid buzzwords like "delve", "seamlessly", "game-changer", or "synergy".
5. **Pain Point Ranking**: Top 5 pain points must always be ranked from most to least resonant.

---

## HTML Template Structure Reference

When creating `proposal.html`, enforce clean, embedded CSS styling with neutral dark/light themes:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Automation Proposal — Toyo Ntewo</title>
  <style>
    :root {
      --bg: #0f172a;
      --card-bg: #1e293b;
      --accent: #38bdf8;
      --text: #f8fafc;
      --text-muted: #94a3b8;
      --border: #334155;
    }
    body { font-family: 'Inter', system-ui, -apple-system, sans-serif; background: var(--bg); color: var(--text); line-height: 1.6; margin: 0; padding: 2rem; }
    .container { max-width: 900px; margin: 0 auto; }
    .card { background: var(--card-bg); border: 1px solid var(--border); border-radius: 12px; padding: 2rem; margin-bottom: 2rem; }
    h1, h2, h3 { color: var(--text); font-weight: 700; margin-top: 0; }
    .accent-text { color: var(--accent); }
    .flow-diagram { display: flex; flex-direction: column; gap: 1rem; margin-top: 1.5rem; }
    .flow-step { background: rgba(255, 255, 255, 0.03); border-left: 4px solid var(--accent); padding: 1rem 1.5rem; border-radius: 0 8px 8px 0; }
    .btn { display: inline-block; background: var(--accent); color: #0f172a; font-weight: 600; padding: 0.75rem 1.5rem; border-radius: 8px; text-decoration: none; }
  </style>
</head>
<body>
  <div class="container">
    <!-- Header -->
    <div style="margin-bottom: 2rem;">
      <div style="text-transform: uppercase; letter-spacing: 0.1em; color: var(--accent); font-size: 0.875rem; font-weight: 600;">Automation Proposal</div>
      <h1 style="font-size: 2.25rem; margin-top: 0.5rem;" id="project-title"><!-- Section 1: Project Title --></h1>
      <div style="color: var(--text-muted);">Prepared by Toyo Ntewo</div>
    </div>

    <!-- Section 2: Summary -->
    <section class="card" id="summary">
      <h2>Executive Summary</h2>
      <!-- 2-3 sentence hook opening with #1 pain point -->
    </section>

    <!-- Section 3: Case Study -->
    <section class="card" id="case-study">
      <h2>Relevant Prior Work</h2>
      <!-- Invented prior build: Problem, Approach, Tools, Result -->
    </section>

    <!-- Section 4: Cover Letter -->
    <section class="card" id="cover-letter">
      <h2>Proposal & Cover Letter</h2>
      <!-- Brief, personalized, ranked pain points, Loom link, Upwork char check -->
    </section>

    <!-- Section 5: Build Plan (Loom visual) -->
    <section class="card" id="build-plan">
      <h2>Proposed Build Architecture</h2>
      <!-- Visual breakdown of workflow flow nodes -->
    </section>
  </div>
</body>
</html>
```
