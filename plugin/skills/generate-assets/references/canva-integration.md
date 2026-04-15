# Canva Integration Reference

How `generate-assets` works with Canva today, and what the Canva Connect API integration will enable.

---

## Current State — Manual Canva Workflow

The `generate-assets` skill currently outputs **Canva-ready design specifications** — structured briefs with exact dimensions, layout descriptions, text layer copy, color values, and Canva template recommendations.

A designer takes each spec and:
1. Opens Canva and searches for the recommended template type
2. Sets the canvas to the exact dimensions specified
3. Applies brand colors from the brand kit (or manually from the hex values in the spec)
4. Places the key visual (product image, lifestyle photo, etc.) as described in the Visual Direction section
5. Adds text layers with the copy and styling from the Text Layers table
6. Exports using the format and quality settings from `references/asset-specs.md`

This workflow is fully functional and produces campaign-ready assets today. The specs are written to eliminate designer guesswork — every decision about layout, copy, color, and hierarchy is already made.

---

## Future State — Canva Connect API Integration

When the Canva Connect API is connected to the StackdMedia platform, `generate-assets` will trigger **programmatic design creation** automatically.

### What the API will enable:

- **Programmatic design creation** from templates — the skill will select a template by ID and populate it with campaign-specific copy, colors, and assets
- **Brand kit auto-application** — brand colors, fonts, and logos will be applied automatically from a stored Canva brand kit linked to the client
- **Asset upload** — product images and photography will be uploaded to Canva directly via the API before design creation
- **Bulk export** — all 9 asset types for a campaign can be exported in a single automated run
- **Shareable Canva links** — the skill will return direct Canva design links so clients or designers can review and tweak before final export
- **Folder organization** — designs will be automatically organized into Canva folders by client and campaign

### What the API cannot currently do (as of early 2026):

- **AI-generated images** — Canva's AI image generation (Magic Media) is not accessible programmatically via the Connect API; images must be provided as uploads
- **Font licensing automation** — premium fonts in Canva require the account to have the appropriate subscription; the API cannot grant font access
- **Template creation** — the API can use existing templates but cannot create new custom templates programmatically
- **Direct publish to social** — the API handles design creation and export, not publishing; social posting requires a separate integration

---

## Preparing Now for a Smooth API Integration

Take these steps in Canva today so the API connection requires minimal rework:

### Naming Conventions

Use consistent file naming in Canva that matches the `generate-assets` output format:
```
[brand]-[asset-type]-v[N].[ext]

Examples:
formfocus-instagram-post-v1.jpg
formfocus-youtube-thumbnail-v2.png
formfocus-ad-banners-feed-v1.jpg
```

### Canva Folder Structure

Organize Canva by client and campaign now. The API will mirror this structure:
```
Canva Root/
  └── [Brand Name]/
        ├── Brand Kit (colors, fonts, logo)
        └── [Campaign Name]/
              ├── Instagram/
              ├── YouTube/
              ├── LinkedIn/
              ├── Ad Banners/
              └── Email/
```

### Brand Kit Setup Checklist

Before the API goes live, ensure each client's Canva Brand Kit contains:
- [ ] Primary brand color (hex)
- [ ] Secondary / accent colors (hex)
- [ ] Background color (hex)
- [ ] Brand fonts (headline weight, body weight)
- [ ] Logo — full color version (PNG with transparency)
- [ ] Logo — white version (for dark backgrounds)
- [ ] Logo — dark version (for light backgrounds)
- [ ] Brand kit name matches the `brand` field in AssetConfig exactly

---

## Webhook / Automation Flow (When API is Live)

When the Canva Connect API integration is active, the `generate-assets` skill will:

1. Parse the design specs it generates
2. POST to the Canva Connect API to create each design from the appropriate template
3. Upload brand assets and campaign visuals via the Canva asset upload endpoint
4. Trigger bulk export for all requested asset types
5. Return a response that includes:
   - Shareable Canva design URLs (for designer review)
   - Direct download links for exported files
   - Canva folder URL for the full campaign asset set

The campaign brief, scripts, and asset links will all be available in a single StackdMedia campaign workspace — no manual file hunting across platforms.
