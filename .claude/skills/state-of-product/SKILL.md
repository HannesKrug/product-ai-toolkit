---
name: state-of-product
description: Creates State Of The Product Reports - internal documents summarizing stakeholder feedback and defining product direction. Use when user mentions "State Of The Product", "Product Report", "Product Summary", "Product Direction Report", or wants to summarize product status and feedback for company stakeholders.
---

# State Of The Product Report

*Create comprehensive internal product reports that summarize stakeholder feedback and set strategic direction.*

---

## Instructions

### 1. Gather Context & Define Scope

Ask the user:
- **Timeframe:** What period does this report cover? (e.g., Q4 2025, last 6 weeks, 2025 overview)
- **Target Audience:** Who will read this? (Leadership, entire company, product team)
- **Key Focus Areas:** Any specific topics to emphasize? (product launches, customer feedback, strategic shifts)
- **Feedback Sources:** Where should feedback come from?
  - User interviews / customer feedback
  - Internal stakeholder feedback (sales, support, engineering)
  - Metrics / analytics data
  - Market research / competitive analysis

### 2. Collect Relevant Information

**Leverage existing files:**
- Check `/user_context/COMPANY_CONTEXT.md` for product strategy, North Star, current priorities
- Check `/outputs/okrs/CURRENT_WEEK.md` or quarterly OKR files for progress updates
- Check `/user_context/raw/` for interview notes, feedback documents, analytics reports

**Ask user to provide:**
- Key feedback themes (what are customers/stakeholders saying?)
- Major wins or achievements this period
- Challenges or blockers encountered
- Metrics updates (usage, revenue, engagement, etc.)
- Upcoming priorities or strategic shifts

### 3. Fill the Template

Use `@reference/template.md` as the structure. See `@reference/guide.md` for detailed section guidance.

**Core sections to complete:**

1. **Executive Summary**
   - One paragraph overview (product health + momentum)
   - Key wins this period (3 bullets)
   - Key challenges (3 bullets)
   - One-sentence outlook for next period

2. **Product Vision & Strategic Lens**
   - Vision (aspirational future state)
   - Strategic pillars (3-5 core themes guiding decisions)
   - Target users / target workflows
   - What "success" looks like long-term

3. **High-Level Metrics Snapshot**
   - Adoption metrics
   - Usage / engagement metrics
   - Reliability & performance (SLIs/SLOs)
   - Support volume & top categories
   - Satisfaction (NPS, CSAT, CES)
   - **Interpretation** (tell the story behind the numbers!)

4. **Customer Insights & Feedback Themes**
   - 3-5 themes structured as:
     - What users say
     - Evidence (quotes, support patterns, examples)
     - Why it matters
   - Optional: "What users love" section

5. **Top Product Gaps**
   - 3-7 gaps that limit adoption, retention, or expansion
   - For each gap:
     - Definition
     - Evidence
     - Impact (who affected + business impact)
     - Priority (High/Medium/Low)
     - Notes / dependencies

6. **Market & Competitive Signals**
   - Industry trends
   - Observed competitor improvements
   - Shifts in user expectations
   - Strategic partnership developments
   - **Implications for our strategy**

7. **Prioritized Opportunities**
   - Group by timeframe (Now / Next / Later)
   - For each opportunity:
     - What it unlocks
     - Expected impact (metric, business, strategic)
     - Confidence level (High/Medium/Low + reasoning)

### 4. Apply Company Context

**Adapt tone and depth based on company stage:**
- **Startup (5-50):** Concise, fast-moving, focus on iteration speed and customer insights
- **Scale-up (50-200):** Balance detail with clarity, emphasize alignment and priorities
- **Corporate (200+):** Structured, data-driven, clear accountability and metrics

**Check `COMPANY_CONTEXT.md` for:**
- Customer type (B2B/B2C/B2B2C) → adjust feedback framing
- Current quarter priorities → ensure alignment
- Team structure → tailor action items to teams

### 5. Review & Refine

**Quality checks:**
- ✅ Executive Summary stands alone (busy leaders can read just this)
- ✅ Product Vision provides strategic framing (everything ladders to this)
- ✅ Metrics tell a story (interpretation, not just numbers)
- ✅ Feedback themes are specific and evidence-based (quotes + data)
- ✅ Product Gaps are prioritized with clear business impact
- ✅ Market signals are relevant with implications spelled out
- ✅ Opportunities connect to gaps/themes (show the thread)
- ✅ Confidence levels are honest (acknowledge uncertainty)
- ✅ Connections between sections are explicit (feedback → gaps → opportunities)
- ✅ Tone balances wins and challenges (build trust through honesty)

**Ask user:**
- "Does this capture the strategic picture accurately?"
- "Are the prioritized opportunities clear and well-justified?"
- "Any feedback sources, gaps, or market signals we missed?"

### 6. Save & Share

**Save to:** `/outputs/product-reports/[Period]-State-of-Product.md`
- Example: `/outputs/product-reports/Q4-2025-State-of-Product.md`
- Example: `/outputs/product-reports/2025-State-of-Product.md`

**Add front matter:**
```yaml
---
title: State Of The Product - [Period]
date: [YYYY-MM-DD]
period: [Q4 2025 / 2025 / etc.]
audience: [Leadership / All-Hands / Product Team]
author: [Your Name]
status: final
---
```

---

## Examples

### Example 1: Quarterly Report

**User Request:**
"Create a State Of The Product report for Q4 2025"

**Workflow:**
1. Gather Q4 context:
   - Check `/outputs/okrs/Q4-2025-OKRs.md` for OKR progress
   - Ask about key customer feedback themes from Q4
   - Request metrics updates (adoption, engagement, satisfaction, support volume)
   - Ask about competitive moves or market signals

2. Fill template with new structure:
   - **Executive Summary:** "instant3Dhub showed strong platform stability but slower ecosystem adoption..." + 3 wins, 3 challenges, outlook
   - **Product Vision & Strategic Lens:** Restate vision, pillars (Dev Experience, Enterprise Reliability, Ecosystem Growth), target users
   - **Metrics Snapshot:** Tables for adoption, engagement, SLIs/SLOs, support, NPS + interpretation
   - **Feedback Themes:** Theme 1: "Setup friction prevents first success" (with quotes + evidence), Theme 2-3...
   - **Product Gaps:** Gap 1: "Onboarding friction" (definition, evidence, impact, priority), Gap 2-5...
   - **Market Signals:** USD standardization, WebGPU adoption, competitor AI features + implications
   - **Opportunities:** Now: "Developer Onboarding Overhaul" (unlocks gaps 1-2, expected impact, high confidence), Next: ..., Later: ...

3. Save to: `/outputs/product-reports/Q4-2025-State-of-Product.md`

### Example 2: Year-End Report

**User Request:**
"I need a State Of The Product report for the entire 2025"

**Workflow:**
1. Gather annual context:
   - Review all quarterly OKRs from 2025
   - Summarize major launches (BRIX, Catena-X, USD support)
   - Annual metrics trends (adoption growth, engagement patterns, satisfaction shifts)
   - Key feedback themes across the year
   - Strategic pivots during the year

2. Fill template:
   - **Executive Summary:** "2025 marked our transition from platform to ecosystem..." + annual wins/challenges
   - **Product Vision:** May reference evolution of vision during the year
   - **Metrics:** Annual trends with quarterly breakdowns
   - **Feedback Themes:** Persistent themes across 2025
   - **Product Gaps:** Current state of gaps (which remain, which resolved)
   - **Market Signals:** Major industry shifts in 2025
   - **Opportunities:** 2026 strategic priorities (Now/Next/Later)

3. Save to: `/outputs/product-reports/2025-State-of-Product.md`

---

## Tips for Great Reports

**✅ DO:**
- **Write Executive Summary LAST** - distill after completing all sections
- **Frame with Vision** - Product Vision section sets the strategic lens for everything
- **Tell stories with metrics** - not just "MAU up 20%" but interpret what it means
- **Use compelling quotes** - bring real user voices into feedback themes
- **Prioritize gaps ruthlessly** - 3-7 major gaps, not 20
- **Connect the dots explicitly** - show how themes → gaps → opportunities
- **Be honest about confidence** - Low confidence is okay if you explain why
- **Show market context** - external signals that influence your strategy
- **Make opportunities specific** - clear impact and concrete next steps

**❌ DON'T:**
- Create a laundry list of every feature shipped (focus on strategic impact)
- Report metrics without interpretation (always tell the story)
- List vague priorities ("improve user experience" is not an opportunity)
- Sugarcoat challenges (honesty builds trust)
- Skip the "why" behind opportunities (always connect to evidence)
- Forget market signals (products don't exist in a vacuum)
- Claim certainty when there's risk (be honest about confidence levels)

---

## Reference Files

- **Report Template:** `@reference/template.md`
- **Section Guide:** `@reference/guide.md`

---

## Company Context Integration

**This Skill leverages:**
- `/user_context/COMPANY_CONTEXT.md` - Product strategy, North Star, customer type
- `/outputs/okrs/` - OKR progress and strategic alignment
- `/user_context/raw/` - Feedback sources, interviews, analytics

**Aligns with:**
- Product-Toolkit principles (outcomes over outputs)
- Company-specific context (B2B, scale-up, developer focus)
- Current priorities (BRIX launch, Catena-X, feedback management)

---

*State Of The Product Skill - Product-Toolkit*
