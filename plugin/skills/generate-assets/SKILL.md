---
name: generate-assets
version: 1.0.0
description: Use when generating visual asset design specs for a campaign, creating Canva-ready design briefs, producing Instagram posts, carousel posts, Stories, TikTok covers, YouTube thumbnails, LinkedIn images, ad banners, or email headers. Triggers on phrases like "generate assets", "create visuals", "design specs", "Instagram post", "YouTube thumbnail", "make assets for this campaign", or when a brief exists and visual creative needs to be produced alongside scripts.
---

# generate-assets

## Purpose

Generate Canva-ready visual asset design specifications for all campaign surfaces. Given a creative brief and brand assets, produce detailed design specs for each requested asset type — detailed enough for a designer (or Canva) to produce the asset without additional direction.

## Pipeline Position

```
generate-brief
      │
      ├──────────────────────┬──────────────────────┐
      │                      │                      │
  script-tiktok          script-*              generate-assets
  script-instagram       (all platforms)            │
  script-youtube-*                            Kie.ai Nano Banana
  script-linkedin                             (2K draft / 4K final)
      │                                             │
      │                                      upload-asset-from-url
      │                                        (final tier)
      │                                             │
      └──────────────────────┴──────────────────────┘
                             │
                         storyboard
                             │
                     full campaign delivery
```

`generate-assets` runs **in parallel** with all `script-*` skills after `generate-brief` completes. It does not depend on scripts, and scripts do not depend on it. Both feed into `storyboard` and final campaign delivery.

## Canva Integration Note

This skill generates images via Kie.ai Nano Banana and — on `canva_assembly: final` — **automatically assembles the full Canva design**: creates the design at correct dimensions, places the generated image as background, and adds all text layers as editable Canva elements. The result is a ready-to-edit Canva design URL, not just loose assets.

See `references/canva-integration.md` for the full MCP call sequence and setup requirements.

---

## AI Image Generation (Kie.ai)

StackdMedia generates campaign images using **Kie.ai Nano Banana** — Google Gemini-powered image generation accessible via the Kie.ai MCP server. Images are generated from the design spec, then uploaded directly to Canva for design assembly.

### Two-Tier Workflow

**Draft (Nano Banana 2K — $0.02/image)**
Use during creative development and client preview rounds.
- Resolution: 2048px native output
- Speed: fast generation (~10-15 seconds)
- Use for: iteration, client approval, internal review
- Images returned as preview URLs — not uploaded to Canva

**Final (Nano Banana 4K — $0.04/image)**
Use for production-ready assets ready for campaign delivery.
- Resolution: 4096px native output (intelligent 4K scaling)
- Quality: highest visual fidelity, improved text rendering
- Use for: final campaign delivery, Canva upload, export
- Images automatically uploaded to Canva via `upload-asset-from-url`

### Prompt Construction Rules

When translating a design spec into a Nano Banana image prompt:
1. **Lead with the key visual** — describe the subject first (product, person, scene)
2. **Include composition** — foreground/background positioning from the Layout section
3. **Specify color palette** — use hex values from brand colors as descriptors ("deep navy blue #1a237e background")
4. **Include lighting and mood** — from the Visual Direction section
5. **Add style keywords** — "professional product photography", "UGC lifestyle photo", "clean minimal ad creative"
6. **Specify aspect ratio** — "square format 1:1", "vertical 9:16", "landscape 16:9"
7. **Avoid** — words like "text", "logo", "typography" (Kie generates images, text layers are added in Canva)

**Example prompt structure:**
```
[Subject/key visual], [composition], [background], [lighting], [mood/style], [aspect ratio], high quality, professional photography, commercial advertising
```

### Image Validation (All tiers)

After Nano Banana returns an image, visually inspect the thumbnail to confirm it contains **no embedded text, logos, or typography**. If text artifacts are present, regenerate with the prompt adjusted (strengthen the avoid-text rule: append "absolutely no text, no words, no letters, no typography, no labels" to the prompt).

### Canva Design Assembly (controlled by `canva_assembly` flag)

**`canva_assembly: skip`** — Return the image URL only. No Canva interaction.

**`canva_assembly: draft`** (default) — Upload only:
1. Call `mcp__claude_ai_Canva__upload-asset-from-url` with the image URL and asset name
2. Return the Canva Asset ID in the spec — designer assembles manually

**`canva_assembly: final`** — Full design assembly:
1. `mcp__claude_ai_Canva__upload-asset-from-url` — upload the Nano Banana image, receive Asset ID
2. `mcp__claude_ai_Canva__generate-design-structured` — create a new design at the correct platform dimensions (see Asset Type Specifications for exact px), using a clean single-image layout
3. `mcp__claude_ai_Canva__start-editing-transaction` — open an editing session on the new design
4. `mcp__claude_ai_Canva__perform-editing-operations` — insert the uploaded asset as the full-bleed background image, then add each row from the **Text Layers** table as an editable text element at the specified position, font style, size, and color
5. `mcp__claude_ai_Canva__commit-editing-transaction` — save and close the editing session
6. `mcp__claude_ai_Canva__get-design-thumbnail` — retrieve a preview thumbnail URL
7. Return the Canva design URL and thumbnail in the spec

**Cost note:** `canva_assembly: final` consumes Canva API quota — use `draft` for iteration rounds and `final` only for production delivery.

---

## Configuration (AssetConfig)

```yaml
assets:          # Array of asset types to generate
                 # Options: instagram-post | instagram-carousel | instagram-story |
                 #          tiktok-cover | youtube-thumbnail | youtube-channel-art |
                 #          linkedin-post | linkedin-carousel-slide |
                 #          ad-banners | email-header | all
brand:           # Brand name — used for file naming and Canva folder organization
variations:      # Number of design directions per asset: 1 | 2 | 3
render_tier:     # draft | final
                 # draft  = Nano Banana 2K ($0.02/image) — fast previews, client review
                 # final  = Nano Banana 4K ($0.04/image) — production quality
                 # default: draft
canva_assembly:  # skip | draft | final
                 # skip   = image generation only, no Canva interaction
                 # draft  = generate image + upload to Canva (returns Asset ID)
                 # final  = generate image + upload + assemble full Canva design with text layers
                 # default: draft
```

**Example:**
```yaml
assets: [instagram-post, instagram-carousel, youtube-thumbnail]
brand: formfocus
variations: 2
```

---

## Required Inputs & Validation

Before generating specs, confirm the following inputs are present in the brief or provided directly. If any are missing, ask before proceeding.

| Input | Required | Notes |
|-------|----------|-------|
| Creative brief | Yes | Output from `generate-brief` or equivalent |
| Brand name | Yes | Used in file naming |
| Brand colors (hex) | Yes | At minimum: primary, background, text, accent |
| Brand fonts | Yes | Font names or style description (e.g., "clean sans-serif, bold headlines") |
| Key visual | Yes | Product image description or reference asset |
| Target platform(s) | Yes | Determines which asset types to generate |
| Campaign hook / headline | Recommended | From brief — informs text layer copy |
| CTA | Recommended | "Try free", "Learn more", etc. |

---

## Asset Type Specifications

### 1. Instagram Post

**Formats:**
- Square: 1080x1080 px
- Portrait: 1080x1350 px

**Safe Zones:**
- Keep all critical content (text, logo, CTA) within the inner 900x900 px for square / 900x1150 px for portrait
- Avoid the outer 90px border — may be clipped in some feed views

**Required Elements:** Brand logo, headline, key visual, CTA (optional for awareness posts)

**Optional Elements:** Subhead, product label, URL, hashtag strip

**Copy Guidelines:**
| Layer | Max Characters |
|-------|----------------|
| Headline | 40 characters |
| Subhead | 80 characters |
| CTA button | 20 characters |
| Caption (not in image) | 2,200 characters |

**Design Direction:** Lead with the key visual (product or lifestyle). Text overlay should feel intentional — not covering the primary visual. Use brand primary color for CTA button.

---

### 2. Instagram Carousel Post

**Format:** Multi-slide, each slide 1080x1080 px

**Safe Zones:** Same as Instagram Post. Additionally: keep important elements away from the right edge of all slides except the last — the right edge bleeds into the next slide.

**Required Elements per set:** Hook on slide 1, content/proof in middle slides, CTA on final slide

**Slide Structure:**
- **Slide 1 (Hook/Cover):** Big bold headline, key visual, swipe prompt ("Swipe to see →" or similar). This is the only slide shown in the feed — it must stop the scroll.
- **Middle Slides (Features/Proof):** One idea per slide. Use a consistent layout system — same logo position, same margin structure across all slides.
- **Last Slide (CTA):** Clear CTA, brand name, URL or handle, minimal design.

**Copy Guidelines:**
| Layer | Max Characters |
|-------|----------------|
| Slide headline | 35 characters |
| Slide body copy | 100 characters |
| Swipe prompt (slide 1) | 20 characters |
| CTA (last slide) | 25 characters |

**Design Direction:** Maintain visual consistency across slides. Use a "connecting" design element (color band, shape, or line) that flows from slide to slide to reward swiping.

---

### 3. Instagram Story

**Format:** 9:16 vertical, 1080x1920 px

**Safe Zones:**
- Top 250px: Instagram UI overlap (profile name, timestamp) — no critical content
- Bottom 250px: Instagram UI overlap (swipe-up / link sticker zone) — no critical content
- Critical content zone: central 1080x1420 px (y: 250–1670)
- Side margins: 75px each side

**Required Elements:** Key visual, headline, CTA (link sticker or "swipe up" prompt)

**Optional Elements:** Countdown sticker area, poll/quiz sticker zone, music attribution

**Copy Guidelines:**
| Layer | Max Characters |
|-------|----------------|
| Headline | 30 characters |
| Supporting text | 60 characters |
| CTA label | 15 characters |

**Design Direction:** Full-bleed visual. Text should overlay with high contrast. Use brand accent color for CTA. Design for vertical viewing — stack elements top to bottom rather than side by side.

---

### 4. TikTok Cover Frame

**Format:** 9:16 vertical, 1080x1920 px

**Safe Zones:**
- Profile grid crop: only the **center 70% of the frame width** (approximately x: 162–918) is visible in the TikTok profile grid — do not place logo or key text outside this zone
- Bottom 300px: TikTok caption overlay area
- Top 150px: Status bar / navigation overlap

**Required Elements:** Key visual (works as both video still and static thumbnail), title text, brand mark

**Optional Elements:** Episode number (for series), duration badge

**Copy Guidelines:**
| Layer | Max Characters |
|-------|----------------|
| Title | 30 characters (must read in profile grid at small size) |
| Series label | 20 characters |

**Design Direction:** This frame appears on the creator's profile grid — it must look intentional, not like a random video still. Design it as a thumbnail first. Bold text, high contrast, clear subject. Should communicate the video topic in under 2 seconds of scanning.

---

### 5. YouTube Thumbnail

**Format:** 16:9 landscape, 1280x720 px (must also work at 320x180)

**Safe Zones:**
- Keep all text and key visuals within the inner 1140x620 px
- Outer 70px border may be clipped or overlapped by player chrome

**Required Elements:** Expressive face/reaction (if applicable), bold text overlay, high-contrast background

**Optional Elements:** Product/device mockup, arrow or pointer element, episode branding

**Copy Guidelines:**
| Layer | Max Characters |
|-------|----------------|
| Thumbnail text | **6 words maximum** — must be legible at 320x180 |
| Secondary text | 3-4 words, smaller — omit if crowding |

**Design Direction:**
- Face + expression + text is the highest-converting thumbnail format
- Use extreme contrast — the thumbnail competes with hundreds of others
- Text must be **bold, large, and readable at tiny size** — test your spec at 320x180
- Avoid more than 2 font sizes
- Bright, saturated colors outperform muted palettes on YouTube
- If using a person: crop to face/chest, not full body

---

### 6. YouTube Channel Art

**Format:** 2560x1440 px

**Safe Zones:**
- **TV safe zone:** 2560x1440 px (full canvas — visible on TV)
- **Desktop safe zone:** 1546x423 px (centered) — only this area is guaranteed visible on desktop
- **Mobile safe zone:** 1546x423 px (same as desktop)
- **All devices safe zone:** 1235x338 px (centered) — this area is visible on ALL screens including mobile
- Logo and essential text must be within the 1235x338 px all-devices zone

**Required Elements:** Brand name/logo, tagline or value proposition, visual identity (color, pattern, or imagery)

**Optional Elements:** Social handle, website URL, profile photo coordination

**Copy Guidelines:**
| Layer | Max Characters |
|-------|----------------|
| Brand name | 30 characters |
| Tagline | 60 characters |
| URL/handle | 40 characters |

**Design Direction:** Design the full 2560x1440 canvas as a branded environment, but ensure the core message lives within the 1235x338 center zone. Treat outer areas as decorative/brand pattern extensions.

---

### 7. LinkedIn Post Image

**Format:** 1200x627 px

**Safe Zones:**
- Keep all critical content within the inner 1100x527 px
- Outer 50px may be clipped in some LinkedIn views

**Required Elements:** Key visual or data visualization, headline, brand logo

**Optional Elements:** Author name/title, company name, stat or pull quote

**Copy Guidelines:**
| Layer | Max Characters |
|-------|----------------|
| Headline | 50 characters |
| Supporting text / stat | 80 characters |
| Author attribution | 40 characters |

**Design Direction:** LinkedIn audience expects professional, credible visuals. Prioritize data, outcomes, and authority signals (logos, credentials, stats). Clean layouts with whitespace outperform busy designs. Brand logo should be present but not dominant.

---

### 8. Facebook/Instagram Ad Banners

Generate all 4 sizes as a set. Copy must scale — the headline that works at 1200x628 must also work compressed at 300x250.

**Sizes:**
| Format | Dimensions | Primary Use |
|--------|-----------|-------------|
| Feed banner | 1200x628 px | Facebook/Instagram feed ad |
| Square | 1080x1080 px | Instagram feed + Facebook square |
| Story | 1080x1920 px | Stories placement |
| Display | 300x250 px | Google Display / partner networks |

**Safe Zones:**
- Feed (1200x628): inner 1100x528 px
- Square (1080x1080): inner 900x900 px
- Story (1080x1920): central 1080x1420 px (same as Instagram Story)
- Display (300x250): inner 260x210 px — every pixel counts at this size

**Required Elements (all sizes):** Brand logo, headline, CTA button or label, key visual

**Copy Scaling Rules:**
| Layer | 1200x628 | 1080x1080 | 1080x1920 | 300x250 |
|-------|----------|----------|----------|---------|
| Headline | 50 chars | 40 chars | 35 chars | **20 chars max** |
| Subhead | 80 chars | 80 chars | 60 chars | omit |
| CTA | 20 chars | 20 chars | 15 chars | 12 chars |

**Design Direction:** Ad banners must communicate the core offer in under 3 seconds. Lead with the outcome, not the product. CTA button must be visually distinct. For 300x250 display: reduce to logo + 1 bold headline + 1 CTA — nothing else.

---

### 9. Email Header

**Format:** 600x200 px (standard email header)

**Safe Zones:**
- Design for 600px desktop rendering AND ~320px mobile rendering (retina 2x)
- Text must be large enough to read on mobile **without zooming**
- Minimum headline font size: 28px (displayed), which renders as 56px in retina-export Canva files

**Required Elements:** Brand logo, headline or campaign name, optional CTA or date

**Optional Elements:** Divider line, subtle background pattern, preheader complement graphic

**Copy Guidelines:**
| Layer | Max Characters |
|-------|----------------|
| Headline | 40 characters |
| Subhead | 60 characters |
| CTA label | 20 characters |

**Design Direction:** Email headers are viewed across wildly different email clients — keep designs simple and robust. Avoid tiny text. Use RGB/sRGB colors (no CMYK). Export as JPG for photo-heavy headers, PNG if transparency or crisp text on flat color is needed.

---

### 10. LinkedIn Carousel Slide

Used with the `script-linkedin-post` skill (carousel format). Each carousel is a set of 5–10 slides produced as individual image assets.

**Format:** 1080x1080 px (square) — renders cleanly both in the LinkedIn carousel viewer and as standalone posts

**Safe Zones:**
- Keep all critical content within the inner 900x900 px
- Leave the right edge of slides 1 through N-1 visually "open" — the carousel bleeds into the next slide

**Required Elements per slide:**
- Slide 1 (Cover): Bold headline, key visual, swipe prompt ("Swipe →")
- Middle slides: Short title, 1–2 lines of body copy, supporting visual
- Last slide (CTA): Clear ask, brand name, URL or handle

**Copy Guidelines:**
| Layer | Max Characters |
|-------|----------------|
| Slide headline / title | 40 characters |
| Body copy | 120 characters |
| Swipe prompt (slide 1 only) | 20 characters |
| CTA (last slide) | 30 characters |

**Slide numbering in file names:** `[brand]-linkedin-carousel-slide-[N]-v[variation].[ext]`

**Design Direction:** Maintain consistent layout across all slides — same logo position, same margin grid, same font sizing. Use a visual "connecting" element (color band, shape, or overlapping graphic) that flows from slide to slide to reward swiping. Each slide must stand alone as a readable unit — a viewer who drops in on slide 3 should still get value.

**AI Image Prompt guidance:** For carousel slides, generate a supporting background image per slide that reinforces the slide's one idea. Avoid busy compositions — the image is a backdrop for the text. Keep subject matter consistent across the set (same brand color world, same photographic style, same mood).

---

## Output Format

For each asset, produce one spec block per variation using this exact format:

```
## [Asset Name] — Variation [N]

**Dimensions:** [W x H px]
**Format:** [JPG/PNG]
**File name:** [brand]-[asset-type]-v[N].[ext]

### Layout
[Describe the visual layout: what's in the foreground, midground, background. Be spatial and specific — top-left, center, bottom-right.]

### Text Layers
| Layer | Copy | Font Style | Size | Color | Position |
|-------|------|-----------|------|-------|----------|
| Headline | [copy] | [style] | [size] | [hex] | [position] |
| Subhead | [copy] | [style] | [size] | [hex] | [position] |
| CTA | [copy] | [style] | [size] | [hex] | [position] |
| Logo | N/A | N/A | [size] | [hex or "full color"] | [position] |

### Visual Direction
[Product placement, background treatment, mood, lighting, color palette application. Be specific: "warm gradient from #2563EB at top-left to #10B981 at bottom-right" is better than "colorful background".]

### Brand Application
[How brand colors are applied: which color on which element. How brand fonts are used: which weight/style for headline vs body vs CTA.]

### Canva Template Recommendation
[Describe the type of Canva template to start from. Be specific enough that a designer can search and find it — e.g., "Minimalist product launch Instagram post with bold headline overlay", "Lifestyle photography with text strip at bottom".]

### Designer Notes
[Special instructions: safe zones to respect, elements to avoid, accessibility considerations, export settings.]

### AI Image Prompt
[The exact prompt sent to Nano Banana for this variation]

### Generated Image
[URL returned by Nano Banana — populated after generation]

### Canva Asset ID
[Asset ID after upload-asset-from-url — populated when canva_assembly is draft or final]

### Canva Design URL
[URL of the assembled Canva design — populated when canva_assembly: final only]

### Canva Thumbnail
[Preview thumbnail URL — populated when canva_assembly: final only]
```

---

## Your Task

Given the creative brief, brand assets, and AssetConfig, produce Canva-ready design specifications for each requested asset type.

**Step-by-step:**

1. **Parse inputs:** Extract brand colors, fonts, key visual description, campaign hook, and CTA from the brief. Confirm `canva_assembly` setting — if not specified, default to `draft`.
2. **Confirm asset list:** If `assets: all`, generate specs for all 10 asset types. Otherwise generate only the specified types.
3. **Apply brief to each asset:** Use the campaign's hook, proof points, and CTA to populate text layers. Do not use placeholder copy — generate real copy derived from the brief.
4. **Generate AI prompts:** For each asset variation, construct a Nano Banana image prompt using the rules in the AI Image Generation section above. Add the prompt to each spec block under `### AI Image Prompt`.
5. **Generate images via Kie.ai:** Call Nano Banana with each prompt at the appropriate tier (2K for draft, 4K for final). Validate the returned image — if text artifacts appear in the thumbnail, regenerate with a stronger no-text instruction. Populate `### Generated Image` with the final URL.
6. **Canva workflow (per `canva_assembly` setting):**
   - `skip`: skip steps 6a–6e entirely
   - `draft`: run step 6a only
   - `final`: run all steps 6a–6e
   - **6a.** Call `mcp__claude_ai_Canva__upload-asset-from-url` → populate `### Canva Asset ID`
   - **6b.** Call `mcp__claude_ai_Canva__generate-design-structured` at correct dimensions → receive design ID
   - **6c.** Call `mcp__claude_ai_Canva__start-editing-transaction` on the design
   - **6d.** Call `mcp__claude_ai_Canva__perform-editing-operations` to place image as background and add each text layer from the spec
   - **6e.** Call `mcp__claude_ai_Canva__commit-editing-transaction`, then `mcp__claude_ai_Canva__get-design-thumbnail` → populate `### Canva Design URL` and `### Canva Thumbnail`
7. **Output specs:** One complete spec block per asset per variation, with all fields populated.
8. **Close with file list:** End with a summary table of all assets, their status, and Canva design URLs (final assembly) or Asset IDs (draft) or preview URLs (skip).

Each spec must be detailed enough for a designer to open Canva and build the asset immediately — without asking any follow-up questions.

---

## Reference Files

- `references/asset-specs.md` — Exact dimensions, safe zones, platform file size limits, export settings
- `references/canva-integration.md` — Current manual workflow + future Canva Connect API integration plan
- `references/example-output.md` — Complete example output for FormFocus (AI form builder)
