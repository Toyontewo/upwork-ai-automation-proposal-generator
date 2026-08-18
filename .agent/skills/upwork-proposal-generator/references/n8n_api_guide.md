# n8n.io Template API Reference

This document provides the agent with the API endpoints and response format for searching and downloading free n8n workflow templates from the public n8n.io template library.

---

## Endpoints

### Search Templates

```
GET https://api.n8n.io/api/templates/search?search=<query>&rows=<count>&page=<page>
```

**Parameters**:
- `search` (required): URL-encoded search keywords (e.g., `shopify+abandoned+cart`, `lead+capture+crm`)
- `rows` (optional, default 10): Number of results per page
- `page` (optional, default 1): Page number

**Response Format** (JSON):
```json
{
  "totalWorkflows": 42,
  "workflows": [
    {
      "id": 8092,
      "name": "Automated Shopify Abandoned Cart Alerts",
      "totalViews": 502,
      "price": 0,
      "purchaseUrl": null,
      "user": {
        "name": "Author Name",
        "username": "author"
      },
      "description": "Full description text...",
      "createdAt": "2025-08-31T20:37:21.169Z",
      "nodes": [
        {
          "name": "n8n-nodes-base.httpRequest",
          "displayName": "HTTP Request"
        }
      ]
    }
  ]
}
```

### Get Full Workflow JSON

```
GET https://api.n8n.io/api/templates/workflows/<id>
```

**Parameters**:
- `id` (required): The numeric workflow ID from search results

**Response Format** (JSON):
```json
{
  "workflow": {
    "id": 8092,
    "name": "Workflow Name",
    "description": "...",
    "workflow": {
      "nodes": [...],
      "connections": {...},
      "settings": {...}
    },
    "nodes": [...],
    "user": {...}
  }
}
```

The actual importable n8n JSON is inside `response.workflow.workflow` (the nested `workflow` object containing `nodes`, `connections`, and `settings`).

---

## Filtering Logic

When selecting a template from search results:

1. **Prefer free templates**: Select workflows where `price === 0` or `price === null`. Skip any with a non-zero `price` or a `purchaseUrl`.
2. **Thematic adjacency**: The template should be *thematically adjacent* to the client's problem, NOT an exact match. This template represents a "previous client build" (social proof), so it should be from a related but distinct industry or use case.
3. **Relevance signals**: Prefer templates with:
   - Higher `totalViews` (more community validation)
   - Node types that overlap with the client's mentioned tools
   - Clear architecture described in the `description` field
4. **Avoid**: Templates that are clearly spam, have very low views, or whose descriptions are just marketing copy without technical substance.

---

## Search Strategy

Derive 2-3 search queries from the job post:

1. **Primary query**: The core workflow type (e.g., "lead capture crm", "abandoned cart recovery", "email triage")
2. **Tool-specific query**: Key platform + action (e.g., "shopify webhook openai", "gmail slack notification")
3. **Adjacent query**: A related but different use case to find social-proof templates (e.g., if the client needs "lead capture", search for "customer onboarding" or "appointment booking")

Use the **adjacent query** to find the template for the case study workflow JSON, since this represents a *previous client's* build, not the current prospect's exact need.

---

## Customizing the Downloaded JSON

After downloading the workflow JSON:

1. **Rename the workflow**: Change `name` to match the case study title (e.g., "Shopify Abandoned Cart Recovery with AI Personalization")
2. **Update sticky notes**: If the workflow has sticky note nodes, update their text to describe the build sections matching the case study
3. **Preserve node connections**: Do NOT modify the `connections` object or node `position` values
4. **Preserve credentials**: Do NOT add any credential values (they should remain empty/placeholder)
5. **Save as `workflow.json`**: The output file should be the full importable workflow JSON (the nested `workflow` object from the API response)
