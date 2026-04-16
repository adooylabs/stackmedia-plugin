# Canva Integration Reference

How `generate-assets` works with Kie.ai and Canva in the current pipeline.

---

## Pipeline Overview

```
Design Spec
    │
    ▼
Nano Banana 2K or 4K            ← Kie.ai MCP (KIE_AI_API_KEY)
(image generation — no text)
    │
    ▼
Image Validation
(reject if text artifacts present — regenerate)
    │
    ├── canva_assembly: skip ────────────────→ Return image URL only
    │
    ├── canva_assembly: draft ───────────────→ upload-asset-from-url → Canva Asset ID
    │                                           (designer assembles manually)
    │
    └── canva_assembly: final
            │
            ▼
        upload-asset-from-url               ← mcp__claude_ai_Canva__upload-asset-from-url
        (upload image, receive Asset ID)
            │
            ▼
        generate-design-structured          ← mcp__claude_ai_Canva__generate-design-structured
        (create design at correct px dims)
            │
            ▼
        start-editing-transaction           ← mcp__claude_ai_Canva__start-editing-transaction
            │
            ▼
        perform-editing-operations          ← mcp__claude_ai_Canva__perform-editing-operations
        (place image as background +
         add text layers from spec)
            │
            ▼
        commit-editing-transaction          ← mcp__claude_ai_Canva__commit-editing-transaction
            │
            ▼
        get-design-thumbnail                ← mcp__claude_ai_Canva__get-design-thumbnail
            │
            ▼
        Return: Canva Design URL + Thumbnail
```

---

## MCP Call Reference (canva_assembly: final)

### Step 1 — Upload image

```
mcp__claude_ai_Canva__upload-asset-from-url
  url:   [Nano Banana image URL]
  name:  [brand]-[asset-type]-v[N]-final
```
Returns: `assetId`

### Step 2 — Create design

```
mcp__claude_ai_Canva__generate-design-structured
  title:  [brand] [asset-type] v[N]
  width:  [px — per asset type spec]
  height: [px — per asset type spec]
```

**Dimension reference:**
| Asset Type | Width | Height |
|------------|-------|--------|
| instagram-post (square) | 1080 | 1080 |
| instagram-post (portrait) | 1080 | 1350 |
| instagram-carousel | 1080 | 1080 |
| instagram-story | 1080 | 1920 |
| tiktok-cover | 1080 | 1920 |
| youtube-thumbnail | 1280 | 720 |
| youtube-channel-art | 2560 | 1440 |
| linkedin-post | 1200 | 627 |
| linkedin-carousel-slide | 1080 | 1080 |
| ad-banners (feed) | 1200 | 628 |
| email-header | 600 | 200 |

Returns: `designId`

### Step 3 — Open editing session

```
mcp__claude_ai_Canva__start-editing-transaction
  designId: [from step 2]
```
Returns: `transactionId`

### Step 4 — Place image + add text layers

```
mcp__claude_ai_Canva__perform-editing-operations
  transactionId: [from step 3]
  operations:
    - type: ADD_IMAGE
      assetId: [from step 1]
      position: full-bleed background
    - type: ADD_TEXT
      content: [headline copy from spec]
      style: [font, size, color, weight from Text Layers table]
      position: [from spec — e.g., top-left, bottom-center]
    - type: ADD_TEXT
      content: [subhead copy]
      ...
    - type: ADD_TEXT
      content: [CTA copy]
      ...
```

Add one `ADD_TEXT` operation per row in the spec's **Text Layers** table. Logo placement is handled manually or via brand kit — do not attempt to add logo via this step.

### Step 5 — Commit and preview

```
mcp__claude_ai_Canva__commit-editing-transaction
  transactionId: [from step 3]
```

```
mcp__claude_ai_Canva__get-design-thumbnail
  designId: [from step 2]
```

Returns: `designUrl`, `thumbnailUrl`

---

## Setup Requirements

1. **Kie.ai MCP server** must be connected with `KIE_AI_API_KEY` env var set
2. **Canva MCP server** (`claude.ai Canva`) must be connected — available as a Claude.ai integration
3. Both MCP servers are available in Claude Code after setup

---

## Cost Reference

| Operation | Cost | Notes |
|-----------|------|-------|
| Nano Banana 2K | $0.02/image | Draft tier |
| Nano Banana 4K | $0.04/image | Final tier |
| Canva API calls | Canva plan quota | `generate-design-structured`, `perform-editing-operations`, etc. consume Canva API usage |

Use `canva_assembly: draft` for iteration rounds. Reserve `canva_assembly: final` for production delivery to minimize Canva API quota usage.

---

## Canva Asset Naming

Use consistent naming when uploading assets:

```
[brand]-[asset-type]-v[N]-[tier]

Examples:
formfocus-instagram-post-v1-draft
formfocus-youtube-thumbnail-v2-final
formfocus-linkedin-carousel-slide-3-v1-final
```

---

## Canva Folder Structure

Organize assets by brand and campaign:

```
Canva Root/
  └── [Brand Name]/
        ├── Brand Kit (colors, fonts, logo)
        └── [Campaign Name]/
              ├── Instagram/
              ├── YouTube/
              ├── LinkedIn/
              │     ├── linkedin-post-v1 (design)
              │     └── linkedin-carousel/ (slide designs)
              ├── Ad Banners/
              └── Email/
```

---

## Brand Kit Setup Checklist

Before generating `canva_assembly: final` assets, ensure the client's Canva Brand Kit contains:
- [ ] Primary brand color (hex)
- [ ] Secondary / accent colors (hex)
- [ ] Background color (hex)
- [ ] Brand fonts (headline weight, body weight)
- [ ] Logo — full color version (PNG with transparency)
- [ ] Logo — white version (for dark backgrounds)
- [ ] Logo — dark version (for light backgrounds)
- [ ] Brand kit name matches the `brand` field in AssetConfig exactly

---

## What Still Requires Manual Canva Work

Even with `canva_assembly: final`, the following are not automated:
- **Logo placement** — add from Brand Kit manually after assembly
- **Brand kit application** — font and color swatches applied manually
- **Safe zone final check** — designer confirms no critical content is clipped
- **Export** — download from Canva at correct format and resolution
- **Shareable link generation** — share from Canva editor

---

## Limitations

- **Canva Magic Media** is not accessible via MCP — Kie.ai Nano Banana is the image generation engine
- **Font licensing** — premium Canva fonts require account subscription; API cannot grant font access
- **Direct social publishing** — Canva handles design creation and export, not social posting
- **Custom template creation** — designs start from scratch or Canva's default layouts, not custom saved templates
