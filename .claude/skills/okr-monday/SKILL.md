---
name: okr-monday
description: >
  Weekly Monday Commitment check-in for OKRs. Use when user mentions "Monday", "Weekly Check-in",
  "OKR Update", "Monday Commitments", or at the start of each week to update OKRs.
---

# Monday Commitment - Weekly OKR Check-in

Facilitate a **15-minute** Monday morning check-in to set commitments for the week (Wodtke's Weekly OKR Cadence).

## Instructions

### 1. Identify Current Week
- What's today's date? Please check the current day with an actual check in the system. This is critical
- Which week are we in? (Calculate from Q4 start date)

### 2. Read Current OKRs
**Load:** `/outputs/okrs/Q4-2025-OKRs.md`

**Find:**
- All Key Results
- Current progress
- Last week's commitments

### 3. Ask For Each KR
For **EACH** Key Result:
- "What's your confidence NOW (0-10) for hitting [KR target] by [end date]?"
- "What are 1-2 CONCRETE actions you'll do THIS WEEK?"

**Push for specificity:**
- ❌ "Work on client stuff" → Too vague!
- ✅ "Send proposal to Client A's CTO" → Specific!

### 4. Update OKR File
Update `/outputs/okrs/Q4-2025-OKRs.md` for current week:

```markdown
### Week X (Date Range)

**Monday Commitments:**
- [ ] KR1: [action 1], [action 2]
- [ ] KR2: [action 1], [action 2]
- [ ] KRN: [action 1], [action 2]

**Confidence Update:**
- KR1: X/10
- KR2: X/10
- KRN: X/10
```

### 5. Update CURRENT_WEEK.md
**IMPORTANT:** Always update `/outputs/okrs/CURRENT_WEEK.md` with:

- Week number & period
- This week's commitments (checkboxes)
- Updated progress for each KR
- Updated confidence levels
- Focus statement

**This is the Single Source of Truth for the current week!**

### 6. Summarize & Close
**Provide:**
- This week's focus (4-8 key actions)
- Any confidence drops or blockers flagged
- "See you Friday for Wins & Learning!"

**Keep it SHORT - 15 min max!**

---

## Example

**User:** "Monday Commitments!"

**You:**
```
Morning! ☕ Let's do Monday Commitments - 15 min max!

We're in Week 3 (Nov 4-8) of Q4 2025.

Your Key Results:
1. €8K MRR from retainers (Current: €2K)
2. 10 discovery calls from LinkedIn (Current: 2)
3. NPS 9+ + case study (Current: in progress)
4. €6K workshop revenue (Current: €0)

**KR1 (€8K MRR):**
Last week confidence: 5/10
- What's your confidence NOW (0-10)?
- What are 1-2 actions THIS WEEK?

[Wait for user response, then continue with KR2, KR3, KR4...]

[After collecting all:]

✅ Updated! Here's your week:

**This Week's Focus:**
- KR1: Follow-up to Client A, pricing call with Client B
- KR2: Write 3 LinkedIn posts, engage 10 competitor posts
- KR3: Send NPS survey, start case study outline
- KR4: Finalize workshop deck, outreach 5 warm leads

Confidence: KR1 (6/10 ↑), KR2 (4/10 =), KR3 (7/10 ↑), KR4 (5/10 =)

Keep it focused - these are your ONLY commitments this week!

See you Friday! 🎉
```

---

## File Reference

**Update (2 files!):**
1. `/outputs/okrs/Q4-2025-OKRs.md` (main OKR file - archive of all weeks)
2. `/outputs/okrs/CURRENT_WEEK.md` (current week only - Single Source of Truth!)

**CRITICAL:** Both files must be updated every Monday!

**Never:**
- ❌ Change OKRs themselves (no editing mid-quarter!)
- ❌ Change target numbers
- ❌ Skip weeks
- ❌ Forget to update CURRENT_WEEK.md!

---

*Monday Commitment Skill - Wodtke's Weekly Cadence*
