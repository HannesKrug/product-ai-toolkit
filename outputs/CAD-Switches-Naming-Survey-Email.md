# CAD Switches - Naming Survey Email
**Ready to send | Copy-paste template below**

---

## Email Template

### Subject Line:
```
Quick input needed: Naming our new API (3 min)
```

---

### Email Body:

```
Hi [Name],

Quick favor – I need 3 minutes of your input on naming a new API we're building for instant3Dhub 3.13.0.

**What we're building:**

We're creating a unified API that maps CAD-native concepts from tools like NX and CATIA into instant3Dhub.

**CAD Concepts we're mapping:**

*Filtering/Visibility:*
- Reference Sets (NX) – control which geometry of a part is visible
- Layers (NX, CATIA) – organize and toggle visibility of model elements
- Variants (NX, CATIA) – product configuration states

*Overwrites (future):*
- Arrangements (NX) – position alternatives for assemblies
- Interpart Expressions – parametric overrides
- Color/appearance modifications

**The Problem:**
Today, these concepts are handled by separate APIs (LayerFilterAPI, VariantsAPI).
Each new CAD concept requires changes across many components. Not scalable.

**The Solution:**
One unified API that handles all these CAD concepts through a single, extensible interface.
Add new CAD concepts (e.g., Arrangements) without rewriting the system.

**I need your help choosing the right name for this API.**

---

**Question 1: Which name best describes this API?**

A) CAD Switches
B) CAD States
C) CAD Filters
D) CAD Profiles
E) Other (please suggest): __________

Your choice: [  ]

---

**Question 2: Why did you choose that name?** (1-2 sentences)

Your answer:



---

**Question 3: Based on the name you chose, what would you EXPECT this API to do?**
(Imagine seeing it in docs without context)

Your answer:



---

**Question 4 (Optional): Any concerns or alternative suggestions?**

Your answer:



---

That's it! Just hit reply with your answers.

Thanks for helping us get this right! 🙏

Best,
Hannes

P.S. We're targeting Q1 2026 (3.13.0) for release. I'll share the decision and rationale once we finalize.
```

---

## Suggested Recipients

**Target: 5-8 people**

- [ ] Internal web developer 1: _________________
- [ ] Internal web developer 2: _________________
- [ ] Grob developer contact: _________________
- [ ] Daimler Truck developer contact: _________________
- [ ] Partner/beta customer 1: _________________
- [ ] Partner/beta customer 2: _________________
- [ ] Other active webvis.js user: _________________

---

## Timeline

- **Send:** Today/Tomorrow
- **Follow-up:** Gentle reminder after 2 days (if no response)
- **Deadline:** Collect responses by end of week
- **Decision:** Finalize naming next Monday

---

## How to Use This Document

1. ✅ Copy the email body above
2. ✅ Paste into your email client
3. ✅ Replace `[Name]` with recipient's name
4. ✅ Send to 5-8 web developers
5. ✅ Track responses (tally in table below)

---

## Response Tracker

| Name | Choice (A/B/C/D/E) | Rationale | Expectations | Concerns | Notes |
|------|-------------------|-----------|--------------|----------|-------|
|      |                   |           |              |          |       |
|      |                   |           |              |          |       |
|      |                   |           |              |          |       |
|      |                   |           |              |          |       |
|      |                   |           |              |          |       |
|      |                   |           |              |          |       |
|      |                   |           |              |          |       |
|      |                   |           |              |          |       |

---

## Decision Framework

**After collecting responses:**

1. **Tally votes:** Count A/B/C/D/E choices
2. **Read rationale:** Do people understand what it does?
3. **Check expectations:** Does the name set correct expectations?
4. **Look for red flags:** Confusion with "Configuration Management"?

**Decision rule:**
- ✅ 60%+ prefer one name → Adopt it
- ⚠️ Split vote (50/50) → Quick call with 2-3 respondents
- ❌ Concerns about confusion → Avoid that name

---

## Next Steps After Decision

1. ✅ Update PRD (`/outputs/prd/CAD-Switches-PRD.md`) with final name
2. ✅ Announce decision to stakeholders (Maik, Tim, Engineering)
3. ✅ Update API naming in technical spec
4. ✅ Proceed with stakeholder review (Task #2 from next steps list)

---

**Created:** 2025-11-28
**Owner:** Hannes Krug (Senior PM)
**Related:** CAD Switches PRD v1.1
