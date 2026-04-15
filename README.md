# StackdMedia Plugin

UGC ad content creation toolkit for Claude Code. Generates creative briefs, platform-optimized scripts, and production storyboards for TikTok, Instagram, YouTube Shorts, YouTube long-form, and LinkedIn.

## Installation

```bash
/plugin install github:StackdApps/stackdmedia-plugin
```

## Skills

| Skill | Trigger |
|-------|---------|
| `generate-brief` | "generate a brief for [brand/product]" |
| `script-tiktok` | "write a TikTok script" / "TikTok ad for [product]" |
| `script-instagram` | "write an Instagram script" / "Instagram Reels ad for [product]" |
| `script-youtube-shorts` | "write a YouTube Shorts script" / "Shorts ad for [product]" |
| `script-youtube-long` | "write a YouTube script" / "long-form YouTube ad for [product]" |
| `script-linkedin` | "write a LinkedIn script" / "LinkedIn video ad for [product]" |
| `storyboard` | "create a storyboard" / "storyboard this script" |

## Workflow

1. Start with `generate-brief` — provide brand inputs as JSON
2. Use the output brief with any script skill to generate platform-specific variations
3. Run `storyboard` on any generated script for production-ready shot lists
4. Request multiple variations per run (e.g. "give me 3 TikTok variations")

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
