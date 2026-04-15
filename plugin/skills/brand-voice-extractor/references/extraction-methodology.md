# Brand Voice Extraction Methodology

A practical guide to reading brand materials and producing voice documentation that's actually usable.

---

## Reading Between the Lines of Brand Adjectives

Most brand briefs describe voice with adjectives: "authentic", "approachable", "bold", "human". These words are almost always useless as written — not because they're wrong, but because they're unresolved. "Authentic" describes a feeling, not a behavior. The job of extraction is to resolve the adjective into a behavior.

The technique: for every adjective in the brief, ask "what does that look like in a sentence?" and then "what's the opposite sentence that also fits that adjective but isn't what this brand means?"

- "Authentic" could mean unfiltered ("we messed this up and here's how") or it could mean storytelling ("here's the journey behind why we built this"). Both are authentic. They produce completely different copy.
- "Bold" could mean provocative ("most CRMs are garbage") or visually loud (big typography, short copy). A brand brief that says "bold" without examples is telling you almost nothing.
- "Human" almost always means "we don't want to sound like a robot" — which is a constraint, not a style guide.

When adjectives appear without examples, treat them as hypotheses to test against the actual copy, not as findings. If the copy is gentle and qualifies every claim, "bold" was aspirational, not actual. Note the gap. Document both the stated aspiration and the demonstrated reality. For AI downstream use, demonstrated reality is what matters.

---

## The Anti-Brand Audit

One of the most efficient ways to define a brand voice is to find three brands the client would hate being compared to, then reverse-engineer what to avoid.

The process:
1. Ask the client (or infer from materials): "Which brands in your space make you cringe?" or "Which brands do you think sound wrong for your audience?"
2. Identify the specific traits those brands share: the vocabulary, the sentence structure, the emotional register, the implicit assumptions about the reader.
3. Document those traits as explicit exclusions in the voice guide.

Why this works: brands know what they aren't more viscerally than what they are. A startup founder who says "we're not like Salesforce" is giving you a precise negative space. Salesforce sounds like: long sentences, heavy noun stacks, capability-first messaging, implied enterprise authority. Everything that's not that is now useful.

Common anti-brand categories:
- **The over-promiser** (brands that stack superlatives and guarantees): signals what confident understatement looks like for your client
- **The jargon brand** (heavy technical or MBA vocabulary): signals where to draw the plain-language line
- **The relatable-try-hard** (brands that perform personality through slang, memes, or forced casualness): signals how to stay genuine without performing genuineness

Document the anti-brand audit in the Confidence Notes section. It's supporting evidence, not a headline finding — but it sharpens the "Doesn't Sound Like" column considerably.

---

## Customer Reviews as Voice Mirror

Customer reviews are among the most underused inputs in brand voice extraction. When customers write unprompted about a product they love, they describe it using the language they wish the brand would use.

The phenomenon: buyers internalize brand messaging, then reflect it back in their own words. The result is a filtered, humanized version of the brand voice — stripped of corporate polish, translated into how real people talk.

How to use reviews:
- Collect 20-30 reviews from platforms where customers write freely (G2, Capterra, App Store, Amazon, Reddit threads)
- Look for repeated phrases, metaphors, and emotional descriptors — these are the words that stuck
- Note what problems customers describe before the solution: this reveals the pain language the brand should speak fluently
- Flag any phrases that appear in reviews AND in the brand's own copy: these are confirmed resonant terms

Specific things to look for:
- **Comparison phrases**: "It's like having a..." — customers use analogies freely. These become Voice in One Sentence candidates.
- **Before/after language**: "I used to spend hours on X, now..." — this is the story structure that converts.
- **Negative framing of alternatives**: "Unlike other tools that..." — confirms what the brand is positioned against.

Customer reviews are treated as (B) confidence evidence unless the brand has explicitly incorporated customer language into their own copy (which upgrades them to A).

---

## The Confidence Ladder (A/B/C) and Why It Matters for AI Downstream Use

Brand voice guides are only as reliable as the evidence behind them. When a voice guide is passed downstream to `generate-brief` and then to script generation, every uncertain finding multiplies in impact. A (C)-confidence vocabulary preference can produce scripts with entirely wrong tone if the AI treats it as settled fact.

The three levels:

**(A) Directly stated** — The brand's own materials explicitly describe this. A brand guide that says "never use exclamation marks" is an A finding. A tagline that demonstrates a specific sentence pattern is A.

**(B) Strongly inferred** — Multiple independent signals point in the same direction. If three different pieces of copy all use the same rhetorical structure, that's a B. If the website, a product video, and social posts all avoid passive voice, that's a B.

**(C) Inferred from limited evidence** — One signal, or a weak signal extrapolated broadly. An educated guess about vocabulary based on one page of copy is C.

Why this matters for AI use: downstream prompts should be weighted differently based on confidence level. A findings should be treated as constraints ("always do this"). B findings should be defaults ("prefer this unless context suggests otherwise"). C findings should be flagged as guidance ("this seems right but verify before deploying at scale").

When writing the voice guide, always close with a Confidence Notes section listing which findings are A, B, or C, and naming specifically what additional materials would upgrade C findings to higher confidence. This makes the guide honest about its own limitations — and protects creators and AI systems from acting on shaky inference as if it were fact.

---

## When to Ask for More Materials vs. Proceed

The default is to proceed with what you have and document the limitations clearly. Waiting for perfect materials usually means the guide never gets written.

Ask for more materials when:
- All findings would be C confidence (one weak source, nothing cross-referenced)
- The brand's stated voice and demonstrated copy are in direct conflict (e.g., they say "casual" but all copy is formal) — you need more samples to determine which is real
- The brief describes a specific audience but provides no copy targeting that audience (you can't infer tone without knowing who's being addressed)

Proceed with limitations documented when:
- You have at least one strong source (a brand guide, a set of copy samples, or a client intake with specific examples)
- You can produce A or B confidence findings for the core pillars even if peripheral vocabulary preferences are C
- Time constraints require a working guide now, with a revision planned after additional materials are gathered

In all cases: ship the guide with its confidence notes intact. A voice guide marked "C: vocabulary preferences unconfirmed — recommend reviewing 10 social captions before scripting" is far more useful than one that presents everything as certain, or one that was never written at all.
