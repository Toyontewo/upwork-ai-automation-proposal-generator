---
name: upwork-ai-automation-proposal-generator
description: >-
  Generates a complete proposal package for Upwork AI automation gigs.
  Outputs 6 files: proposal.html, build-plan.html, loom_script.txt,
  workflow.json (from n8n.io templates), upwork_macro.txt, and teleprompter.html.
---

# Upwork AI Automation Proposal Generator

Generates a multi-page proposal system for **Toyo Ntewo** targeting Upwork AI automation jobs (n8n, Make, Zapier). Analyzes the job post, sources a real n8n workflow template as social proof, and outputs 6 ready-to-use files.

---

## Input

The user provides:
* An Upwork job title, OR
* A full Upwork job description, OR
* A post caption/description of a pain point or problem they are facing.

---

## Step 1: Understand the Problem

Extract from the job post:
1. **Core Business Problem**: The root pain (lead leakage, manual bottleneck, slow turnaround, etc.)
2. **Workflow Category**: Functional type (Lead Intake, Email Triage, Cart Recovery, etc.)
3. **Tools & Platforms**: All mentioned apps (Gmail, Airtable, HubSpot, Shopify, OpenAI, etc.)
4. **Implicit Pain Points**: Unstated struggles (manual copying = lost revenue, delayed responses, burnout)

---

## Step 2: Rank Pain Points

Rank **Top 5 Pain Points** from highest to lowest financial/emotional resonance:
1. #1 (highest urgency)
2. #2
3. #3
4. #4
5. #5

Write each in the client's internal voice. No corporate filler. No em dashes.

---

## Step 3: Source a Workflow Template

**Two-tier approach:**

1. Check [`references/workflow_library.md`](./references/workflow_library.md) to identify the best-fit category (1-8).
2. Search the n8n.io public API for a real, free, *adjacent* template:
   - Use [`references/n8n_api_guide.md`](./references/n8n_api_guide.md) for API details
   - Search: `GET https://api.n8n.io/api/templates/search?search=<keywords>&rows=10`
   - Pick a **free** template (`price === 0` or `price === null`) that is thematically adjacent
   - Download the full workflow: `GET https://api.n8n.io/api/templates/workflows/<id>`
   - Extract the nested `workflow` object (contains `nodes`, `connections`, `settings`)

**Critical rule**: The sourced workflow represents a *previous client's* build (social proof). It must be adjacent, NOT identical to the current prospect's exact problem.

---

## Step 4: Invent a Prior Client Build

Create a realistic case study using the sourced template as the backbone:

* **Fictional Client**: Adjacent industry, distinct company type
* **Structure**:
  - **Previous Client Build**: 1-2 line description of who and what
  - **Problem**: 3-4 bullets of the bottleneck they faced
  - **Solution**: 4-5 bullets describing the n8n automation built (map to the sourced template's actual nodes)
  - **Result**: 1-2 bullets with quantifiable outcomes (e.g. "conversion from 2.1% to 11.4%, recovered $47k in 6 weeks")

Never mirror the real job post's exact client details.

---

## Step 5: Build the Tailored Plan

Construct a step-by-step **Build Plan** for the real job post. Each step must include:
- Step number and title
- Node type(s) used
- Trigger type
- Purpose (1 sentence)
- Key actions (3-4 bullets)

Use the ranked pain points from Step 2 as the foundation. Aim for 4-7 steps total.

---

## Step 6: Generate the n8n Workflow JSON

Take the downloaded template JSON from Step 3:
1. Rename the workflow to match the case study title
2. Update any sticky note descriptions to match the case study sections
3. Preserve all `connections`, `position` values, and credential placeholders
4. Save as `workflow.json`

---

## Required Outputs (6 Files)

The proposal now embeds an ROI statement and a **Risk Mitigation & Reliability Guarantee** card. The build‑plan page includes the **Caption (Cover Letter)** section with the Upwork macro text. A dedicated teleprompter page (`teleprompter.html`) provides an auto‑scrolling view for the Loom script.


### Output 1: `proposal.html`

Use [`references/html_templates/proposal_template.html`](./references/html_templates/proposal_template.html) as the structural reference.

**Light theme** with clean typography. Must contain these sections in order:

1. **Header**: "Toyo Ntewo." left, "Script" link right
2. **PROJECT label + Title**: Short, high-impact project name
3. **Summary Callout**: Blue-bordered box with "SUMMARY — OPEN WITH THIS" label. 2-3 sentence hook opening with #1 pain point.
4. **Observation**: Direct insight about the client's situation
5. **Tech Stack Pills**: Rounded pill badges for each tool
6. **CASE STUDY section**: Card with Previous Client Build / Problem / Solution / Result. Tech pills repeated below.
7. **FOR THE LOOM — N8N WALKTHROUGH**: Workflow title, description paragraph, "Open workflow in n8n →" green button, "Original template on n8n.io" secondary link
8. **FOR THE LOOM — BUILD PLAN**: "Open build plan ↗" button linking to `build-plan.html`, monospace note "Served at /build-plan.html on this same localhost."

### Output 2: `build-plan.html`

Use [`references/html_templates/build_plan_template.html`](./references/html_templates/build_plan_template.html) as the structural reference.

Separate page for Loom screen recording. Contains:
- Same header with back link to proposal.html
- "Build Plan" label + project title
- Tech stack pills
- Step cards with staggered reveal animations (each card: number badge, title, meta tags for node types, purpose, bullet list of actions)
- Connector lines between steps
- Footer with back-to-proposal button

### Output 3: `loom_script.txt`

Teleprompter script for 60-90 second Loom (~150-220 words). Off-camera voiceover style.

Structure:
1. **Quick Hook**: Open with their #1 pain point
2. **Past Work Tie-In**: 1-2 sentences referencing the case study
3. **Walkthrough**: "Let me show you the build plan" then walk through 3-4 key steps
4. **n8n Demo**: "And here's the actual workflow" referencing the n8n JSON
5. **Soft CTA**: Invite to discuss or test a prototype

### Output 4: `workflow.json`

The real, importable n8n workflow JSON from Step 6. This file can be pasted directly into an n8n canvas via Ctrl+V.

### Output 5: `upwork_macro.txt`

Ready-to-paste Upwork cover letter. Must include:

```
Summary: {summary_text}
Build plan for the Loom: http://localhost:8080/build-plan.html
n8n workflow for the Loom: {n8n_template_url}

Upwork application macro (paste this verbatim, replace {loom_url} after recording):

Hi, confident that I'm the best fit for your {project_type}. Just recorded a 2min video for you on how I'd do it:

{loom_url}

I've doubled the revenue of a 400k business with automations. I'm new to Upwork, but have worked with many big companies like Primal Queen and AG1, and I'm looking to flesh out my profile with some practical work experience.

I'm an AI developer with ~2 years of process automation experience. I am very familiar with both code & no-code. I also have extensive history in content creation, marketing and operations.

If you'd like specific examples of systems I've built and about...
```

### Output 6: `teleprompter.html`

A simple HTML page that displays the Loom teleprompter script with auto‑scrolling, adjustable speed, font size, and optional section highlighting. Served at `/teleprompter.html` on the same localhost.

---

## Strict Constraints

1. **Case Study Isolation**: The workflow JSON and case study represent a *previous client's* adjacent build (social proof), not the current prospect's exact problem.
2. **Upwork Character Limit**: Cover letter in upwork_macro.txt must be under 5,000 characters (target 1,000-1,500).
3. **No Em Dashes**: Never use `—` or `--` anywhere.
4. **No Corporate Filler**: No "delve", "seamlessly", "game-changer", "synergy".
5. **Light Theme**: All HTML uses the light/white theme from the templates. No dark theme.
6. **Free Templates Only**: Only source n8n templates where `price === 0` or `price === null`.
7. **Pain Point Ranking**: Top 5 must always be ranked most to least resonant.

---

## Serving the Output

After generating all 6 files, serve them locally:

```bash
cd <output_directory>
python3 -m http.server 8080
```

Then report:
- Script (teleprompter, off‑camera): http://localhost:8080
- Teleprompter view: http://localhost:8080/teleprompter.html
- Build plan (Loom visual): http://localhost:8080/build-plan.html
- n8n workflow for the Loom: link to the original n8n.io template
