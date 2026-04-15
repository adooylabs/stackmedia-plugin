# TikTok Ad Scripting Principles — Deep Reference

## Algorithm Behavior: What TikTok Rewards

TikTok's For You Page algorithm ranks content on four signals, in order of weight:

1. **Completion rate** — Did the viewer watch to the end? This is the single most important signal. A 30-second video watched fully beats a 60-second video abandoned at 15s. Optimize ruthlessly for completion.
2. **Shares** — The strongest intent signal. A share means the viewer associated the content with someone in their life. Design for the "I need to send this to X" moment.
3. **Saves** — High-intent engagement. Saves indicate utility — viewers expect to return. Tutorial-adjacent content and "reference" scripts earn saves.
4. **Comments** — Engagement, but lower weight than shares/saves. Comments matter for community signals and duet/stitch bait, not for raw distribution.

Likes are a vanity metric on TikTok. Script for completion and shares first.

## Retention Mechanics: Where Viewers Drop Off (and How to Stop It)

**Drop-off moments to defend against:**

- **0-2 seconds:** The hook window. If the first visual frame and first spoken word don't create a reason to stay, viewers are gone before the hook lands.
- **8-10 seconds:** First re-engagement checkpoint. Viewers who stayed through the hook begin to disengage if the "payoff" isn't developing. Insert a pattern interrupt here — a visual cut, a surprising statement, a text overlay reveal.
- **Mid-video (15-20s on a 30s video):** The "am I wasting my time?" moment. Viewers recalibrate. Keep an unresolved question alive through this window — don't resolve the core tension too early.
- **Final 3 seconds:** CTA drop-off. Many viewers close before the CTA. Move critical information (link in bio, product name) one beat earlier than feels natural.

**Pattern interrupt techniques:**
- Hard cut to a new angle or location
- Text overlay appearing mid-sentence
- A rhetorical question that resets attention ("And here's the part no one talks about...")
- A visual prop entering the frame
- B-roll cutaway and return

## Format-Native Patterns: What Feels Native vs. Ad-Like

**Native cues:**
- Creator talking directly to camera, handheld, slightly imperfect framing
- Real-world backgrounds (kitchen, desk, bedroom) — not clean white sets
- Filler language used deliberately ("honestly", "okay so", "like literally")
- Specific personal details ("my Tuesday morning routine", not "every morning")
- Visible skepticism before the payoff ("I didn't expect it to actually work")
- Text overlays in TikTok's native font weight and em-dash rhythm

**Ad-like cues that kill authenticity:**
- Professional lighting setups visible in frame
- Polished transitions or branded lower-thirds
- Opening with the brand name or product name
- Scripted-sounding sentences without natural rhythm breaks
- Overly clean diction — no stumbles, no "um", no breath pauses
- Closing on a brand logo or packshot

**The native test:** Read the script aloud. If it sounds like something someone would say to their phone camera while making coffee, it passes. If it sounds like it was approved by a legal team, rewrite it.

## What's Currently Oversaturated on TikTok

Avoid these patterns — they trigger skip behavior because viewers recognize them immediately:

- **Fake urgency:** "Only 3 left!", "This sale ends TONIGHT" — audiences are trained to ignore this
- **"I can't believe this worked"** — this phrase has become shorthand for paid content and is now a trust signal in reverse
- **Too-polished sets:** Bright studio lighting, branded backdrops, perfectly arranged product shots
- **The slow-zoom face reveal:** Opening with a dramatic zoom into the creator's face before saying anything
- **List-format scripts:** "5 reasons why..." feels like a blog post, not a conversation
- **Stacked hashtags in caption:** 20-30 hashtags signals low-quality content to the algorithm

## Platform Demographics

- **Primary audience:** 18-34 (largest active segment)
- **Highest purchasing intent:** 25-34 (disposable income + discovery-mode buying behavior)
- **B2C sweet spot:** Products under $100 with visible before/after or immediate utility
- **B2B consideration:** 25-40 small business owners, freelancers, solopreneurs — present on TikTok but require trust-building content over 3-5 exposures before conversion
- **Content consumption context:** Mostly mobile, vertical, often in transit or downtime — not a research mindset, an entertainment mindset. The product must feel like a discovery, not a purchase decision.

## Hook Testing Strategy

Always generate 3 hook variations using different hook mechanics. The lead variation should use the `hookPreference` from ScriptConfig. The other two should explore contrasting emotional registers:

- If lead is **Relatable Pain**, contrast with **Curiosity Gap** and **Story/Confession**
- If lead is **Bold Claim**, contrast with **Contrarian** and **Relatable Pain**
- If lead is **Curiosity Gap**, contrast with **Story/Confession** and **Number-Based**

Test hooks by reading just the first 8 words aloud. If the sentence doesn't create a reason to keep watching on its own, it's not a TikTok hook — it's a setup.

**Hook evaluation criteria:**
1. Does it create an unresolved tension?
2. Is it under 8 words spoken?
3. Does it speak to a specific person with a specific problem?
4. Would you pause your scroll to hear the rest?

## Caption Strategy

TikTok captions are read by the algorithm AND by viewers who tap to expand. Optimize for both.

- **Keep it under 150 characters** — captions truncate at ~100 characters in-feed; the rest is only seen on tap
- **Conversational tone** — write like you're texting, not posting
- **No hashtag stuffing** — 3-5 niche hashtags outperform 10 broad ones; the algorithm reads niche hashtags as stronger intent signals
- **Duet/stitch bait in caption** — "Tell me if this happened to you" or "Duet this if you've been here" drives engagement
- **Avoid clickbait in captions** — it increases click-throughs but tanks completion rate if the content doesn't match

**Hashtag selection hierarchy:**
1. One brand/product-specific hashtag
2. One problem/category hashtag (e.g., #smallbizowner, #morningroutine)
3. One broad discovery hashtag with traction (e.g., #fyp, #tiktokfinds) — use sparingly

## Sound Licensing Notes

- **Original audio** (creator voiceover over royalty-free or no music): Preferred for organic reach. TikTok's algorithm gives original audio distribution advantages and enables other creators to use the sound, extending reach.
- **Trending commercial music**: Use only with a TikTok Business Account using licensed tracks from the Commercial Music Library. Do not use trending sounds for paid ads without verifying licensing.
- **For branded/paid content**: Always use TikTok's Commercial Music Library or commission original audio. Trending sounds carry takedown risk for paid amplification.
- **Music volume for UGC ads**: 15-20% volume. Music is atmosphere, not the story. The voiceover carries the narrative.
