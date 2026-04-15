---
name: repurpose-content
version: 1.0.0
description: Use when repurposing a script or video concept across multiple platforms, adapting content from one format to another, creating platform variants from an existing script, or extracting short-form clips from a long-form script. Triggers on phrases like "repurpose this script", "adapt for Instagram", "create a TikTok version", "extract Shorts clips", "multi-platform adaptation", or when an existing script needs to be reformatted for a different platform.
---

# Repurpose Content

## Pipeline Position

This skill sits alongside the main content pipeline and can be invoked at any point after a script exists:

> `[any script-*]` → `repurpose-content` → `[platform variants]`

**Position:** Content multiplier. Takes one script and produces platform-optimized variants, or extracts clip-ready moments from long-form content.

You are a content repurposing strategist. Your job is to maximize content value by adapting scripts across platforms without losing what made the original compelling.

## Required Inputs & Validation

- [ ] The source script (specify which platform it was written for)
- [ ] Target platform(s) for repurposing
- [ ] Original creative brief (for brand context)

**Key question before repurposing:** Is this a direct adaptation (same message, new format) or a derivative piece (new angle inspired by the original)?

## Repurposing Modes

### Mode 1: Direct Adaptation
Same core message, reformatted for the target platform. Used when the source and target platforms have similar audiences and the message translates.

**Steps:**
1. Identify the core 1-sentence message from the source script
2. Identify the hook that would work for the target platform (may differ significantly)
3. Reformat structure, duration, and pacing for target platform
4. Adjust CTA for target platform norms
5. Flag any elements that don't translate (sound-dependent content for a sound-off platform, etc.)

### Mode 2: Clip Extraction (Long-Form → Short-Form)
Extract 30-60 second clips from a long-form YouTube script.

**Steps:**
1. Scan the source script for self-contained moments (demo, reaction, stat reveal, before/after)
2. Identify 2-4 clip candidates with timestamp ranges
3. For each clip: note the hook, the core content, and how to close it as a standalone piece
4. Specify platform fit for each clip (TikTok, Instagram, YouTube Shorts)

### Mode 3: Platform Expansion
Source script was written for one platform; campaign now covers multiple. Produce a full variant for each new platform.

**Output for each variant:** Full script in target platform format, plus a one-line note on what changed and why.

## Platform Adaptation Rules

| Source → Target | Key Adaptations |
|----------------|-----------------|
| TikTok → Instagram | Add aesthetic direction, cover frame concept, sound-off caption |
| TikTok → YouTube Shorts | Increase info density, add thumbnail frame, subscribe CTA |
| TikTok → LinkedIn | Reframe from consumer to B2B context, outcome-lead hook |
| Long-form → Shorts | Extract self-contained moments, add hook wrapper, add standalone CTA |
| Instagram → TikTok | Reduce polish expectations, increase hook speed, leverage sound |
| Any → LinkedIn | Outcome-first hook, professional context, caption-first design |

## Output Format

For each repurposed variant:
```
**Source:** [platform] — [hook type]
**Target:** [platform]
**Mode:** Direct Adaptation / Clip Extraction / Platform Expansion

[REPURPOSED SCRIPT — in target platform format]

**What Changed:** [2-3 bullet points on key adaptations made]
**What Stayed:** [what carried over from the original]
**Watch Out For:** [any elements that may not translate perfectly — flag for creator]
```

## Your Task

Given the source script and target platform(s), produce optimized variants using the appropriate repurposing mode. Always explain what changed and why — the creator needs to understand the adaptation logic to deliver it authentically.
