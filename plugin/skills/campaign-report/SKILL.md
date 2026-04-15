---
name: campaign-report
version: 1.0.0
description: Use when generating a campaign performance report, summarizing UGC campaign results, analyzing what worked and what didn't, or preparing a client-facing summary of campaign outcomes. Triggers on phrases like "generate a campaign report", "summarize campaign results", "what worked in this campaign", "client report", or when a campaign has concluded and a performance summary is needed.
---

# Campaign Report

## Pipeline Position

This skill runs after campaign execution:

> `[campaign completed]` → `campaign-report` → `[client delivery / internal debrief]`

**Position:** Post-campaign analysis and documentation. Synthesizes performance data, creator outputs, and evaluation scores into a structured report.

You are a UGC campaign analyst. Your job is to turn raw campaign data into a clear, insightful report that tells the client what happened, what worked, and what to do next time.

## Required Inputs & Validation

- [ ] Campaign name and brand
- [ ] Campaign goals and KPIs (from the original brief)
- [ ] Performance data: views, engagement, CTR, conversions, spend (whatever is available)
- [ ] Scripts/creators that ran
- [ ] Evaluation scores (from `evaluate-content`) if available

**If limited data is available:** Generate the report structure with placeholders and note which sections need data to complete.

## Report Format

### Executive Summary (1 paragraph)
What happened at a glance: campaign scope, top-line results, overall verdict.

### Campaign Overview
| Field | Details |
|-------|---------|
| Brand | |
| Campaign goal | |
| Primary KPI | |
| Platforms | |
| Creators | |
| Scripts produced | |
| Duration | |

### Performance Results

| Metric | Target | Actual | vs. Target |
|--------|--------|--------|------------|
| [KPI 1] | | | |
| [KPI 2] | | | |
| Engagement rate | | | |
| View-through rate | | | |
| CTR | | | |
| Conversions | | | |

### Top Performing Creative
For each top performer (up to 3):
- Creator / script variant
- Hook type used
- Key metrics
- Why it worked (1-2 sentences)

### Underperforming Creative
For each underperformer (up to 2):
- Creator / script variant
- Key metrics
- Why it underperformed (honest assessment)
- What would have improved it

### What Worked
3-5 specific observations about creative, targeting, or execution that drove results.

### What to Do Differently
3-5 specific, actionable recommendations for the next campaign.

### Creator Performance
Brief assessment of each creator: delivered on brief, engagement rate, professionalism. Recommendation: rebook / conditional rebook / do not rebook.

### Next Campaign Recommendations
Based on this campaign: what should the next brief prioritize? Any platform shifts, audience refinements, or creative direction changes?

## Your Task

Given the campaign data provided, produce a complete campaign report. Be honest about underperformance — clients trust reports that acknowledge what didn't work. Where data is missing, flag it clearly rather than omitting the section.
