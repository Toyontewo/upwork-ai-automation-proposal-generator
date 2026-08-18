# n8n Automation Reference Library

This reference library contains 8 foundational n8n workflow categories. Use these in Step 3 to identify the correct workflow *category* for the case study.

> **Two-tier sourcing strategy:**
> 1. **Local library (this file):** Use to identify the correct category and understand the typical architecture, node types, and metrics for the case study narrative.
> 2. **Live n8n.io API (see [`n8n_api_guide.md`](./n8n_api_guide.md)):** Search for a real, free workflow template that matches the identified category. Download its JSON to include as `workflow.json` in the output. This gives the prospect a real, importable n8n workflow they can open alongside the Loom recording.

---

## Category 1: Lead Intake & CRM Sync

* **Workflow Name**: Automated Lead Qualification & Multi-Channel CRM Sync
* **Typical Triggers**: Webhook (Typeform, Webflow, Tally, Custom Form), Inbound Webhook
* **Core Nodes Used**:
  * `n8n-nodes-base.webhook` (Form Trigger)
  * `n8n-nodes-base.openAi` (GPT-4o Lead Scoring & ICP Matching)
  * `n8n-nodes-base.hubspot` / `n8n-nodes-base.airtable` (CRM Record Creation & Update)
  * `n8n-nodes-base.slack` (Sales Rep Instant Notification)
* **Architecture Flow**:
  1. Captures form submission payload via Webhook.
  2. Passes lead details (company size, budget, problem statement) to GPT-4o to compute an ICP (Ideal Customer Profile) match score (0–100) and draft a 2-sentence summary.
  3. Checks CRM (HubSpot/Airtable) for existing contact by email; updates if existing, creates if new.
  4. If ICP Score > 70, posts high-priority alert in Slack `#sales-hot-leads` with direct CRM link and assigned rep tag.
* **Key Metrics / Impact**:
  * Reduced lead response time from hours to under 60 seconds.
  * Eliminated manual data entry across marketing forms and sales CRM.

---

## Category 2: Email Triage & Auto-Response

* **Workflow Name**: Intelligent Inbox Triage & Draft Response System
* **Typical Triggers**: `n8n-nodes-base.gmailTrigger` or `n8n-nodes-base.emailReadImap`
* **Core Nodes Used**:
  * `n8n-nodes-base.gmail` (Message Fetcher & Draft Creator)
  * `n8n-nodes-base.openAi` (Intent Classification & Reply Generation)
  * `n8n-nodes-base.switch` (Category Router: Sales, Support, Billing, Spam)
  * `n8n-nodes-base.slack` (Team Notification for High-Priority Emails)
* **Architecture Flow**:
  1. Triggers on incoming email in shared inbox.
  2. AI analyzes email intent, urgency, and customer sentiment.
  3. Switch node routes email based on classification:
     * **Billing**: Creates ticket in accounting system & alerts finance channel.
     * **Sales Inquiry**: Generates contextual draft reply in Gmail drafts folder for rep review.
     * **General Info**: Sends automated helpful response with knowledge base links.
  4. Tags email in Gmail with custom label (`AI-Triaged/Sales`, `AI-Triaged/Pending-Review`).
* **Key Metrics / Impact**:
  * Cut daily email processing time by 75%.
  * Ensured zero critical client inquiries were missed or delayed.

---

## Category 3: Appointment Scheduling & Calendar Management

* **Workflow Name**: High-Touch Booking Triage & Pre-Meeting Brief Generator
* **Typical Triggers**: Calendly Webhook / SavvyCal Webhook
* **Core Nodes Used**:
  * `n8n-nodes-base.webhook` (Booking Event)
  * `n8n-nodes-base.googleCalendar` (Event Detail Fetcher)
  * `n8n-nodes-base.openAi` (Dossier & Brief Generator)
  * `n8n-nodes-base.twilio` / `n8n-nodes-base.sendGrid` (SMS / Email Reminders)
* **Architecture Flow**:
  1. Listens for new calendar booking event via webhook.
  2. Extracts attendee domain and queries web search / enrichment API for company overview and recent news.
  3. GPT-4o generates a 1-page pre-meeting briefing document for the meeting host.
  4. Updates Google Calendar event description with the briefing note.
  5. Schedules automated SMS reminder 2 hours prior to meeting via Twilio.
* **Key Metrics / Impact**:
  * Reduced meeting no-show rate from 18% to under 4%.
  * Saved executives 30 minutes of prep time per sales call.

---

## Category 4: Data Enrichment & Web Scraping

* **Workflow Name**: Automated Company Intelligence & Lead Enrichment Pipeline
* **Typical Triggers**: Cron Schedule (Daily batch) or Webhook Trigger
* **Core Nodes Used**:
  * `n8n-nodes-base.postgres` / `n8n-nodes-base.googleSheets` (Un-enriched Records Input)
  * `n8n-nodes-base.httpRequest` (Serper API / Perplexity API / Scrapingbee)
  * `n8n-nodes-base.openAi` (Structured JSON Extraction)
  * `n8n-nodes-base.postgres` (Upsert Enriched Records)
* **Architecture Flow**:
  1. Fetches list of target domains needing enrichment from database or spreadsheet.
  2. Calls web search / scraping endpoints to extract tech stack, executive team, headcount, and recent funding/news.
  3. Uses OpenAI Structured Outputs (JSON Schema) to format extracted data into standardized fields.
  4. Upserts enriched profile back into database and flags qualified prospects for outreach.
* **Key Metrics / Impact**:
  * Enriched 5,000+ domain profiles per week automatically.
  * Provided sales reps with rich context without manual prospect research.

---

## Category 5: Invoice Processing & Reporting Automation

* **Workflow Name**: Multi-Format Invoice Extraction & ERP Sync
* **Typical Triggers**: Gmail Attachment Trigger / Cloud Storage File Upload (Google Drive / S3)
* **Core Nodes Used**:
  * `n8n-nodes-base.googleDriveTrigger` / `n8n-nodes-base.gmail`
  * `n8n-nodes-base.readBinaryFile` (PDF Reader)
  * `n8n-nodes-base.openAi` (Vision / Document Parsing)
  * `n8n-nodes-base.quickbooks` / `n8n-nodes-base.xero` / `n8n-nodes-base.postgres` (Accounting System)
* **Architecture Flow**:
  1. Detects new PDF invoice added to folder or received via email.
  2. Sends binary PDF document to vision AI model to extract line items, vendor name, invoice date, total amount, tax, and payment terms.
  3. Validates extracted numbers against Purchase Orders in accounting database.
  4. Creates draft bill in Quickbooks/Xero and routes for approval via Slack interactive button if amount exceeds $1,000.
* **Key Metrics / Impact**:
  * Reduced invoice processing cost from $12/invoice to under $0.15/invoice.
  * Eliminated manual data entry errors and late payment penalties.

---

## Category 6: Customer Support Ticket Routing & Triage

* **Workflow Name**: Autonomous Support Ticket Classification & Escalation Engine
* **Typical Triggers**: Zendesk Webhook / Freshdesk Webhook / Support Email Trigger
* **Core Nodes Used**:
  * `n8n-nodes-base.webhook` (Ticket Created)
  * `n8n-nodes-base.openAi` (Urgency, Category, Sentiment Classifier)
  * `n8n-nodes-base.zendesk` (Ticket Tagging & Assignee Router)
  * `n8n-nodes-base.slack` (Urgent Escalation Channel)
* **Architecture Flow**:
  1. Triggers instantly upon creation of new support ticket.
  2. Evaluates customer message sentiment (frustrated, neutral, satisfied) and issue category (bug, feature request, account access, billing).
  3. Automatically assigns priority tag (`P1-Critical`, `P2-High`, `P3-Normal`) and assigns to specialized agent group.
  4. For `P1-Critical` tickets from enterprise clients, triggers immediate Slack notification to on-call support team.
* **Key Metrics / Impact**:
  * Reduced average first-response time for critical bugs from 45 minutes to 2 minutes.
  * Improved first-contact resolution rate by 35%.

---

## Category 7: Social Media & Content Pipeline Automation

* **Workflow Name**: Multi-Channel Content Repurposing & Publishing Pipeline
* **Typical Triggers**: Notion Database Trigger / RSS Feed Trigger / Webhook
* **Core Nodes Used**:
  * `n8n-nodes-base.notionTrigger` (Draft Approved Status)
  * `n8n-nodes-base.openAi` (Content Formatting per Platform Spec)
  * `n8n-nodes-base.httpRequest` (LinkedIn API / Twitter API / Buffer API)
  * `n8n-nodes-base.notion` (Status Update to Published)
* **Architecture Flow**:
  1. Detects content piece marked as "Approved" in Notion content database.
  2. Generates tailored variations: punchy thread for X/Twitter, detailed post for LinkedIn, newsletter snippet for Substack/ConvertKit.
  3. Schedules posts across platforms using social APIs or buffer webhook.
  4. Updates Notion record with published post URLs and scheduled timestamps.
* **Key Metrics / Impact**:
  * Saved content team 10+ hours per week on manual reformatting and distribution.
  * Multiplied content reach across 4 platforms from a single source document.

---

## Category 8: RAG & AI Chatbot / Knowledge Base Systems

* **Workflow Name**: Enterprise Knowledge Base RAG Assistant
* **Typical Triggers**: Webhook / Slack App Event / WhatsApp Webhook
* **Core Nodes Used**:
  * `n8n-nodes-base.slack` / `n8n-nodes-base.webhook` (User Query)
  * `n8n-nodes-base.embeddingsOpenAi` (Query Vectorizer)
  * `@n8n/n8n-nodes-langchain.vectorStorePinecone` / `qdrant` (Similarity Search)
  * `@n8n/n8n-nodes-langchain.chainRetrievalQa` (Contextual Answer Engine)
* **Architecture Flow**:
  1. Receives question from employee or client via Slack/Web widget.
  2. Converts question into vector embeddings and queries Pinecone/Qdrant vector database containing internal SOPs, product documentation, and policy PDFs.
  3. Retrieves top 3 relevant context chunks and passes to GPT-4o with strict grounding prompt ("Answer strictly using provided context").
  4. Returns concise, cited answer to user with direct links to internal source documents.
* **Key Metrics / Impact**:
  * Answered 80%+ of internal staff SOP questions instantly without manager intervention.
  * Eliminated outdated advice by centralizing knowledge retrieval around live docs.
