# Notion Database Mapping - Industry Knowledge Workflow

## Overview
This document describes the complete data mapping from the AI Agent output to the Notion database for the "Industry Knowledge - Quick Customer Onboarding" workflow.

## AI Agent Output Structure

The AI Agent extracts the following structured data from customer meeting notes:

```json
{
  "customerName": "string",
  "industry": "string (home goods, apparel, electronics, beauty, other)",
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
  "marketNotes": "string"
}
```

## Notion Database Properties Mapping

### Database Properties (propertiesUi)

| Notion Property | Type | Source Field | Expression |
|----------------|------|--------------|------------|
| Customer Name | Title | `customerName` | `={{ $('AI Agent').item.json.output.customerName }}` |
| Industry | Select | `industry` | `={{ $('AI Agent').item.json.output.industry }}` |
| Product Category | Rich Text | `productCategory` | `={{ $('AI Agent').item.json.output.productCategory }}` |
| Product Name | Rich Text | `productDetails.name` | `={{ $('AI Agent').item.json.output.productDetails.name }}` |
| Target Audience | Rich Text | `clientNeeds.targetAudience` | `={{ $('AI Agent').item.json.output.clientNeeds.targetAudience }}` |
| Key Features | Rich Text | `productDetails.keyFeatures[]` | `={{ $('AI Agent').item.json.output.productDetails.keyFeatures.join('\n• ') }}` |
| Primary Goals | Rich Text | `clientNeeds.primaryGoals[]` | `={{ $('AI Agent').item.json.output.clientNeeds.primaryGoals.join('\n• ') }}` |
| Pain Points | Rich Text | `clientNeeds.painPoints[]` | `={{ $('AI Agent').item.json.output.clientNeeds.painPoints.join('\n• ') }}` |
| Key Selling Points | Rich Text | `keySellingPoints[]` | `={{ $('AI Agent').item.json.output.keySellingPoints.join('\n• ') }}` |
| Competitors | Rich Text | `competitors[]` | `={{ $('AI Agent').item.json.output.competitors.length > 0 ? $('AI Agent').item.json.output.competitors.map(c => c.name + (c.url ? ' (' + c.url + ')' : '')).join('\n• ') : 'None identified' }}` |
| Market Notes | Rich Text | `marketNotes` | `={{ $('AI Agent').item.json.output.marketNotes }}` |
| Status | Status | Static | `Initial` |

### Page Content Blocks (blockUi)

The page content is organized into sections with headings:

1. **Product Details**
   - Heading 2: Product Name (`productDetails.name`)
   - Paragraph: Product Description (`productDetails.description`)
   - Heading 2: Key Features
   - Bullet list: Key Features (`productDetails.keyFeatures[]`)

2. **Client Needs**
   - Heading 2: Primary Goals
   - Bullet list: Primary Goals (`clientNeeds.primaryGoals[]`)
   - Heading 2: Target Audience
   - Paragraph: Target Audience (`clientNeeds.targetAudience`)
   - Heading 2: Pain Points
   - Bullet list: Pain Points (`clientNeeds.painPoints[]`)

3. **Market Intelligence**
   - Heading 2: Key Selling Points
   - Bullet list: Key Selling Points (`keySellingPoints[]`)
   - Heading 2: Competitors
   - Bullet list: Competitors (name and URL if available)
   - Heading 2: Market Notes
   - Paragraph: Market Notes (`marketNotes`)

## Notion Database Setup Requirements

To use this workflow, ensure your Notion database "Industry Library" has the following properties:

### Required Properties

1. **Customer Name** (Title) - Required, used as page title
2. **Industry** (Select) - Options: home goods, apparel, electronics, beauty, other
3. **Product Category** (Rich Text)
4. **Product Name** (Rich Text)
5. **Target Audience** (Rich Text)
6. **Key Features** (Rich Text)
7. **Primary Goals** (Rich Text)
8. **Pain Points** (Rich Text)
9. **Key Selling Points** (Rich Text)
10. **Competitors** (Rich Text)
11. **Market Notes** (Rich Text)
12. **Status** (Status) - Default: "Initial"

### Property Types Explained

- **Title**: Used for the primary identifier (Customer Name)
- **Select**: Dropdown with predefined options (Industry)
- **Rich Text**: Multi-line text fields for descriptions and lists
- **Status**: Status field with default value "Initial"

## Usage Notes

1. **Array Handling**: Arrays are joined with newlines and bullet points (`\n• `) for better readability in Notion
2. **Empty Arrays**: Competitors array shows "None identified" if empty
3. **Competitor URLs**: Competitor URLs are included in parentheses after the name if available
4. **Expression Syntax**: 
   - Properties use `$('AI Agent').item.json.output` to reference the AI Agent node
   - Blocks use `$json.output` which refers to the input from the previous node

## Testing

To test the mapping:
1. Import the updated workflow JSON into n8n
2. Ensure all Notion database properties exist
3. Run the workflow with test data
4. Verify all fields are populated correctly in Notion

## Troubleshooting

### Common Issues

1. **Missing Properties**: If a property doesn't exist in Notion, the workflow will fail. Create all required properties first.

2. **Expression Errors**: If expressions fail, check:
   - Node name matches exactly: `'AI Agent'` (case-sensitive)
   - Field paths match the AI output structure exactly
   - Array methods (`.join()`, `.map()`) are used correctly

3. **Empty Values**: If arrays are empty, they will show as empty strings or default messages. This is expected behavior.

4. **Special Characters**: Newline characters (`\n`) in expressions create line breaks in Notion rich text fields.
