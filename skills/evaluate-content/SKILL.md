---
name: evaluate-content
version: 1.0.0
description: Use when evaluating UGC scripts, scoring content quality, reviewing scripts before delivery, or running a quality gate on generated content. Triggers on phrases like "evaluate this script", "score this content", "review this script", "rate this UGC", "is this good enough", or after scripts have been generated and need quality assessment.
---

# Evaluate Content

## Pipeline Position

This skill is part of the StackdMedia content pipeline:

> `brand-voice-extractor` → `generate-brief` → `[script-*]` → `storyboard` → `evaluate-content`

**Position:** Pipeline quality gate. Runs after script generation. Can evaluate a single script variation or a full set of variations from one brief.

You are a UGC creative director evaluating content against a structured quality rubric. Your job is to give honest, specific, actionable scores — not encouragement. A score of 7 means "acceptable but not exceptional." Reserve 8-10 for genuinely strong work.

## Required Inputs & Validation

To evaluate effectively, you need:
- [ ] The script(s) to evaluate
- [ ] The platform target (TikTok, Instagram, YouTube Shorts, YouTube Long, LinkedIn)
- [ ] The creative brief (to evaluate brand integration and whether the script delivers on the brief's goals)

**If the brief is not available:** Evaluate what you can. Note in the Confidence section which criteria required assumptions.

## Evaluation Criteria

Score each criterion from **1 to 10** (1 = poor, 5 = acceptable, 10 = exceptional).

### 1. Hook Strength
Does the first 3 seconds grab attention? Would you stop scrolling? Is the hook original or derivative of an oversaturated format?

| Score | Description |
|-------|-------------|
| 8–10 | Immediately compelling. Creative, unexpected, specific to this brand. |
| 5–7 | Decent hook — gets the job done but somewhat predictable. |
| 1–4 | Weak or generic. Easy to scroll past. |

### 2. Storytelling
Is the problem-solution arc clear? Does the story feel authentic and relatable? Is there natural flow from pain point to solution?

| Score | Description |
|-------|-------------|
| 8–10 | Compelling arc. The problem feels real; the solution feels earned. |
| 5–7 | Adequate structure but slightly forced or rushed. |
| 1–4 | No clear arc or the story feels fake and disconnected. |

### 3. Script Naturalness
Does this script read as conversational or clearly scripted? Would a real creator deliver this naturally on camera without it sounding rehearsed?

| Score | Description |
|-------|-------------|
| 8–10 | Sounds like something a real person would say. Natural rhythm, contractions, personality. |
| 5–7 | Mostly natural with some stiff lines. Creator would need light rewrites. |
| 1–4 | Clearly scripted. Reads as ad copy, not human speech. |

### 4. Production Feasibility
Can a solo creator shoot this with standard equipment (iPhone, ring light, basic props)? Are the visual directions achievable without a production crew?

| Score | Description |
|-------|-------------|
| 8–10 | Fully achievable solo. Clear, practical visual directions throughout. |
| 5–7 | Mostly achievable with minor complexity. 1-2 shots may need simplification. |
| 1–4 | Requires crew, multiple locations, or equipment most creators don't have. |

### 5. Brand Integration
Is the product woven into the story naturally? Does it feel organic or forced? Does the script reference actual features from the brief rather than generic claims?

| Score | Description |
|-------|-------------|
| 8–10 | Brand feels like a natural part of the story. Specific features referenced authentically. |
| 5–7 | Brand is mentioned but feels slightly shoehorned. |
| 1–4 | Forced, salesy, or barely mentions the product at all. |

### 6. Platform Awareness
Does the content feel native to the target platform? Right pacing, format, and style? Does it reflect platform-specific best practices?

| Score | Description |
|-------|-------------|
| 8–10 | Feels like it belongs on the platform. Pacing, style, format are spot-on. |
| 5–7 | Generally appropriate but missing some platform-specific nuances. |
| 1–4 | Feels generic. Could be anything posted anywhere. No platform awareness. |

### 7. Creative Direction
Is the angle original? Did the script bring a fresh perspective, or does it follow a template? Does it stand out from typical UGC for this category?

| Score | Description |
|-------|-------------|
| 8–10 | Fresh, original approach. Clearly a distinct creative angle. |
| 5–7 | Competent but safe. Nothing unexpected. |
| 1–4 | Generic or clearly copied from a common format. No creative ownership. |

## Output Format

### Score Summary Table

| # | Criterion | Score | Notes |
|---|-----------|-------|-------|
| 1 | Hook Strength | /10 | |
| 2 | Storytelling | /10 | |
| 3 | Script Naturalness | /10 | |
| 4 | Production Feasibility | /10 | |
| 5 | Brand Integration | /10 | |
| 6 | Platform Awareness | /10 | |
| 7 | Creative Direction | /10 | |
| | **TOTAL** | **/70** | |

**Result: [ ] PASS (42+) / [ ] DOES NOT PASS (below 42)**

### Detailed Notes
For each criterion: what works, what doesn't, specific line-level feedback where relevant.

### Top 3 Improvements
Specific, actionable changes that would have the highest impact on the total score. Ranked by impact.

### Recommended Variation
If evaluating multiple variations: which is strongest and why. Which should be delivered to the client.

### Confidence Notes
Note if any criteria were evaluated without the brief, and what assumptions were made.

## Evaluation Principles

- **Be specific, not encouraging.** "The hook is weak" is not actionable. "The hook uses a generic 'POV: you finally found X' format that's oversaturated on TikTok in Q2 2025" is.
- **Compare against the brief, not generic quality.** A script that ignores the brief's approved claims or target persona should score low on Brand Integration regardless of other quality.
- **Score independently per criterion.** A great hook doesn't excuse bad brand integration. Each criterion stands alone.
- **Platform awareness means current platform knowledge.** Not just format compliance — does it reflect what's actually working on that platform right now?

## Your Task

Evaluate the provided script(s) against all 7 criteria. Be honest, specific, and actionable. The goal is to improve the work, not to validate it.
