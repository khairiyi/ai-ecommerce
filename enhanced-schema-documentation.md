# Enhanced Schema Documentation - Industry Knowledge

## Overview

The Industry Knowledge schema has been enhanced to include comprehensive fields for content strategy, compliance, brand guidelines, and a catch-all field for additional information. This ensures all relevant industry knowledge is captured and can be used by downstream agents (Image-to-Video Agent, Store/Listing Management Agent).

---

## Complete Schema Structure

```json
{
  "customerName": "string",
  "industry": "string (e.g., home goods, apparel, electronics, beauty, other)",
  "productCategory": "string",
  "productDetails": {
    "name": "string",
    "description": "string",
    "keyFeatures": ["string"]
  },
  "clientNeeds": {
    "primaryGoals": ["string"],
    "targetAudience": "string",
    "painPoints": ["string"]
  },
  "competitors": [
    {
      "name": "string",
      "url": "string"
    }
  ],
  "keySellingPoints": ["string"],
  "marketNotes": "string",
  "contentStrategy": {
    "videoStyle": "string (e.g., lifestyle, product-focused, tutorial, testimonial, behind-the-scenes, cinematic, minimalist, energetic, professional)",
    "contentTone": "string (e.g., professional, casual, friendly, authoritative, playful, sophisticated, aspirational)",
    "brandVoice": "string",
    "platformRequirements": {
      "amazon": "string",
      "tiktok": "string",
      "instagram": "string",
      "facebook": "string",
      "youtube": "string",
      "other": "string"
    },
    "trendingAngles": ["string"],
    "marketingKeywords": ["string"]
  },
  "compliance": {
    "dos": ["string"],
    "donts": ["string"],
    "claimsToAvoid": ["string"],
    "regulatoryNotes": "string",
    "platformSpecificRules": {
      "meta": "string",
      "tiktok": "string",
      "amazon": "string",
      "ftc": "string",
      "fda": "string",
      "other": "string"
    }
  },
  "brandGuidelines": {
    "colorPalette": ["string"],
    "visualStyle": "string",
    "messagingGuidelines": "string",
    "contentPreferences": ["string"]
  },
  "additionalInfo": "string (any other relevant information that doesn't fit into the above structured fields)"
}
```

---

## New Fields Added

### 1. **contentStrategy** (Object)

Contains all content creation and marketing strategy information:

- **videoStyle**: Preferred video style for content creation (used by Image-to-Video Agent)
  - Examples: lifestyle, product-focused, tutorial, testimonial, behind-the-scenes, cinematic, minimalist, energetic, professional
- **contentTone**: Desired tone for all content
  - Examples: professional, casual, friendly, authoritative, playful, sophisticated, aspirational
- **brandVoice**: Description of the brand's voice and personality
- **platformRequirements**: Platform-specific content requirements
  - Keys: amazon, tiktok, instagram, facebook, youtube, other
- **trendingAngles**: Array of trending marketing angles or approaches
- **marketingKeywords**: Array of important marketing keywords for SEO and content

### 2. **compliance** (Object)

Contains compliance and regulatory information to prevent non-compliant content:

- **dos**: Array of things that should be done (compliant practices)
- **donts**: Array of things that should NOT be done (non-compliant practices)
- **claimsToAvoid**: Array of claims or statements to avoid (e.g., health claims, unsubstantiated claims)
- **regulatoryNotes**: General regulatory notes and guidelines
- **platformSpecificRules**: Platform-specific compliance rules
  - Keys: meta, tiktok, amazon, ftc, fda, other

### 3. **brandGuidelines** (Object)

Contains brand identity and visual guidelines:

- **colorPalette**: Array of brand colors (hex codes or color names)
- **visualStyle**: Description of preferred visual style
- **messagingGuidelines**: Guidelines for messaging and copy
- **contentPreferences**: Array of content preferences or requirements

### 4. **additionalInfo** (String)

Catch-all field for any information that doesn't fit into the structured fields above. This ensures no important information is lost.

---

## Notion Database Mapping

### New Properties Added

The following properties have been added to the Notion database:

| Notion Property | Type | Source Field | Expression |
|----------------|------|--------------|------------|
| Video Style | Rich Text | `contentStrategy.videoStyle` | `$json.output.contentStrategy.videoStyle` |
| Content Tone | Rich Text | `contentStrategy.contentTone` | `$json.output.contentStrategy.contentTone` |
| Brand Voice | Rich Text | `contentStrategy.brandVoice` | `$json.output.contentStrategy.brandVoice` |
| Trending Angles | Rich Text | `contentStrategy.trendingAngles[]` | `$json.output.contentStrategy.trendingAngles.join('\n• ')` |
| Marketing Keywords | Rich Text | `contentStrategy.marketingKeywords[]` | `$json.output.contentStrategy.marketingKeywords.join(', ')` |
| Compliance Do's | Rich Text | `compliance.dos[]` | `$json.output.compliance.dos.join('\n• ')` |
| Compliance Don'ts | Rich Text | `compliance.donts[]` | `$json.output.compliance.donts.join('\n• ')` |
| Claims to Avoid | Rich Text | `compliance.claimsToAvoid[]` | `$json.output.compliance.claimsToAvoid.join('\n• ')` |
| Regulatory Notes | Rich Text | `compliance.regulatoryNotes` | `$json.output.compliance.regulatoryNotes` |
| Additional Info | Rich Text | `additionalInfo` | `$json.output.additionalInfo` |

### New Page Content Sections

The Notion page content now includes three new sections:

1. **Content Strategy**
   - Video Style
   - Content Tone
   - Brand Voice
   - Platform Requirements (JSON formatted)
   - Trending Angles
   - Marketing Keywords

2. **Compliance & Regulatory**
   - Do's
   - Don'ts
   - Claims to Avoid
   - Regulatory Notes
   - Platform-Specific Rules (JSON formatted)

3. **Brand Guidelines**
   - Complete brand guidelines object (JSON formatted)

4. **Additional Information**
   - Any other relevant information

---

## Usage by Downstream Agents

### Image-to-Video Agent

Uses:
- `contentStrategy.videoStyle` - To determine video style
- `contentStrategy.contentTone` - To set appropriate tone
- `brandGuidelines.colorPalette` - For color consistency
- `brandGuidelines.visualStyle` - For visual consistency
- `compliance.donts` and `compliance.claimsToAvoid` - To avoid non-compliant content

### Store/Listing Management Agent

Uses:
- `contentStrategy.marketingKeywords` - For SEO and listing optimization
- `contentStrategy.platformRequirements` - For platform-specific optimizations
- `compliance.dos` and `compliance.donts` - To ensure compliant listings
- `compliance.platformSpecificRules` - For platform-specific compliance
- `brandGuidelines.messagingGuidelines` - For consistent messaging

---

## AI Agent Extraction Guidelines

The AI Agent is instructed to extract:

1. **Video Style**: Infer from context or use common styles (lifestyle, product-focused, tutorial, testimonial, behind-the-scenes, cinematic, minimalist, energetic, professional)

2. **Content Tone**: Infer from context (professional, casual, friendly, authoritative, playful, sophisticated, aspirational)

3. **Platform Requirements**: Extract requirements mentioned for Amazon, TikTok, Instagram, Facebook, YouTube

4. **Compliance Information**: Extract do's, don'ts, claims to avoid, regulatory notes, and platform-specific rules (Meta, TikTok, Amazon, FTC, FDA)

5. **Brand Guidelines**: Extract color palette, visual style preferences, messaging guidelines, content preferences

6. **Additional Info**: Place any information that doesn't fit into structured fields here

---

## Update Flow Integration

The Update flow (with Perplexity search) now also searches for and updates:
- Latest video content trends
- Content strategy best practices
- Compliance rule updates (FTC, FDA, platform policies)
- Brand guideline updates
- All new fields are included in the update

---

## Notion Database Setup

Ensure your Notion database "Industry Library" has these additional properties:

- [ ] **Video Style** (Rich Text)
- [ ] **Content Tone** (Rich Text)
- [ ] **Brand Voice** (Rich Text)
- [ ] **Trending Angles** (Rich Text)
- [ ] **Marketing Keywords** (Rich Text)
- [ ] **Compliance Do's** (Rich Text)
- [ ] **Compliance Don'ts** (Rich Text)
- [ ] **Claims to Avoid** (Rich Text)
- [ ] **Regulatory Notes** (Rich Text)
- [ ] **Additional Info** (Rich Text)

---

## Files Updated

1. **Workflow JSON**: `Industry Knowledge - Quick Customer Onboarding (1).json`
   - Updated both Structured Output Parsers (Create and Update)
   - Updated AI Agent prompts
   - Updated Notion Create node properties and blocks
   - Updated Notion Update node properties and blocks

2. **Documentation**: This file (`enhanced-schema-documentation.md`)
