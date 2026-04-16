---
name: generate-video
version: 1.0.0
description: Use when generating AI video content from a script or storyboard. Triggers on "generate video", "create video from storyboard", "make a video ad", "video preview", "render this script as video", "draft video", "final video render", or when a storyboard exists and a video preview or final render is needed. Uses Seedance 2.0 for fast draft previews and Veo 3 for cinematic final renders.
---

# generate-video

## Purpose

Generate AI video content for UGC campaigns using Kie.ai video models. Takes a storyboard or script as input and produces video clips — draft previews via Seedance 2.0 or cinematic final renders via Veo 3.

## Pipeline Position

```
storyboard
    │
    ├── evaluate-content (parallel)
    │
    ▼
generate-video
    │
    ├── Draft: Seedance 2.0 (fast preview, client approval)
    │
    └── Final: Veo 3 (cinematic render, campaign delivery)
         │
         ▼
    campaign delivery
```

`generate-video` runs **after storyboard** and optionally **after evaluate-content passes**. Draft previews can be generated at any point for stakeholder review. Final renders should only be triggered after the script passes evaluation (42/70+).

---

## Configuration (VideoConfig)

```yaml
render_tier:     # draft | final
                 # draft = Seedance 2.0 — 30-40s generation, UGC-optimized, fast iteration
                 # final = Veo 3 — cinematic quality, native audio + lip sync, ~$0.40/video
                 # default: draft

model_override:  # Optional — override the tier default
                 # seedance | veo3 | kling3
                 # kling3 = Kling 3.0 — best for multi-shot product showcases

duration:        # Target clip duration in seconds
                 # 5 | 8 | 10 | 15
                 # Veo 3: 8s max per clip | Seedance 2.0: up to 10s

aspect_ratio:    # 9:16 | 16:9 | 1:1
                 # 9:16 = TikTok, Instagram, YouTube Shorts (default)
                 # 16:9 = YouTube Long-Form, LinkedIn
                 # 1:1 = Instagram Feed square

input_type:      # text | image | storyboard
                 # text = text-to-video from script lines
                 # image = image-to-video from a reference frame
                 # storyboard = scene-by-scene from storyboard output
                 # default: storyboard
```

**Example:**
```yaml
render_tier: draft
duration: 8
aspect_ratio: 9:16
input_type: storyboard
```

---

## Required Inputs & Validation

Before generating, confirm the following are present. If missing, ask before proceeding.

| Input | Required | Notes |
|-------|----------|-------|
| Script or storyboard | Yes | Output from `storyboard` skill (preferred) or `script-*` skill |
| Platform | Yes | Determines aspect ratio and duration defaults |
| render_tier | Yes | draft or final — confirm before generating finals (cost) |
| Brand name | Yes | Used for file naming |
| Key subject | Yes | Main person, product, or scene — anchors prompt construction |

**Cost warning:** Before triggering `final` tier, display the estimated cost to the user:
- Seedance 2.0 (draft): ~$0.05-0.15/video
- Veo 3 (final): ~$0.40/video (8s)

---

## Model Selection Guide

| Use Case | Recommended | Why |
|----------|-------------|-----|
| UGC testimonial / talking head | Seedance 2.0 | Best human video, phoneme-level lip sync, 8+ languages |
| Fast client preview | Seedance 2.0 | 30-40s generation, cost-effective |
| High-volume short clips | Seedance 2.0 | Speed and cost scale well |
| Cinematic hero video | Veo 3 | Best photorealism, physically believable motion |
| Dialogue with native audio | Veo 3 | Only model with native audio + lip sync generation |
| Product showcase (multi-shot) | Kling 3.0 (override) | Best subject consistency across camera angles |
| Brand film / campaign hero | Veo 3 | Reference-grade quality |
| YouTube Long-Form clips | Veo 3 | Best 16:9 landscape quality |

**Default logic:**
- `render_tier: draft` → Seedance 2.0
- `render_tier: final` → Veo 3
- `model_override: kling3` → Kling 3.0 (any tier)

---

## Prompt Construction

### From Storyboard (Recommended)

For each scene in the storyboard output, construct a video prompt using:

1. **Subject** — from `Subject` and `Action` fields
2. **Shot type** — from `Shot Type` and `Camera Angle` fields (e.g., "close-up shot", "wide establishing shot")
3. **Camera movement** — from `Movement` field (e.g., "slow push in", "static camera", "handheld slight shake")
4. **Setting** — from `Setting` and `Lighting` fields
5. **Action** — what the subject is doing, body language, expression
6. **Audio note** — from `Spoken Line` and `Audio Note` fields (Veo 3 only)
7. **Style** — UGC-authentic for social, cinematic for YouTube/LinkedIn

**Storyboard-to-prompt conversion example:**
```
Storyboard scene:
  Shot Type: ECU (Extreme Close-Up)
  Camera Angle: Slightly low angle
  Movement: Static
  Subject: Young woman, 25-30, casual athleisure
  Action: Holds phone to camera showing app, looks directly at lens, slight smile
  Setting: Bright home office, natural light from window left
  Spoken Line: "I used to forget which password was which..."
  Audio Note: Conversational, slightly self-deprecating

Generated prompt:
"Extreme close-up shot, slightly low angle, static camera. Young woman 25-30 in casual athleisure holds a smartphone toward the camera showing an app screen, looking directly at lens with a slight self-deprecating smile. Bright home office setting, natural window light from left, clean background. UGC-style authentic feel, relatable lifestyle video, vertical 9:16 format."
```

### From Script (Text-to-Video)

When no storyboard exists, extract from the script:
1. Each timestamped section becomes one clip
2. Describe the visual action implied by the spoken lines
3. Specify creator type (age range, style, energy level from Director's Note)
4. Include setting from context in the brief

### Prompt Rules

- **Always specify aspect ratio** at the end ("vertical 9:16 format" or "landscape 16:9 format")
- **Avoid** abstract words — be concrete and visual
- **For Seedance:** emphasize "UGC-style", "authentic", "social media content"
- **For Veo 3:** emphasize "cinematic", "photorealistic", "professional production"
- **For Kling 3.0:** emphasize "product showcase", "consistent subject", "multi-angle"
- **Max prompt length:** 500 characters for best results

---

## Output Format

For each generated clip:

```
## [Scene Name / Timestamp] — [Model] — [Tier]

**Model:** Seedance 2.0 / Veo 3 / Kling 3.0
**Render Tier:** Draft / Final
**Duration:** [X]s
**Aspect Ratio:** [ratio]
**File Name:** [brand]-[platform]-clip-[scene]-v[N]-[tier].mp4

### Prompt Used
[Exact prompt sent to the model]

### Generated Video
[Video URL returned by Kie.ai]

### Thumbnail Frame
[Thumbnail/poster frame URL if available]

### Production Notes
[Any issues, retry notes, or direction for the next revision]
```

**Close with a clip inventory table:**

| Scene | Model | Duration | Tier | Video URL | Status |
|-------|-------|----------|------|-----------|--------|
| Scene 1 — Hook | Seedance 2.0 | 5s | Draft | [url] | ✅ |
| Scene 2 — Problem | Seedance 2.0 | 8s | Draft | [url] | ✅ |
| ... | ... | ... | ... | ... | ... |

---

## Reference Files

- `references/video-specs.md` — Model capabilities, limits, pricing, and platform requirements
- `references/example-output.md` — Complete example for a VaultSync TikTok campaign (3 scenes, draft tier)
