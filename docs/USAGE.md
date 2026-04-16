# StackdMedia Plugin — Documentation & Usage Guide

> **Version:** 0.1.0 · **Author:** Audee Velasco · **Repo:** [adooylabs/stackmedia-plugin](https://github.com/adooylabs/stackmedia-plugin)

The StackdMedia plugin turns Claude Code into a full UGC content creation studio. It provides **17 AI skills** and **1 orchestration agent** that cover every stage of a paid-UGC campaign — from client onboarding through post-campaign reporting.

---

## Table of Contents

1. [Installation](#installation)
2. [Quick Start](#quick-start)
3. [Plugin Architecture](#plugin-architecture)
4. [Complete Skill Reference](#complete-skill-reference)
5. [User Flows](#user-flows)
   - [Flow 1: Full Campaign (End-to-End)](#flow-1-full-campaign-end-to-end)
   - [Flow 2: Quick Script Generation](#flow-2-quick-script-generation)
   - [Flow 3: Multi-Platform Expansion](#flow-3-multi-platform-expansion)
   - [Flow 4: Creator Management](#flow-4-creator-management)
   - [Flow 5: Post-Campaign Review](#flow-5-post-campaign-review)
6. [The Content Pipeline](#the-content-pipeline)
7. [Platform Reference](#platform-reference)
8. [Brand Input Schema](#brand-input-schema)
9. [Tips & Best Practices](#tips--best-practices)

---

## Installation

```bash
# Step 1: Add the marketplace
claude plugin marketplace add adooylabs/stackmedia-plugin

# Step 2: Install the plugin
claude plugin install stackdmedia@adooylabs
```

After installation, restart Claude Code. All 16 skills activate automatically based on your prompts.

---

## Quick Start

### "I just want a TikTok script"

```
Write a TikTok script for VaultSync, a password manager that auto-fills
across devices. Target: tech-savvy millennials who reuse passwords.
Campaign goal: app installs. Give me 3 variations.
```

Claude uses `script-tiktok` automatically — no setup needed.

### "I want the full pipeline"

```
Run the full content pipeline for VaultSync.
Here's the brand info: [paste BrandInputs JSON]
```

Claude uses the `content-creator` agent to orchestrate all skills in sequence.

### "I have a brief already"

```
Here's my creative brief: [paste brief]
Write scripts for TikTok, Instagram, and YouTube Shorts — 2 variations each.
Then storyboard the top-scoring one.
```

Claude runs the script skills in parallel, evaluates them, and storyboards the winner.

---

## Plugin Architecture

```
stackdmedia/
├── agents/
│   └── content-creator       ← Orchestrates the full pipeline
└── skills/
    ├── client-intake          ← Phase 1: Intake & Research
    ├── brand-voice-extractor
    ├── trend-research
    ├── generate-brief         ← Phase 2: Content Creation
    ├── script-tiktok
    ├── script-instagram
    ├── script-youtube-shorts
    ├── script-youtube-long
    ├── script-linkedin
    ├── generate-assets
    ├── generate-video
    ├── storyboard
    ├── evaluate-content       ← Phase 3: Review & Distribution
    ├── creator-match
    ├── creator-feedback
    ├── repurpose-content
    └── campaign-report
```

---

## Complete Skill Reference

### Phase 1: Intake & Research

| Skill | What It Does | Trigger Phrases |
|-------|-------------|-----------------|
| **client-intake** | Structures raw client info (discovery calls, forms, emails) into a campaign-ready intake document | "process this client intake", "structure this brand info", "new client onboarding for [brand]" |
| **brand-voice-extractor** | Extracts voice pillars, vocabulary rules, and tone guidelines from brand materials | "extract brand voice from [materials]", "analyze this brand guide", "what's the voice for [brand]" |
| **trend-research** | Researches current platform trends, hook formats, and competitor benchmarks | "research TikTok trends for [category]", "what's trending in [niche]", "hook audit for [platform]" |

### Phase 2: Content Creation

| Skill | What It Does | Trigger Phrases |
|-------|-------------|-----------------|
| **generate-brief** | Transforms brand inputs into a structured creative brief with hook strategies and platform notes | "generate a brief for [brand]", "create a creative brief", "brief this campaign" |
| **script-tiktok** | Writes TikTok scripts (15-60s, sweet spot 21-34s) with timestamped scenes, captions, and director notes | "write a TikTok script", "TikTok ad for [product]", "3 TikTok variations" |
| **script-instagram** | Writes Instagram Reels/feed scripts (15-90s) with cover frame concepts and cross-post recommendations | "write an Instagram script", "Instagram Reels for [product]", "IG ad variations" |
| **script-youtube-shorts** | Writes YouTube Shorts scripts (up to 60s, sweet spot 30-45s) with thumbnail concepts | "write a YouTube Shorts script", "Shorts ad for [product]" |
| **script-youtube-long** | Writes long-form YouTube scripts (2-15 min) with SEO packages, chapter lists, and thumbnail concepts | "write a YouTube script", "long-form YouTube for [product]", "YouTube review video" |
| **script-linkedin** | Writes LinkedIn video scripts in Sponsored Ad (15-30s) or Thought Leadership (2-5 min) format | "write a LinkedIn script", "LinkedIn video for [product]", "B2B video ad" |
| **generate-assets** | Generates images via Kie.ai Nano Banana (draft: 2K/$0.02, final: 4K/$0.04) and uploads to Canva for 9 asset types (thumbnails, carousels, covers, banners, etc.) | "generate visual assets", "create Instagram post designs", "YouTube thumbnail specs" |
| **generate-video** | Generates AI video footage for specific posts or shorts that need it — Seedance 2.0 for drafts, Veo 3 for final production quality | "generate video for this scene", "create AI video for this post", "I need a video clip for this short" |
| **storyboard** | Converts any script into a scene-by-scene visual storyboard with shot types, camera angles, and production notes | "storyboard this script", "create a storyboard", "shot list for this script" |

### Phase 3: Review & Distribution

| Skill | What It Does | Trigger Phrases |
|-------|-------------|-----------------|
| **evaluate-content** | Scores scripts on a 7-criterion rubric (/70). Pass threshold: 42 | "evaluate this script", "score these variations", "quality check this content" |
| **creator-match** | Matches creator profiles to campaigns using a 4-dimension scoring framework (/100) | "match creators to this brief", "evaluate these creator profiles", "creator hiring spec" |
| **creator-feedback** | Translates evaluation scores into actionable, human-readable feedback for creators | "give feedback on this script", "creator revision notes", "feedback for round 2" |
| **repurpose-content** | Adapts scripts across platforms or extracts short-form clips from long-form content | "repurpose this for Instagram", "extract Shorts from this YouTube script", "adapt for LinkedIn" |
| **campaign-report** | Generates post-campaign performance reports with recommendations for the next campaign | "generate campaign report", "post-campaign summary for [brand]", "performance review" |

---

## User Flows

### Flow 1: Full Campaign (End-to-End)

**When to use:** You're starting a new campaign from scratch for a client.

**Steps:**

```
Step 1 → client-intake
         "Process this client intake for VaultSync: [raw info]"
         Output: Structured intake document

Step 2 → brand-voice-extractor
         "Extract brand voice from this guide: [brand materials]"
         Output: Voice pillars, vocabulary, tone rules

Step 3 → trend-research
         "Research TikTok and Instagram trends for password managers"
         Output: Trending hooks, formats to avoid, competitor audit

Step 4 → generate-brief
         "Generate a creative brief using this intake and voice doc"
         Output: Full creative brief with hook strategies

Step 5 → script-tiktok / script-instagram / script-* (parallel)
         "Write 3 TikTok variations and 2 Instagram variations from this brief"
         Output: Platform-specific scripts with director notes

Step 6 → generate-assets (parallel with scripts)
         "Generate Instagram post, YouTube thumbnail, and TikTok cover specs"
         Output: Canva-ready design specifications

Step 7 → evaluate-content
         "Score all script variations"
         Output: Score table (42+ = PASS), top 3 improvements

Step 8 → storyboard (for passing scripts)
         "Storyboard the top-scoring TikTok variation"
         Output: Scene-by-scene shot list with production notes

Step 9 → creator-match
         "Match creators to this brief. Here are 5 profiles: [profiles]"
         Output: Scored creator recommendations

Step 10 → creator-feedback (after creator submits)
          "Give feedback on this creator's first draft"
          Output: What's working, must-fix, line notes

Step 11 → campaign-report (after campaign runs)
          "Generate performance report. Data: [metrics]"
          Output: Executive summary, top creatives, next-campaign recs
```

**Shortcut:** Say *"Run the full content pipeline for [brand]"* to trigger the `content-creator` agent, which orchestrates steps 1-8 automatically.

---

### Flow 2: Quick Script Generation

**When to use:** You already know what you want — just need scripts fast.

```
Step 1 → generate-brief (or skip if you have one)
         "Generate a brief for NightOwl Coffee targeting remote workers on TikTok"

Step 2 → script-tiktok
         "Write 3 TikTok scripts from this brief. Hook preference: relatable pain"

Step 3 → evaluate-content (optional)
         "Score these scripts"

Done. Three scripts ready for production in under 2 minutes.
```

**Pro tip:** You can skip `generate-brief` entirely — just provide enough context in your script prompt:

```
Write 3 TikTok scripts for NightOwl Coffee, a cold brew delivery subscription.
Target: remote workers who crash at 2pm. Goal: trial signups.
Tone: witty, self-deprecating. Hook preference: relatable pain.
```

---

### Flow 3: Multi-Platform Expansion

**When to use:** You have a script for one platform and want to expand to others.

```
Option A: Repurpose existing script
         "Repurpose this TikTok script for Instagram and LinkedIn"
         → repurpose-content adapts tone, timing, and format per platform

Option B: Generate fresh per platform
         "Write scripts for all 5 platforms from this brief — 2 variations each"
         → Claude runs all 5 script skills and outputs 10 total scripts

Option C: Extract clips from long-form
         "Extract 3 YouTube Shorts clips from this long-form YouTube script"
         → repurpose-content identifies best moments with timestamps
```

---

### Flow 4: Creator Management

**When to use:** You need to find, brief, and manage UGC creators.

```
Step 1 → creator-match (Criteria mode)
         "Create a creator hiring spec for this brief"
         Output: Ideal creator profile, platform requirements, audience match

Step 2 → creator-match (Evaluate mode)
         "Score these 5 creator profiles against the brief"
         Output: Ranked list with scores, recommendations, conditions

Step 3 → [Creator produces content]

Step 4 → evaluate-content
         "Score this creator's submitted script"
         Output: 7-criterion score, PASS/DOES NOT PASS

Step 5 → creator-feedback
         "This is revision round 1. Give feedback on this submission"
         Output: Structured feedback with specific line notes

Step 6 → [Creator revises] → Repeat steps 4-5 until PASS

Step 7 → storyboard
         "Storyboard the approved script for production"
         Output: Shot list, production notes, equipment list
```

---

### Flow 5: Post-Campaign Review

**When to use:** Campaign has run, you have performance data.

```
Step 1 → campaign-report
         "Generate a campaign report for VaultSync Q1.
          Goals: 500K views, 2% CTR, 1000 app installs.
          Actual: 620K views, 2.4% CTR, 1,340 installs.
          Top creator: @techsarah (340K views).
          Lowest: @gadgetguy (45K views)."
         Output: Executive summary, performance analysis, creator rebooking recs,
                 next-campaign recommendations

Step 2 → trend-research (prep for next campaign)
         "Research what changed in TikTok trends since our last campaign"
         Output: Updated trend report to inform the next brief
```

---

## The Content Pipeline

The plugin follows a linear pipeline with optional side paths:

```
┌─────────────────── PHASE 1: INTAKE & RESEARCH ───────────────────┐
│                                                                    │
│  client-intake ──→ brand-voice-extractor ──→ trend-research       │
│  (raw info)        (voice doc)               (trend report)        │
│                                                                    │
└────────────────────────────┬───────────────────────────────────────┘
                             │
                             ▼
┌─────────────────── PHASE 2: CONTENT CREATION ────────────────────┐
│                                                                    │
│                      generate-brief                                │
│                           │                                        │
│              ┌────────────┼────────────┐                          │
│              ▼            ▼            ▼                           │
│        script-tiktok  script-*   generate-assets                  │
│              │            │       (Kie.ai Nano Banana)             │
│              └────────────┼────────────┘                          │
│                           ▼                                        │
│                      storyboard                                    │
│                           │                                        │
│                           ▼                                        │
│                    generate-video  ← on-demand only               │
│                  (Kie.ai Seedance/Veo 3, specific scenes)          │
│                                                                    │
└────────────────────────────┬───────────────────────────────────────┘
                             │
                             ▼
┌─────────────────── PHASE 3: REVIEW & DISTRIBUTION ───────────────┐
│                                                                    │
│  evaluate-content ──→ creator-feedback ──→ [creator revises]      │
│       │                                        │                   │
│       │                                        ▼                   │
│       │                                   evaluate-content (loop)  │
│       │                                                            │
│  creator-match        repurpose-content       campaign-report      │
│  (find creators)      (expand platforms)      (post-campaign)      │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

**Key decision points:**
- Already have a brief? Skip straight to `script-*`
- Already have scripts? Skip to `storyboard` or `evaluate-content`
- Need multiple platforms? Use `repurpose-content` or run script skills in parallel
- Score below 42/70? Route through `creator-feedback` → revision loop
- Specific post needs AI video footage? Use `generate-video` for that scene only — not the full campaign

---

## Platform Reference

| Platform | Skill | Duration | Orientation | Sound | Sweet Spot |
|----------|-------|----------|-------------|-------|------------|
| TikTok | `script-tiktok` | 15-60s | 9:16 vertical | ON | 21-34s |
| Instagram | `script-instagram` | 15-90s | 9:16 vertical | OFF (captions) | 15-30s |
| YouTube Shorts | `script-youtube-shorts` | Up to 60s | 9:16 vertical | ON | 30-45s |
| YouTube Long | `script-youtube-long` | 2-15 min | 16:9 landscape | ON | 2-5 min |
| LinkedIn | `script-linkedin` | 15s-5 min | 16:9 or 1:1 | OFF (captions) | 15-30s (ads), 2-5 min (thought leadership) |

### Hook Types by Platform

**All platforms support:**
- Curiosity Gap — *"I can't believe no one talks about this..."*
- Relatable Pain — *"POV: you just forgot your password... again"*
- Bold Claim — *"This app saved me 4 hours a week"*
- POV/Identity — *"Things only [audience] understand"*
- Number-Based — *"3 reasons you need this"*

**TikTok adds:** Contrarian, Story/Confession
**Instagram adds:** Aesthetic Open (visual-first hook)
**YouTube Long adds:** Promise Hook, Myth Bust, Transformation
**LinkedIn adds:** Business Outcome, Credibility Opener, Social Proof Lead

---

## Brand Input Schema

The `generate-brief` skill accepts this JSON structure:

```json
{
  "brandName": "VaultSync",
  "productDescription": "Cross-device password manager with zero-knowledge encryption",
  "problemItSolves": "Password reuse, account breaches, login friction across devices",
  "targetAudience": "Tech-savvy millennials (25-35) who work across multiple devices",
  "campaignGoal": "Drive app installs via TikTok and Instagram",
  "primaryKPI": "Cost per install (target: <$3.50)",
  "platforms": ["tiktok", "instagram", "youtube-shorts"],
  "brandTone": "Confident, witty, technically credible but never condescending",
  "topFeatures": [
    "One-tap autofill across all devices",
    "Zero-knowledge encryption",
    "Breach monitoring with real-time alerts"
  ],
  "keyDifferentiator": "Only password manager with cross-device autofill under 200ms",
  "approvedClaims": "200ms autofill, zero-knowledge encryption, 50M+ passwords secured",
  "offLimitsClaims": "No fear-mongering, no competitor bashing, no 'unhackable' claims",
  "proofPoints": "TechRadar Editor's Choice 2026, 4.8-star App Store rating",
  "brandVoice": "[optional — output from brand-voice-extractor]"
}
```

**Required fields:** brandName, productDescription, problemItSolves, targetAudience, campaignGoal

**Everything else is optional** — Claude will still generate a usable brief with just the required fields.

---

## Kie.ai Integration

The `generate-assets` and `generate-video` skills use [Kie.ai](https://kie.ai) — a unified AI generation API — to produce actual images and videos instead of text specs.

### Setup

1. Get a Kie.ai API key at [kie.ai](https://kie.ai)
2. Add the MCP server to Claude Code:
   ```json
   {
     "mcpServers": {
       "kie-ai": {
         "command": "npx",
         "args": ["-y", "@felores/kie-ai-mcp-server"],
         "env": { "KIE_AI_API_KEY": "your-key-here" }
       }
     }
   }
   ```
3. Verify with `/mcp` — you should see Kie.ai tools available

### Image Generation (generate-assets)

| Tier | Model | Resolution | Cost | Use Case |
|------|-------|-----------|------|----------|
| `draft` | Nano Banana 2K | 2048px | $0.02/image | Client previews, iteration |
| `final` | Nano Banana 4K | 4096px (upscaled) | $0.04/image | Production — auto-uploads to Canva |

### Video Generation (generate-video)

| Tier | Default Model | Speed | Cost | Use Case |
|------|--------------|-------|------|----------|
| `draft` | Seedance 2.0 | 30-40s | ~$0.05-0.15/clip | Client previews, fast iteration |
| `final` | Veo 3 | ~2-3 min | ~$0.40/8s | Production — photorealism + native audio |

**Model override:** Add `model_override: kling3` for multi-shot product showcase videos.

---

## Asset Types (generate-assets)

| Asset | Dimensions | Use Case |
|-------|-----------|----------|
| Instagram Post | 1080×1080 or 1080×1350 | Feed post, ad creative |
| Instagram Carousel | 1080×1080 (multi-page) | Educational/product showcase |
| Instagram Story | 1080×1920 | Story ad, swipe-up CTA |
| TikTok Cover Frame | 1080×1920 | Video thumbnail on profile grid |
| YouTube Thumbnail | 1280×720 | Video thumbnail (search + browse) |
| YouTube Channel Art | 2560×1440 | Channel banner |
| LinkedIn Post | 1200×627 | Feed image, sponsored content |
| Ad Banners | 4 sizes (1200×628, 1080×1080, 1080×1920, 300×250) | Paid media across networks |
| Email Header | 600×200 | Newsletter/campaign email |

---

## Tips & Best Practices

### Getting the Best Results

1. **More context = better output.** The more you provide in BrandInputs, the sharper the scripts. Even "optional" fields like `brandTone` and `proofPoints` significantly improve quality.

2. **Use hook preferences strategically.** If you know your audience responds to social proof, set `hookPreference: "bold-claim"`. Use `"any"` to let Claude choose the best mix.

3. **Always evaluate before delivering.** Run `evaluate-content` on every script — even ones that feel good. The 7-criterion rubric catches blind spots.

4. **Generate 3 variations, not 1.** More variations = more creative range. The evaluation skill will identify the strongest one.

5. **Use the agent for new campaigns.** Say *"Run the full content pipeline"* — the `content-creator` agent handles the orchestration so you can focus on reviewing output.

### Common Patterns

| You want to... | Do this |
|----------------|---------|
| Start from zero with a new client | `client-intake` → `brand-voice-extractor` → `generate-brief` |
| Get scripts fast | Paste context directly into `script-*` (skip brief) |
| Cover all platforms | Run all 5 `script-*` skills from one brief |
| Adapt one script everywhere | `repurpose-content` on your best script |
| Find the right creators | `creator-match` in Criteria mode for hiring spec |
| Quality-check before delivery | `evaluate-content` → `creator-feedback` if needed |
| Report results to client | `campaign-report` with performance data |
| Create visual assets | `generate-assets` with brand colors and campaign headline |
| A post needs AI-generated video footage | `generate-video` for that specific storyboard scene |

### What NOT to Do

- **Don't skip the brief for multi-platform campaigns.** When you need scripts across 3+ platforms, the brief ensures consistent messaging.
- **Don't send scripts scoring below 42/70.** The threshold exists for a reason — sub-42 scripts have structural issues.
- **Don't use `repurpose-content` for vastly different platforms.** TikTok→Instagram works great. TikTok→YouTube Long does not — generate fresh for long-form.
- **Don't paste the same prompt to multiple script skills.** Each skill is platform-optimized. Let the brief carry the shared context; each skill handles the platform-specific adaptation.

---

## Evaluation Criteria (evaluate-content)

| # | Criterion | What It Measures | Max Score |
|---|-----------|-----------------|-----------|
| 1 | Hook Strength | Does the first 3 seconds stop the scroll? | /10 |
| 2 | Storytelling | Is there a clear arc (problem → solution → proof)? | /10 |
| 3 | Script Naturalness | Does it sound like a real person, not an ad? | /10 |
| 4 | Production Feasibility | Can a solo creator actually film this? | /10 |
| 5 | Brand Integration | Is the product woven in naturally? | /10 |
| 6 | Platform Awareness | Does it follow platform-specific conventions? | /10 |
| 7 | Creative Direction | Is there a fresh angle, not just a template? | /10 |

**PASS:** 42/70+ · **DOES NOT PASS:** Below 42/70

---

## Creator Scoring (creator-match)

| Dimension | Weight | What It Measures |
|-----------|--------|-----------------|
| Demographic Alignment | /25 | Creator's audience matches target demo |
| Content Style Fit | /25 | Creator's aesthetic matches brand tone |
| Platform Performance | /25 | Engagement rate, views, growth trajectory |
| Brand Safety | /25 | No controversies, aligned values, professionalism |

**RECOMMEND:** 80+ · **CONDITIONAL:** 60-79 · **DO NOT RECOMMEND:** Below 60

---

*Built with Claude Code by [StackdMedia](https://github.com/adooylabs/stackmedia-plugin)*
