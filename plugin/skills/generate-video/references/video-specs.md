# Video Generation Specifications

Technical specs, model capabilities, pricing, and platform requirements for AI video generation via Kie.ai.

---

## Model Comparison

| Spec | Seedance 2.0 | Veo 3 | Kling 3.0 |
|------|-------------|-------|-----------|
| Provider | ByteDance | Google DeepMind | Kuaishou |
| Best for | UGC, human video, speed | Cinematic, native audio | Multi-shot, product |
| Generation speed | 30-40s | 45-60s | 45-60s |
| Native audio | Yes (phoneme lip sync) | Yes (full audio gen) | No |
| Max duration | 10s | 8s | 15s (multi-shot) |
| Resolutions | Up to 2K | Up to 4K | Up to 4K |
| Languages (lip sync) | 8+ | English (primary) | Limited |
| Price via Kie.ai | ~$0.05-0.15/video | ~$0.40/video (8s) | Competitive |
| Quality rank (overall) | #1 image-to-video | #1 photorealism | #1 multi-shot |

---

## Platform Requirements

| Platform | Aspect Ratio | Duration | Notes |
|----------|-------------|----------|-------|
| TikTok | 9:16 | 15-60s | Multiple clips stitched in editing |
| Instagram Reels | 9:16 | 15-90s | Sweet spot: 15-30s |
| YouTube Shorts | 9:16 | Up to 60s | Sweet spot: 30-45s |
| YouTube Long | 16:9 | 2-15 min | Multiple clips + b-roll |
| LinkedIn | 16:9 or 1:1 | 15s-5 min | B2B tone essential |

Note: AI-generated clips are typically 5-15s. Final videos are assembled from multiple clips in post-production.

---

## Pricing Reference (via Kie.ai)

| Model | Duration | Approx. Cost |
|-------|----------|-------------|
| Seedance 2.0 | 5s | ~$0.05 |
| Seedance 2.0 | 8s | ~$0.08 |
| Seedance 2.0 | 10s | ~$0.12 |
| Veo 3 | 8s | ~$0.40 |
| Nano Banana 2K (image) | — | $0.02 |
| Nano Banana 4K (image) | — | $0.04 |

Check [kie.ai/pricing](https://kie.ai/pricing) for current rates.

---

## Input Types

### Text-to-Video
- Provide a descriptive scene prompt
- Best for: abstract concepts, product demos, lifestyle scenarios
- No reference image needed

### Image-to-Video
- Provide a starting frame (generated via Nano Banana or provided by client)
- Best for: animating product shots, bringing storyboard frames to life
- Seedance 2.0 is the strongest image-to-video model (top leaderboard as of Q1 2026)

### Storyboard-to-Video
- Break each scene into individual clips
- Use Shot Type, Movement, Subject, and Action fields to construct prompts
- Most predictable results — storyboard constrains the generation

---

## Quality Tips

### For Seedance 2.0
- Works best with clear, specific action descriptions
- Include creator demographics (age, style, energy)
- Specify "UGC-style" or "authentic social media content" for natural feel
- Phoneme lip sync works best when dialogue is included in the prompt

### For Veo 3
- Include audio intent in the prompt (Veo 3 generates synchronized audio)
- Describe ambient sounds, music energy, and dialogue tone
- Use cinematic language: "golden hour lighting", "shallow depth of field", "slow push in"
- Best results with photorealistic, commercial-quality descriptions

### For Kling 3.0
- Specify "consistent subject across multiple angles" for product showcases
- Use for 3-15 second multi-shot sequences
- Include brand colors in product description for better consistency
