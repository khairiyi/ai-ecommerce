# Analytics Agent - Requirements

## Overview
Analyze data and extract insights; new product recommendations and product feedback; dashboard for stakeholders.

## Features

1. Analyze data and extract insights; new product recommendations and product feedback; dashboard for stakeholders.
2. **Live dashboard**: Generate and update live dashboard for stakeholders to monitor insights.
3. Defined data sources: platform APIs (Meta, TikTok, etc.), store (Amazon, Shopify), spreadsheets/CSVs. Start with one store + one social channel; expand in phases.
4. **Key metrics tracking**:
   - Ad spending across different platforms
   - Top performing videos
5. **Alert system**: Automated alerts for:
   - GMV dropping over X%
   - Conversion rate change in X channels
   - SKU inventories dropping low
   - Video/photo CTR dropped
6. Consistent recommendations format: e.g. trending keywords, underperforming SKUs, top creatives for dashboard and reports.
7. Scheduled dashboard refresh (e.g. daily) at first; real-time when pipelines and APIs allow.
8. Predictive analytics: predict future product performance and sales from historical data and competitor analysis.
9. A/B testing recommendations: suggest tests for ads and for product offerings and pricing.

## Integration Points
- Consumes: Platform APIs (Meta, TikTok), Store APIs (Amazon, Shopify), CSV/Spreadsheet data
- Outputs to: Dashboard, Alert system
