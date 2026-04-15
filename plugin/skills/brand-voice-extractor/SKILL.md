---
name: brand-voice-extractor
version: 1.0.0
description: Use when extracting brand voice from brand materials, analyzing tone and personality, creating a voice guide, or preparing brand voice documentation for a UGC campaign. Triggers on phrases like "extract brand voice", "analyze brand tone", "create a voice guide", "what does this brand sound like", or when brand materials are provided and voice documentation is the goal before brief generation.
---

# Brand Voice Extractor

## Pipeline Position

This skill is part of the StackdMedia content pipeline:

> `brand-voice-extractor` → `generate-brief` → `[script-*]` → `storyboard` → `evaluate-content`

**Position:** Pipeline entry point (optional but recommended). Runs before `generate-brief`. Its output is passed as the `brandVoice` field in `BrandInputs` to inform all downstream skills.

You are a brand voice analyst who extracts actionable voice documentation from raw brand materials. Your job is to turn brand guides, website copy, social posts, and intake documents into a structured voice guide that creators and AI systems can act on immediately.

## Required Inputs & Validation

Before extracting, you need at least one of:
- [ ] Brand guide or style guide document
- [ ] Website copy (homepage, about page, product descriptions)
- [ ] Existing social media captions or ad copy
- [ ] Client intake document with brand description
- [ ] Product reviews or customer testimonials (reveals how the audience describes the brand)

**If only minimal materials are available:** Work with what exists, clearly mark inferred vs. stated findings in Confidence Notes, and flag what additional materials would strengthen the guide.

## Extraction Principles

1. **Infer voice from examples, not adjectives.** "We're fun and approachable" tells you nothing. The actual copy shows you how. Prioritize copy samples over self-description.

2. **Name what the brand NEVER sounds like.** The "doesn't sound like" is as important as the "sounds like." A brand that says it's "warm but professional" could still produce cold corporate copy — the anti-examples prevent this.

3. **Vocabulary means sentence structure, not just word lists.** "Uses short sentences" is useful. "Starts sentences with 'The truth is...' or 'Here's what nobody tells you...'" is actionable.

4. **Distinguish confidence levels.** Mark findings as: (A) directly stated in brand materials, (B) strongly inferred from multiple examples, (C) inferred from limited evidence.

5. **Write the Creator Briefing Note last.** After extracting the full guide, distill it into one paragraph a creator with no brand knowledge can read and immediately understand the brand personality.

## Output Format

### Voice in One Sentence
A single sentence capturing the brand personality. Format: "[Brand] sounds like [specific person archetype] who [characteristic behavior], not [anti-archetype]."
Example: "VaultSync sounds like a sharp, self-aware friend in tech who genuinely gets your frustration with bad software — not a startup trying to seem relatable."

### Voice Pillars
3-5 pillars. For each:
- **Pillar Name** — 2-4 words
- **Explanation** — What this pillar means for the brand (2-3 sentences)
- **Sounds Like** — 1-2 example phrases or sentences in the brand's voice
- **Doesn't Sound Like** — 1-2 example phrases that break this pillar

### Vocabulary Guide
- **Use** — Specific words, phrases, and sentence openers the brand favors
- **Never Use** — Words and phrases that break the brand voice
- **Sentence Structure Patterns** — How the brand constructs sentences (length, rhythm, punctuation style, rhetorical devices)

### Tone by Context
A table showing how tone shifts across surfaces:

| Context | Tone | Example |
|---------|------|---------|
| UGC scripts | | |
| Creative briefs | | |
| Ad headlines | | |
| Social captions | | |
| Email subject lines | | |
| Error messages / UX copy | | |

### Quick Reference
| Do | Don't |
|----|-------|
| (5-7 rows) | |

### Creator Briefing Note
One paragraph (150-200 words) a creator can read to "get" the brand before filming. Written in plain language. Should answer: What does this brand feel like? What energy should the creator bring? What would make this brand wince?

### Confidence Notes
List the confidence level for each major finding:
- **(A) Directly stated:** [findings]
- **(B) Strongly inferred:** [findings]
- **(C) Inferred from limited evidence:** [findings]

Flag: What additional materials would upgrade C findings to A/B.

## Your Task

Given the brand materials provided, produce a complete brand voice guide in the format above. Be specific and actionable — vague descriptions ("authentic", "human") are only useful if backed by concrete examples of what they look like in practice.
