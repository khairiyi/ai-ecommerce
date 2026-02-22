# Industry Knowledge Agent - Requirements

## Overview
Auto-fetch and research best practices; build and maintain a library by industry.

## Features

1. Auto-fetch and research best practices; build and maintain a library by industry.
2. Scope industries explicitly (e.g. home goods, apparel, electronics, beauty); prioritize a short list of verticals at launch.
3. U.S. localization and compliance: ad and claim rules (FTC, platform policies), industry-specific rules (health, supplements, kids). Tag "do / don't" by region and vertical so other agents don't generate non-compliant content.
4. Refresh and versioning: configurable re-fetch frequency per vertical; "knowledge version" or "as of" date for traceability.
5. Output schema: minimal, stable schema (e.g. best practices, tone, claims to avoid, trending angles) consumable by image-to-video and store-listing agents.
6. Optional real-time monitoring: industry reports, trends, consumer behavior shifts, competitor marketing strategies.
7. Recommendation engine: personalized suggestions per brand owner from the library (not only a static library).
8. **Daily newsletter generation**: Automatically create and distribute daily summaries including:
   - Major platforms' rules updates (Meta, TikTok, Amazon, etc.)
   - Macro regulations updates (FTC, FDA, etc.)
   - Latest market trends: trending keywords from Reddit, TikTok, Google
   - Competitor updates: pricing changes, product modifications, new launches
9. **Quick research for new customers**: When onboarding new business customers, quickly perform web search, parse website information, and create initial industry knowledge base for their product.
10. **Customer-specific knowledge storage**: Store unique customer requirements and product information in database for personalized recommendations.

## Integration Points
- Consumed by: Image-to-Video Agent, Store/Listing Management Agent
- Consumes: Web search APIs, platform APIs (Meta, TikTok, Amazon), regulatory sources


