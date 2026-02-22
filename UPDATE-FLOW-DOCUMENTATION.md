# Update Flow – Industry Knowledge Quick Customer Onboarding

## Overview

When a client **already has a row** in the Industry Library database, the workflow now:

1. **Detects** existing data (by Customer Name from “Customer Details”).
2. **Runs a Perplexity web search** for latest market trends, competitors, and selling points.
3. **Merges** that research with the existing Notion data via an AI agent.
4. **Updates** the same Notion database row and page with the enriched content.

---

## Flow Summary

```
Customer Details (docId, customerName)
    → Get many database pages (filter: Customer Name contains customerName)
    → Route Create vs Update (Code)
         • 0 results → createNew: true (docId, customerName) → Create path
         • 1+ results → createNew: false + Notion page item(s) → Update path

Create path:
    → Switch (Create New Account) → Get a document → AI Agent → Create a database page1

Update path:
    → Switch (Update Account) → Update context (Set)
         • pageId, customerName, existingDataText (from Notion page)
         ├→ Merge (input 1)
         └→ AI Agent1
              • Prompt: existing data + “use Perplexity tool, then output updated JSON”
              • Tool: Message a model in Perplexity (sonar-deep-research)
              • Output: Structured Output Parser (Update) → same schema as Create
              └→ Merge (input 2)
    → Merge (combine by position) → Update a database page
```

---

## Nodes Added or Changed

### 1. **Route Create vs Update** (Code)

- **After:** Get many database pages  
- **Logic:**
  - If Get many returns **0 items**: output **one** item with `createNew: true`, `docId`, `customerName` (from Customer Details) so the Create path runs.
  - If Get many returns **1+ items**: pass each Notion page item with `createNew: false` so the Update path runs (once per page).

### 2. **Switch**

- **Input:** From Route Create vs Update.
- **Rules:**
  - **Create New Account:** `createNew === true` → Get a document (then doc → AI Agent → Create page).
  - **Update Account:** `createNew === false` → Update context (then Perplexity + AI Agent1 → Merge → Update page).

### 3. **Update context** (Set)

- **Input:** One Notion page item from Switch (Update Account).
- **Outputs:** Same item with:
  - `pageId`: `$json.id` (Notion page ID for the update).
  - `customerName`: from Notion title (supports `Customer Name` and `Customer Name|title`).
  - `existingDataText`: stringified Notion properties (so the AI can read existing data).
- **Connections:** One branch to **Merge** (input 1), one branch to **AI Agent1**.

### 4. **AI Agent1** (Update / enrich)

- **Input:** From Update context (`pageId`, `customerName`, `existingDataText`).
- **Prompt:** Instructs the agent to:
  - Use the **Perplexity web search tool** for latest market trends, competitors, key selling points for this customer/industry.
  - Merge that research with the existing Notion data.
  - Output **one** JSON object in the **same schema** as the Create flow (customerName, industry, productDetails, clientNeeds, competitors, keySellingPoints, marketNotes, etc.).
- **Tool:** Message a model in Perplexity (e.g. sonar-deep-research).
- **Output:** Parsed via **Structured Output Parser (Update)** (same schema as the main Create agent).

### 5. **Structured Output Parser (Update)**

- Same JSON schema as the Create flow.
- Connected to AI Agent1 as `ai_outputParser`.

### 6. **Merge**

- **Mode:** Combine by position.
- **Input 1:** Update context (so each item has `pageId`, `customerName`, `existingDataText`).
- **Input 2:** AI Agent1 (each item has `output` = the updated structured object).
- **Output:** One item per pair with `pageId` + `output` (and any other fields from both inputs).

### 7. **Update a database page**

- **Input:** From Merge.
- **Page ID:** `$json.pageId`.
- **Properties:** Same mapping as Create, but from `$json.output` (e.g. `$json.output.customerName`, `$json.output.clientNeeds.primaryGoals.join('\n• ')`, etc.).
- **Status:** Set to **Updated** (vs “Initial” on Create).
- **Blocks (blockUi):** Same structure as Create (Product Details, Client Needs, Market Intelligence), using `$json.output.*` so the page body is refreshed with the enriched content.

---

## Data Mapping (Update path)

Update uses the **same** field mapping as Create; the only difference is the **source** of the data:

- **Create:** `$('AI Agent').item.json.output.*`
- **Update:** `$json.output.*` (after Merge), with `pageId` from `$json.pageId`.

So all properties and blocks (Product Details, Key Features, Primary Goals, Pain Points, Key Selling Points, Competitors, Market Notes) are updated from the AI Agent1 output.

---

## Perplexity Role

- **Node:** Message a model in Perplexity (used as an **AI tool** for AI Agent1).
- **Behavior:** The agent is instructed to call this tool to search for:
  - Latest market trends for the customer/industry  
  - Competitors  
  - Key selling points and any relevant recent news  
- The agent then merges this with the existing Notion data and returns the single updated JSON used to update the row and page.

---

## How to Test

1. **Create path:** Use a `customerName` that does **not** exist in the Industry Library → workflow should create a new page (existing behavior).
2. **Update path:** Use a `customerName` that **does** exist in the Industry Library → workflow should:
   - Find the page(s),
   - Run Perplexity (via the tool),
   - Enrich with new research,
   - Update that row’s properties and page content.

---

## File Updated

- **Workflow JSON:** `Industry Knowledge - Quick Customer Onboarding (1).json` (in your Downloads folder or wherever you keep it).

Re-import this JSON into n8n to use the new Create vs Update flow with Perplexity and full Notion row + page update.
