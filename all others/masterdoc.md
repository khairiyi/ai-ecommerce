# Project Master Document: AI-Driven Sofa Manufacturing & Export Automation (China → USA)

**Date:** December 13, 2025  
**Project Lead:** [Your Name]  
**Objective:** To establish a fully automated, end-to-end workflow for sofa design, manufacturing, and export, leveraging leading AI tools and n8n orchestration to maximize efficiency and market fit in the US sector.

---

## 1. Executive Summary

This project aims to revolutionize the traditional furniture supply chain by integrating AI into every vertical. By connecting discrete AI agents via **n8n**, we will reduce the "Idea-to-Market" cycle time, minimize design risk through data-driven validation, and automate the administrative burden of cross-border e-commerce.

---

## 2. Technology Stack Architecture

### The Orchestrator (The Central Nervous System)

- **n8n:** The primary workflow automation tool. It will trigger events, pass data between AI agents, and manage API connections (Webhooks, HTTP Requests).

### The AI Agents (The Workers)

| Domain | Primary Tool | Fallback/Secondary | Function |
| :--- | :--- | :--- | :--- |
| **Trend Intelligence** | **Browse AI** + **Perplexity API** | Apify | Scraping competitor data & analyzing trends. |
| **Visual Design** | **Midjourney** (via API/Discord) | Stable Diffusion (ControlNet) | Generating photorealistic concepts. |
| **3D & Technical** | **Vizcom** / **CSM.ai** | Rodin | Turning sketches/images into 3D models/CAD. |
| **Market Testing** | **Buffer** / **Pinterest API** | OpenAI Vision | Posting to social & analyzing engagement. |
| **Product Photography** | **Flair.ai** | Booth.ai | Placing products in lifestyle scenes. |
| **Documentation** | **Claude 3.5 Sonnet** | GPT-4o | Writing listings, manuals, and compliance docs. |
| **Operations** | **Airtable** / **Google Sheets** | Monday.com | Central database for product lifecycle. |

---

## 3. Automated Workflow Phases

### Phase 1: Trend Intelligence & Idea Collection

**Goal:** Identify high-performing designs and gaps in the US market.

**Workflow:**
1. **n8n Trigger:** Scheduled (Weekly).
2. **Action:** Scrape "Best Sellers" from Amazon US (Home & Kitchen), Wayfair, and Pinterest Trends using **Browse AI** or **Apify**.
3. **Analysis:** Send data (images + text) to **GPT-4o Vision**.
4. **Prompt:** *"Analyze these top-selling sofas. Identify common features (fabric, color, arm style, dimensions) and output a design brief for a new contender."*
5. **Output:** Save structured "Design Briefs" to **Airtable**.

### Phase 2: Generative Design

**Goal:** Turn text briefs into visual concepts.

**Workflow:**
1. **n8n Trigger:** New record in Airtable ("Design Brief").
2. **Action:** Send prompt to **Midjourney** (via Discord Webhook or API wrapper).
3. **Refinement:** Use **Stable Diffusion** with ControlNet if specific structural constraints are needed (e.g., "Must keep this exact leg style").
4. **Output:** 4-8 High-fidelity variation images saved to Google Drive/Airtable.

### Phase 3: Social Validation (The "Digital Twin" Test)

**Goal:** Test market demand before manufacturing a single unit.

**Workflow:**
1. **n8n Trigger:** New Design Images generated.
2. **Action:** Auto-post images to **Pinterest** and **Instagram** (via Buffer/n8n nodes) with tags like #NewSofaDesign #InteriorTrends.
3. **Feedback Loop:** After 48 hours, n8n scrapes engagement metrics (Likes, Saves, Comments).
4. **Decision:** If `Engagement > Threshold`, mark status as "Approved for Production" in Airtable.

### Phase 4: Technical Translation (Design to Factory)

**Goal:** Convert pretty pictures into manufacturing specs.

**Workflow:**
1. **n8n Trigger:** Status changed to "Approved".
2. **Action:** Send winning image to **Vizcom** or **CSM.ai** to generate a rough 3D model/mesh.
3. **Documentation:** Send image + dimensions constraints to **Claude 3.5 Sonnet**.
4. **Prompt:** *"Act as a furniture engineer. Based on this image and standard US shipping constraints, generate a technical specification sheet (Frame material, Foam density, Fabric yardage)."*
5. **Human Step:** Factory engineer reviews the AI-generated spec sheet (Human-in-the-loop is crucial here).

### Phase 5: AI Product Photography (Virtual Photoshoot)

**Goal:** Create marketing assets without physical staging.

**Workflow:**
1. **n8n Trigger:** Final Production Design confirmed.
2. **Action:** Use **Flair.ai** or **Midjourney Inpainting**.
3. **Process:** Remove background of the sofa design → Place in 10 different US-style living room settings (Modern, Farmhouse, Industrial).
4. **Output:** 10+ High-res marketing images ready for e-commerce.

### Phase 6: E-Commerce Listing Creation

**Goal:** SEO-optimized listings for Amazon & TikTok Shop.

**Workflow:**
1. **n8n Trigger:** Marketing images ready.
2. **Action:** Send specs and images to **GPT-4o**.
3. **Prompt:** *"Create an Amazon Product Listing. Title (200 chars), 5 Bullet Points (SEO optimized for keywords: 'Sectional', 'Velvet', 'Pet-friendly'), and A+ Content description."*
4. **Action:** Generate JSON file formatted for Amazon Seller Central bulk upload.

### Phase 7: Logistics & Shipping Docs

**Goal:** Generate export paperwork.

**Workflow:**
1. **n8n Trigger:** Production Order placed.
2. **Action:** Generate Commercial Invoice and Packing List using **Google Docs** templating (populated by Airtable data).
3. **Compliance:** Check HS Codes via OpenAI to ensure correct US Tariff classification.

---

## 4. Implementation Roadmap

### Sprint 1: The Foundation (Weeks 1-2)

- [ ] Set up **n8n** (Self-hosted or Cloud).
- [ ] Build **Airtable** database schema (Products, Designs, Competitors).
- [ ] Configure **OpenAI API** and **Midjourney** access.

### Sprint 2: Design & Test Loop (Weeks 3-4)

- [ ] Build the "Trend Scraper" workflow.
- [ ] Build the "Social Media Posting" bot.
- [ ] Test the feedback loop (Can n8n read the likes?).

### Sprint 3: Production & Listing (Weeks 5-6)

- [ ] Integrate **Flair.ai** for photography.
- [ ] Build the Amazon Listing generator.
- [ ] Run a full end-to-end test with a dummy product.

---

## 5. Key Metrics for Success (KPIs)

- **Time-to-Market:** Target < 21 days from "Trend Spotted" to "Listing Live".
- **Design Success Rate:** % of designs that get >100 saves on Pinterest.
- **Listing Quality:** Amazon SEO score (via Helium 10 or similar).

---

## 6. Next Steps

1. **Confirm the Toolset:** Do you have subscriptions to the tools mentioned (Midjourney, ChatGPT Plus, n8n)?
2. **Define the Niche:** Are we focusing on Sectionals, Recliners, or Loveseats initially?
3. **Connect the APIs:** Start by getting your API keys for OpenAI and setting up your n8n instance.
