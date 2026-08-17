# Upwork AI Automation Proposal Generator Skill

An agent skill and marketplace catalog for generating complete, ready-to-send proposal packages for **Upwork AI automation gigs** (n8n, Make, Zapier workflow builds).

Created by **Toyo Ntewo**.

---

## Features

- **Automated Job Analysis**: Extracts core bottlenecks, underlying systems, tools/platforms, and implicit client pain points from raw Upwork job posts.
- **Ranked Pain Points**: Formulates the top 5 client pain points, strictly ordered by emotional and financial impact.
- **Workflow Template Sourcing**: Sourced from a local library of 8 core n8n automation categories (Lead Intake, Email Triage, Booking, Scraping, Invoicing, Support, Content, RAG/Chatbots) or live adjacent `n8n.io` workflows.
- **Plausible Case Studies**: Generates believable prior client builds demonstrating technical competence without mirroring the client's exact post.
- **Tailored Build Plan**: Step-by-step architectural breakdown designed specifically for the target job.
- **Dual Output**:
  1. **HTML Proposal (`proposal.html`)**: Clean visual layout with Project Title, Summary, Case Study, Cover Letter (respecting Upwork's character limits), and Build Plan diagram.
  2. **Loom Script (`loom_script.txt`)**: 60-90 second off-camera teleprompter script for screen-recording proposal walkthroughs.

---

## Installation & Usage

### Installing via Agent Marketplace

You can install this skill package in your agent workspace by using the `marketplace.json` manifest:

```json
{
  "skills": [
    "upwork-ai-automation-proposal-generator"
  ]
}
```

### Manual Directory Structure

```text
.agent/
├── marketplace.json
└── skills/
    └── upwork-proposal-generator/
        ├── SKILL.md
        └── references/
            └── workflow_library.md
```

---

## License

MIT License
