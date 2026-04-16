# StackdMedia Plugin

UGC ad content creation toolkit for Claude Code. Generates creative briefs, platform-optimized scripts, production storyboards, visual assets, and AI video footage for TikTok, Instagram, YouTube Shorts, YouTube long-form, and LinkedIn.

## Installation

### Option 1: Install via Claude Code (recommended)

```bash
# Step 1: Add the marketplace
claude plugin marketplace add adooylabs/stackmedia-plugin

# Step 2: Install the plugin
claude plugin install stackdmedia@adooylabs
```

Restart Claude Code after installation. All 17 skills activate automatically based on your prompts.

### Option 2: Install from GitHub directly

```bash
/plugin install github:adooylabs/stackmedia-plugin
```

### Option 3: Install locally (for development)

```bash
# Clone the repo
git clone git@github.com:adooylabs/stackmedia-plugin.git ~/.claude/plugins/local/stackdmedia

# Reload plugins in Claude Code
/plugin reload
```

> **Full documentation:** See [`docs/USAGE.md`](docs/USAGE.md) for complete workflow guides, user flows, and platform reference.

## Skills

| Skill | Trigger |
|-------|---------|
| `client-intake` | "process this client intake" / "new client onboarding for [brand]" |
| `brand-voice-extractor` | "extract brand voice" / "analyze this brand guide" |
| `trend-research` | "research TikTok trends for [category]" / "what's trending in [niche]" |
| `generate-brief` | "generate a brief for [brand/product]" |
| `script-tiktok` | "write a TikTok script" / "TikTok ad for [product]" |
| `script-instagram` | "write an Instagram script" / "Instagram Reels ad for [product]" |
| `script-youtube-shorts` | "write a YouTube Shorts script" / "Shorts ad for [product]" |
| `script-youtube-long` | "write a YouTube script" / "long-form YouTube ad for [product]" |
| `script-linkedin` | "write a LinkedIn script" / "LinkedIn video ad for [product]" |
| `generate-assets` | "generate visual assets" / "create Instagram post designs" |
| `generate-video` | "generate video for this scene" / "create AI video for this post" |
| `storyboard` | "create a storyboard" / "storyboard this script" |
| `evaluate-content` | "evaluate this script" / "score these variations" |
| `creator-match` | "match creators to this brief" / "creator hiring spec" |
| `creator-feedback` | "give feedback on this script" / "creator revision notes" |
| `repurpose-content` | "repurpose this for Instagram" / "extract Shorts from this YouTube script" |
| `campaign-report` | "generate campaign report" / "post-campaign summary for [brand]" |

## Workflow

1. **Intake** — `client-intake` → `brand-voice-extractor` → `trend-research`
2. **Brief** — `generate-brief` with brand inputs JSON
3. **Scripts** — any `script-*` skill for platform-specific variations (ask for 3 at once)
4. **Assets** — `generate-assets` for images (Kie.ai Nano Banana) / `generate-video` for AI video clips (Seedance 2.0 drafts, Veo 3 finals)
5. **Review** — `evaluate-content` (pass threshold: 42/70) → `storyboard` top scripts
6. **Distribute** — `creator-match`, `creator-feedback`, `repurpose-content`, `campaign-report`

**Full pipeline shortcut:** "Run the full content pipeline for [brand]" triggers the `content-creator` agent to orchestrate steps 1–5 automatically.

## Brand Input Schema (for generate-brief)

```json
{
  "brandName": "",
  "productDescription": "",
  "problemItSolves": "",
  "targetAudience": "",
  "campaignGoal": "",
  "primaryKPI": "",
  "platforms": ["tiktok", "instagram", "youtube-shorts", "youtube-long", "linkedin"],
  "brandTone": "",
  "topFeatures": [],
  "keyDifferentiator": "",
  "approvedClaims": [],
  "offLimitsClaims": [],
  "proofPoints": []
}
```
