# Canva Integration Reference

How `generate-assets` works with Kie.ai and Canva in the current pipeline.

---

## Current Pipeline — Kie.ai Nano Banana + Canva

The `generate-assets` skill now generates actual images using **Kie.ai Nano Banana** and uploads them to Canva for design assembly.

### Full Workflow

```
Design Spec
    │
    ▼
Nano Banana 2K or 4K         ← Kie.ai MCP (KIE_AI_API_KEY)
(image generation)
    │
    ▼
Generated Image URL
    │
    ├── Draft tier: return as preview URL
    │
    └── Final tier:
            │
            ▼
        upload-asset-from-url  ← Canva MCP
        (upload to Canva)
            │
            ▼
        Canva Asset ID
        (ready for design assembly)
```

### Setup Requirements

1. **Kie.ai MCP server** must be connected with `KIE_AI_API_KEY` set
2. **Canva MCP server** must be connected for final-tier uploads
3. Both MCP servers are available in Claude Code after setup

### Cost Reference

| Tier | Model | Resolution | Cost | Use Case |
|------|-------|-----------|------|----------|
| Draft | Nano Banana 2K | 2048px native | $0.02/image | Client previews, iteration |
| Final | Nano Banana 4K | 4096px (intelligent upscale) | $0.04/image | Production delivery |

---

## Canva Asset Naming

Use consistent naming when uploading assets to Canva:

```
[brand]-[asset-type]-v[N]-[tier]

Examples:
vaultsync-instagram-post-v1-draft
vaultsync-youtube-thumbnail-v2-final
vaultsync-ad-banners-feed-v1-final
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
              ├── Ad Banners/
              └── Email/
```

---

## Brand Kit Setup Checklist

Before generating final-tier assets, ensure the client's Canva Brand Kit contains:
- [ ] Primary brand color (hex)
- [ ] Secondary / accent colors (hex)
- [ ] Background color (hex)
- [ ] Brand fonts (headline weight, body weight)
- [ ] Logo — full color version (PNG with transparency)
- [ ] Logo — white version (for dark backgrounds)
- [ ] Logo — dark version (for light backgrounds)
- [ ] Brand kit name matches the `brand` field in AssetConfig exactly

---

## What Canva Handles (Post-Upload)

After images are uploaded via Kie.ai → Canva:

1. **Text layer overlay** — headlines, CTAs, subheads added in Canva editor
2. **Brand kit application** — brand colors, fonts, logos applied from Brand Kit
3. **Safe zone compliance** — designer ensures content stays within safe zones per asset type
4. **Export** — final files exported per platform specs (JPG/PNG, sRGB, correct dimensions)
5. **Shareable links** — Canva design URLs returned for client review

---

## Limitations

- **Canva Magic Media** is not accessible via MCP — Kie.ai Nano Banana is the image generation engine
- **Font licensing** — premium Canva fonts require account subscription; API cannot grant font access
- **Direct social publishing** — Canva handles design creation and export, not social posting
- **Template creation** — the API uses existing Canva templates, not custom ones
