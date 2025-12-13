# n8n Setup Structure: AI-Driven Sofa Manufacturing Automation

**Last Updated:** December 13, 2025  
**Purpose:** Step-by-step guide for setting up n8n workflows in the correct order.

---

## Overview: The Complete Flow

```
Step 1: Setup & Foundation
   ↓
Step 2: Trend Intelligence
   ↓
Step 3: Design Generation
   ↓
Step 4: Market Validation
   ↓
Step 5: Production Preparation
   ↓
Step 6: Marketing Assets
   ↓
Step 7: E-Commerce Integration
   ↓
Step 8: Logistics & Shipping
```

---

## Step 1: Setup & Foundation

**Goal:** Get n8n running and connect core services.

### Tasks:
- [ ] Install n8n (self-hosted or cloud)
- [ ] Create admin account
- [ ] Set up Airtable base with required tables
- [ ] Configure Google Drive folder structure
- [ ] Collect all API keys

### Workflows to Create:
- None yet (foundation only)

### Airtable Tables to Create:
- `Design Briefs` - Stores trend analysis results
- `Design Images` - Stores generated design images
- `Social Posts` - Tracks social media posts and engagement
- `Product Specs` - Technical specifications
- `Marketing Images` - Product photography
- `Amazon Listings` - E-commerce listing data
- `Shipping Docs` - Export documentation

---

## Step 2: Trend Intelligence

**Goal:** Automatically discover trending sofa designs in the US market.

### Workflows to Create:

#### Workflow 2.1: Weekly Trend Scraper
- **Trigger:** Schedule (Every Monday at 9 AM)
- **What it does:**
  1. Scrapes Amazon best sellers
  2. Scrapes Wayfair trending items
  3. Scrapes Pinterest trends
  4. Analyzes data with AI
  5. Creates design briefs in Airtable

#### Workflow 2.2: Competitor Analysis
- **Trigger:** Manual or scheduled
- **What it does:**
  1. Monitors competitor pricing
  2. Tracks competitor new releases
  3. Updates competitor database in Airtable

### Dependencies:
- Requires: Step 1 complete
- Creates: Records in `Design Briefs` table

---

## Step 3: Design Generation

**Goal:** Convert design briefs into visual concepts.

### Workflows to Create:

#### Workflow 3.1: Design Brief to Image Generator
- **Trigger:** New record in Airtable `Design Briefs` table
- **What it does:**
  1. Reads design brief from Airtable
  2. Formats prompt for Midjourney
  3. Generates 4-8 design variations
  4. Saves images to Google Drive
  5. Updates Airtable with image URLs

#### Workflow 3.2: Image Refinement
- **Trigger:** Manual or after initial generation
- **What it does:**
  1. Refines selected designs
  2. Applies specific style constraints
  3. Generates additional variations

### Dependencies:
- Requires: Step 2 (needs design briefs)
- Creates: Records in `Design Images` table

---

## Step 4: Market Validation

**Goal:** Test market demand before manufacturing.

### Workflows to Create:

#### Workflow 4.1: Social Media Poster
- **Trigger:** New design images ready in Airtable
- **What it does:**
  1. Formats images for social media
  2. Posts to Pinterest
  3. Posts to Instagram (via Buffer)
  4. Logs post IDs in Airtable

#### Workflow 4.2: Engagement Analyzer
- **Trigger:** 48 hours after social posts
- **What it does:**
  1. Scrapes engagement metrics (likes, saves, comments)
  2. Calculates total engagement score
  3. Compares to threshold (e.g., 100 saves)
  4. Updates Airtable status: "Approved" or "Rejected"

### Dependencies:
- Requires: Step 3 (needs design images)
- Updates: Status in `Design Briefs` table

---

## Step 5: Production Preparation

**Goal:** Convert approved designs into manufacturing specifications.

### Workflows to Create:

#### Workflow 5.1: Technical Spec Generator
- **Trigger:** Status changed to "Approved" in Airtable
- **What it does:**
  1. Gets approved design image
  2. Generates 3D model (Vizcom/CSM.ai)
  3. Creates technical spec sheet with AI
  4. Saves spec document to Google Drive
  5. Updates Airtable with spec sheet URL
  6. Notifies factory engineer for review

#### Workflow 5.2: 3D Model Converter
- **Trigger:** After spec generation
- **What it does:**
  1. Converts 3D model to CAD format
  2. Validates model dimensions
  3. Saves CAD files to Google Drive

### Dependencies:
- Requires: Step 4 (needs approved designs)
- Creates: Records in `Product Specs` table

---

## Step 6: Marketing Assets

**Goal:** Create professional product photography without physical staging.

### Workflows to Create:

#### Workflow 6.1: Product Photography Generator
- **Trigger:** Production design confirmed in Airtable
- **What it does:**
  1. Gets design image
  2. Removes background
  3. Places product in 10 different room styles:
     - Modern Living Room
     - Farmhouse Style
     - Industrial Loft
     - Minimalist
     - Coastal
     - Traditional
     - Mid-Century Modern
     - Scandinavian
     - Bohemian
     - Contemporary
  4. Saves all variations to Google Drive
  5. Updates Airtable with marketing image URLs

#### Workflow 6.2: Image Batch Processor
- **Trigger:** After photography generation
- **What it does:**
  1. Optimizes images for web
  2. Creates thumbnails
  3. Generates image variants for different platforms

### Dependencies:
- Requires: Step 5 (needs confirmed production design)
- Creates: Records in `Marketing Images` table

---

## Step 7: E-Commerce Integration

**Goal:** Create SEO-optimized listings for Amazon and TikTok Shop.

### Workflows to Create:

#### Workflow 7.1: Amazon Listing Creator
- **Trigger:** Marketing images ready in Airtable
- **What it does:**
  1. Gets product specs and marketing images
  2. Generates SEO-optimized title, bullets, and description with AI
  3. Formats data for Amazon Seller Central
  4. Saves listing data to Google Sheets
  5. Creates listing via Amazon SP-API
  6. Updates Airtable with Amazon ASIN

#### Workflow 7.2: TikTok Shop Integration
- **Trigger:** After Amazon listing created
- **What it does:**
  1. Adapts listing for TikTok Shop format
  2. Creates TikTok Shop listing
  3. Updates Airtable with TikTok product ID

### Dependencies:
- Requires: Step 6 (needs marketing images)
- Creates: Records in `Amazon Listings` table

---

## Step 8: Logistics & Shipping

**Goal:** Automate export documentation and compliance.

### Workflows to Create:

#### Workflow 8.1: Shipping Doc Generator
- **Trigger:** Production order placed in Airtable
- **What it does:**
  1. Gets product and order details
  2. Checks HS Code classification with AI
  3. Generates Commercial Invoice
  4. Generates Packing List
  5. Saves documents to Google Drive
  6. Sends documents to shipping department
  7. Updates Airtable with document URLs

#### Workflow 8.2: Compliance Checker
- **Trigger:** Before shipping doc generation
- **What it does:**
  1. Validates HS Code
  2. Checks US import regulations
  3. Verifies product compliance
  4. Flags any issues for review

### Dependencies:
- Requires: Step 7 (needs production orders)
- Creates: Records in `Shipping Docs` table

---

## Implementation Order

### Phase 1: Foundation (Week 1)
1. Complete Step 1: Setup & Foundation
2. Build Workflow 2.1: Weekly Trend Scraper
3. Test with sample data

### Phase 2: Design Loop (Week 2)
4. Build Workflow 3.1: Design Brief to Image Generator
5. Build Workflow 4.1: Social Media Poster
6. Build Workflow 4.2: Engagement Analyzer
7. Test end-to-end: Trend → Design → Social → Analysis

### Phase 3: Production Pipeline (Week 3)
8. Build Workflow 5.1: Technical Spec Generator
9. Build Workflow 6.1: Product Photography Generator
10. Test production workflow

### Phase 4: E-Commerce & Logistics (Week 4)
11. Build Workflow 7.1: Amazon Listing Creator
12. Build Workflow 8.1: Shipping Doc Generator
13. Run full end-to-end test with one product

---

## Workflow Summary Table

| Step | Workflow Name | Trigger | Creates/Updates |
|------|--------------|---------|-----------------|
| 2 | Weekly Trend Scraper | Schedule (Weekly) | `Design Briefs` table |
| 2 | Competitor Analysis | Schedule/Manual | Competitor data |
| 3 | Design Brief to Image | Airtable trigger | `Design Images` table |
| 3 | Image Refinement | Manual | `Design Images` table |
| 4 | Social Media Poster | Airtable trigger | `Social Posts` table |
| 4 | Engagement Analyzer | Schedule (48h delay) | `Design Briefs` status |
| 5 | Technical Spec Generator | Airtable trigger | `Product Specs` table |
| 5 | 3D Model Converter | Airtable trigger | CAD files in Drive |
| 6 | Product Photography | Airtable trigger | `Marketing Images` table |
| 6 | Image Batch Processor | Airtable trigger | Optimized images |
| 7 | Amazon Listing Creator | Airtable trigger | `Amazon Listings` table |
| 7 | TikTok Shop Integration | Airtable trigger | TikTok listings |
| 8 | Shipping Doc Generator | Airtable trigger | `Shipping Docs` table |
| 8 | Compliance Checker | Airtable trigger | Compliance status |

---

## Key Connections Between Workflows

```
Trend Scraper (Step 2)
   → Creates Design Briefs
   ↓
Design Generator (Step 3)
   → Creates Design Images
   ↓
Social Media Poster (Step 4)
   → Creates Social Posts
   ↓
Engagement Analyzer (Step 4)
   → Updates Design Briefs status to "Approved"
   ↓
Technical Spec Generator (Step 5)
   → Creates Product Specs
   ↓
Product Photography (Step 6)
   → Creates Marketing Images
   ↓
Amazon Listing Creator (Step 7)
   → Creates Amazon Listings
   ↓
Shipping Doc Generator (Step 8)
   → Creates Shipping Docs
```

---

## Next Steps

1. **Start with Step 1** - Set up n8n and Airtable
2. **Build workflows in order** - Follow the implementation phases
3. **Test each workflow** - Before moving to the next step
4. **Connect workflows** - Link them via Airtable triggers
5. **Monitor and refine** - Adjust based on real-world performance
