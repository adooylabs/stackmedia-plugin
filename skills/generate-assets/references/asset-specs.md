# Asset Specifications Reference

Complete technical specifications for all 9 asset types produced by the `generate-assets` skill.

---

## Color Mode — All Assets

- **Color space:** sRGB (not Adobe RGB, not CMYK)
- **Mode:** RGB for all digital assets
- **Bit depth:** 8-bit per channel (24-bit color)
- Canva exports in sRGB by default — no action required unless the designer manually changed color profiles

---

## 1. Instagram Post

| Property | Square | Portrait |
|----------|--------|---------|
| Dimensions | 1080x1080 px | 1080x1350 px |
| Aspect ratio | 1:1 | 4:5 |
| Format | JPG or PNG | JPG or PNG |
| Max file size | 30 MB | 30 MB |
| Min resolution | 72 dpi (screen) | 72 dpi (screen) |

**Safe zone:** Keep all critical content within the inner 900x900 px (square) or 900x1150 px (portrait). The outer ~90px border may be clipped.

**Canva export settings:** Download as JPG (quality: High) for photo-heavy designs. Use PNG if the design includes a transparent element or crisp flat-color text on a solid background.

**Text readability:** Minimum headline font size 36px at 1080px canvas width.

---

## 2. Instagram Carousel Post

| Property | Value |
|----------|-------|
| Dimensions | 1080x1080 px per slide |
| Aspect ratio | 1:1 |
| Slides | 2–10 slides per carousel |
| Format | JPG or PNG |
| Max file size | 30 MB per slide |

**Safe zone:** Keep critical content within the inner 900x900 px. Additionally: avoid the rightmost 90px on all slides except the last — this area is visually adjacent to the next slide in the swipe transition.

**Canva export settings:** Export each slide as a separate JPG. Name files sequentially: `[brand]-carousel-s1.jpg`, `[brand]-carousel-s2.jpg`, etc.

**Text readability:** Minimum headline font size 36px. Slide body copy minimum 24px.

---

## 3. Instagram Story

| Property | Value |
|----------|-------|
| Dimensions | 1080x1920 px |
| Aspect ratio | 9:16 |
| Format | JPG or PNG (static); MP4/MOV (video) |
| Max file size | 30 MB (image), 4 GB (video) |

**Safe zone diagram:**
```
┌─────────────────────────────┐ ↑ 1920px total
│  [TOP UI ZONE — 250px]      │ ← Instagram profile + timestamp overlay
│  ─────────────────────────  │
│                             │
│                             │
│   CRITICAL CONTENT ZONE     │
│   1080 x 1420 px            │ ← All text, logo, CTA must live here
│   (y: 250px – 1670px)       │
│                             │
│                             │
│  ─────────────────────────  │
│  [BOTTOM UI ZONE — 250px]   │ ← Link sticker / swipe-up area
└─────────────────────────────┘
```

**Side margins:** 75px each side inside the critical content zone.

**Canva export settings:** PNG for text-heavy designs; JPG for photography-based designs.

**Text readability:** Minimum headline font size 60px. Supporting text minimum 36px.

---

## 4. TikTok Cover Frame

| Property | Value |
|----------|-------|
| Dimensions | 1080x1920 px |
| Aspect ratio | 9:16 |
| Format | JPG or PNG |
| Max file size | 50 MB |

**Safe zone diagram:**
```
┌─────────────────────────────┐ ↑ 1920px total
│ [TOP — 150px]               │ ← Status bar / nav overlap
│ ░░░░░[LEFT 162px]░░░░       │
│        ┌──────────────┐     │
│        │              │     │
│        │  PROFILE     │     │
│        │  GRID SAFE   │     │ ← 756px wide (x: 162–918)
│        │  ZONE        │     │ ← This is what appears in profile grid
│        │              │     │
│        └──────────────┘     │
│ ░░░░░[RIGHT 162px]░░░░      │
│ [BOTTOM — 300px]            │ ← Caption overlay area
└─────────────────────────────┘
```

**Critical rule:** The profile grid crops ~15% from each horizontal edge. All logos, title text, and primary visuals must be within the center 756px width (x: 162–918).

**Canva export settings:** JPG, high quality.

**Text readability:** Title text minimum 72px — must be legible at the small profile grid thumbnail size.

---

## 5. YouTube Thumbnail

| Property | Value |
|----------|-------|
| Dimensions | 1280x720 px |
| Aspect ratio | 16:9 |
| Format | JPG or PNG |
| Max file size | **2 MB** (YouTube hard limit) |
| Recommended format | JPG (smaller file size) |

**Safe zone:** Keep all text and key visuals within the inner 1140x620 px. Outer 70px may be clipped or overlapped by player chrome.

**Critical size test:** Design must be legible at 320x180 px (the size shown in YouTube's sidebar "Up Next" section). After creating the spec, verify: would a viewer reading at 320px wide understand the topic?

**Canva export settings:** Download as JPG. If the file exceeds 2 MB, reduce quality slider to 80% in Canva's download dialog.

**Text readability:** Thumbnail headline minimum 80px at 1280px canvas (scales to ~20px at 320px — bold weight required). Maximum 6 words. High contrast — minimum 4.5:1 contrast ratio between text and background.

---

## 6. YouTube Channel Art

| Property | Value |
|----------|-------|
| Dimensions | 2560x1440 px |
| Aspect ratio | 16:9 |
| Format | JPG or PNG |
| Max file size | 6 MB |

**Safe zone diagram — 3 zones:**
```
┌────────────────────────────────────────────────────┐ ← 2560px
│                                                    │
│   ┌────────────────────────────────────────┐       │
│   │  Desktop + Mobile safe (1546x423 px)   │       │
│   │   ┌──────────────────────────────┐     │       │
│   │   │  ALL DEVICES safe            │     │       │
│   │   │  1235 x 338 px (centered)    │     │       │ ← 1440px
│   │   │  Logo + tagline + URL HERE   │     │       │
│   │   └──────────────────────────────┘     │       │
│   └────────────────────────────────────────┘       │
│                                                    │
└────────────────────────────────────────────────────┘
```

- TV safe: entire 2560x1440 canvas
- Desktop + mobile safe: 1546x423 px centered
- All devices safe: 1235x338 px centered — **logo and essential content must be here**

**Canva export settings:** PNG for designs with text/logos; JPG for photography backgrounds. If PNG exceeds 6 MB, switch to JPG at 90% quality.

**Text readability:** All text in the 1235x338 zone minimum 36px. Treat this zone like a business card — very limited space.

---

## 7. LinkedIn Post Image

| Property | Value |
|----------|-------|
| Dimensions | 1200x627 px |
| Aspect ratio | ~1.91:1 |
| Format | JPG or PNG |
| Max file size | **5 MB** |

**Safe zone:** Keep all critical content within the inner 1100x527 px. Outer 50px may be clipped in some LinkedIn views.

**Canva export settings:** JPG for photography-heavy designs (keeps file size under 5 MB). PNG for designs with flat colors, text, or data visualizations.

**Text readability:** Minimum headline font size 48px. Data/stat text minimum 36px. Minimum contrast ratio 4.5:1 (WCAG AA).

---

## 8. Facebook/Instagram Ad Banners (Set of 4)

| Format | Dimensions | Aspect Ratio | Max File Size | Primary Use |
|--------|-----------|-------------|--------------|-------------|
| Feed banner | 1200x628 px | ~1.91:1 | 30 MB | Facebook/Instagram feed ad |
| Square | 1080x1080 px | 1:1 | 30 MB | Instagram feed + Facebook square |
| Story | 1080x1920 px | 9:16 | 30 MB | Stories placement |
| Display | 300x250 px | 6:5 | **150 KB** | Google Display / partner networks |

**Critical — Display ad (300x250) file size:** Google Display Network hard limit is 150 KB. Export as JPG at 60–70% quality. Avoid complex gradients or large photography in display ads — flat colors compress better.

**Safe zones:**
- Feed (1200x628): inner 1100x528 px
- Square (1080x1080): inner 900x900 px
- Story (1080x1920): central 1080x1420 px (same as Instagram Story)
- Display (300x250): inner 260x210 px — every pixel matters; no wasted space

**Canva export settings:**
- Feed, Square, Story: JPG (high quality)
- Display (300x250): JPG, reduce quality slider until file size is under 150 KB

**Text readability by size:**
| Format | Minimum headline size |
|--------|----------------------|
| 1200x628 | 48px |
| 1080x1080 | 48px |
| 1080x1920 | 60px |
| 300x250 | **28px** (every px counts — go bold weight) |

---

## 9. Email Header

| Property | Value |
|----------|-------|
| Dimensions | 600x200 px |
| Aspect ratio | 3:1 |
| Format | JPG or PNG |
| Max file size | 200 KB (for fast email load) |

**Responsive rendering:** Email headers are displayed at 600px on desktop. On mobile (320px viewport), email clients scale the image to ~320px wide. All text must remain legible after this 50% scale-down.

**Safe zone:** No standard crop — but keep critical content away from extreme edges. Left/right: 20px internal margin. Top/bottom: 15px internal margin.

**Mobile readability rule:** If the headline appears at 200px canvas height but scales to 100px effective height on mobile, ensure the font size chosen at 600px width will read at half that rendered size. Minimum headline at 600px: 40px bold. This renders to ~20px effective on mobile — acceptable minimum.

**Canva export settings:** 
- PNG if the design has a transparent background (for emails with colored backgrounds)
- JPG if the header is fully opaque and photo-based (smaller file size)
- Target under 200 KB — large email images increase load time and can trigger spam filters

**Text readability:** Minimum headline 40px at 600px canvas. Minimum supporting text 24px. Avoid fine serif fonts — they render poorly at small sizes in email clients.

---

## Platform File Size Limits Summary

| Platform/Format | Max File Size | Notes |
|----------------|--------------|-------|
| Instagram (all) | 30 MB | Images |
| YouTube thumbnail | **2 MB** | Hard limit — most common failure point |
| YouTube channel art | 6 MB | |
| LinkedIn | **5 MB** | |
| Facebook ads | 30 MB | |
| Google Display (300x250) | **150 KB** | Hard limit — export at reduced quality |
| Email header | 200 KB | Soft recommendation — affects load time |
| TikTok cover | 50 MB | |

---

## Contrast Ratios & Accessibility

- **Minimum text contrast:** 4.5:1 (WCAG AA) for all body text and small labels
- **Large text (18px+ bold):** 3:1 minimum
- **CTA buttons:** 4.5:1 minimum between button text and button background
- **Text over images:** Use a semi-transparent overlay (e.g., black at 40–60% opacity) or a text shadow when placing text directly on photography
- Use a contrast checker tool (e.g., WebAIM Contrast Checker) if unsure — especially for brand color combinations
