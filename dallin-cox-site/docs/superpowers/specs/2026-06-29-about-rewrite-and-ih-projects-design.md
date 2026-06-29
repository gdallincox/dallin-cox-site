# About Section Rewrite + Intermountain Internship Projects — Design

**Date:** 2026-06-29
**Site:** thedallincox.com (repo: `gdallincox/dallin-cox-site`)
**File touched:** `index.html` (single-file static site)

## Goal

Update the About section to reflect the role transition (no longer Director of Strategic Operations at RVSU; now Associate Continuous Improvement Consultant at Intermountain Health + ongoing RVSU advisory contract). Add two new project entries documenting the Intermountain Health internship work (Jan 2026 – Apr 2026). Recruiter is the primary audience.

## Scope

**In scope:**

- Replace the three About paragraphs (`#about` section, current paragraphs at lines ~2124–2126) with a new two-paragraph version: ¶1 career arc, ¶2 current state.
- Update one bullet in the existing Experience entry for `Continuous Improvement Intern` (line ~2495) to remove the word "neurology" for consistency with the new redaction posture.
- Append two new `featured-card` entries to the end of the Projects section, after the existing Prior Authorization Tracking card (currently ends ~line 2444).
- Add minimal CSS so the new cards render correctly as text-only (no `.featured-visual` block).

**Out of scope (do not touch):**

- Hero section, including pills and headline
- Stats section (already updated in a prior session)
- Credentials grid inside About (McKinsey Forward, LSS Green Belt, ACHE, Spanish)
- Existing Projects entries (Scheduler, Insights, Patient Growth, Supply Chain, Utah Retina Website, PA Tracking)
- Other Experience entries
- Contact section, footer, metadata, site styling beyond the one CSS addition called out below
- All image assets and any new visual creation (cards ship text-only)

## Primary reader

Recruiters and hiring managers screening for analyst / consulting / healthcare-operations roles. Tone: confident, scannable, grounded in concrete outcomes. No academic framing.

## Design decisions

| Decision | Choice | Rationale |
|---|---|---|
| About opening structure | Career-arc | More memorable than a title-led opener; the story is the differentiator |
| About length | Two paragraphs | Forward-looking ¶3 from the original would read as aspirational; folding AI/analytics into ¶1 keeps the differentiator without a separate beat |
| AI / Anthropic coursework framing | Folded lightly into arc | Real differentiator vs. other healthcare ops candidates; do not lose it, do not feature it |
| Primary audience | Recruiters | Optimize tone and keyword scan for hiring pipeline |
| Status pill on new project cards | `Internship Project` | Cleaner than "case study"; matches the short noun-phrase voice of existing pills |
| Project card placement | Append at end of Projects section, after PA Tracking | Internship work is most recent and methodology-forward; chronological tail |
| Confidentiality posture | Strict LinkedIn-bullet boundary | Public LinkedIn bullets are the floor; nothing beyond them; no IH branding, no internal screens, no specific service-line names |
| Visuals on new cards | Text-only with small CSS tweak | Avoids creating concept SVGs and avoids any IH-adjacent visual risk |
| Cross-section consistency on "neurology" | Update Experience bullet too | Page can't contradict itself; LinkedIn already says "neurology" publicly but the redaction posture going forward is "specialty service line" |

## Architecture

Single file: `/index.html`. Three discrete edits, all inside this file:

1. About `<p>` blocks inside `.about-text` (lines ~2124–2126)
2. One `<li>` inside the `Continuous Improvement Intern` Experience entry (line ~2495)
3. Two new `<article class="featured-card …">` blocks appended inside `.featured-projects` after the PA Tracking entry (after line ~2444)
4. One CSS rule added to the existing `<style>` block to handle a text-only `featured-card` (no `.featured-visual`)

The CSS addition is the only structural site change. Everything else is content.

## Content

### About section — new copy

**¶1 — Arc:**

> I'm Dallin Cox. I began college with the intent to attend medical school, until a singular healthcare leadership class at BYU pulled me toward the business side of medicine instead. Trying to learn all I could, I started taking on operational problems at Retina and Vitreous Surgeons of Utah. I ultimately grew into the Strategic Operations Director role, and from there earned a Continuous Improvement internship at Intermountain Health. This eventually led to a full-time offer to return as a Continuous Improvement Consultant. Along the way, analytics, process design, and AI-augmented systems became the operational tools that built how I work, not as buzzwords, but as the tools behind operational decisions that hold up.

**¶2 — Current state:**

> Today, I'm at Intermountain Health as a Continuous Improvement Consultant, supporting process redesign, operational efficiency, and quality initiatives across the system. I also continue to advise Retina and Vitreous Surgeons of Utah on contract — an 8-location retinal specialty practice with 30,000+ annual patient visits. I work on process improvement, operational workflows, and the analytics behind both.

Use em dashes (`&mdash;`) and curly apostrophes consistent with the rest of the file.

**Title-naming rule (site-wide):** Only the Experience section uses the full LinkedIn title `Associate Continuous Improvement Consultant`. Every other reference on the page (About, future copy, any new mentions) uses the shortened `Continuous Improvement Consultant`.

### Experience bullet — single-word change

In the `Continuous Improvement Intern` entry (`Jan 2026 — Apr 2026`), change the first bullet from:

> Redesigned referral intake workflows for a **neurology service line** supporting 9 providers…

to:

> Redesigned referral intake workflows for a **specialty service line** supporting 9 providers…

Rest of the bullet, and the second bullet (Patient Safety Monitor), unchanged.

### Project card 1 — Referral Intake Redesign

- **Status pill:** `Internship Project`
- **Tag:** `Process Redesign — Specialty Service Line`
- **Title:** `Referral Intake Redesign — Cutting the backlog, restoring access.`
- **URL line:** `9 providers · 100+ referrals · Workflow redesign`
- **Description:**
  > A referral intake workflow redesign for a specialty service line supporting 9 providers. The existing intake process had accumulated a backlog of 100+ unaddressed referrals — patients waiting on care while the routing gap grew. The redesign reworked the intake workflow end-to-end, eliminating the backlog and improving access and throughput across the service line.
- **Feats list:**
  - Specialty service line supporting 9 providers
  - 100+ unaddressed referrals in backlog at start
  - Referral intake workflow redesigned end-to-end
  - Backlog eliminated
  - Patient access and throughput improved
- **Tools:** `Process Mapping`, `Workflow Redesign`, `Healthcare Operations`, `Continuous Improvement`
- **Visual:** none — text-only treatment

### Project card 2 — Patient Safety Monitor Utilization

- **Status pill:** `Internship Project`
- **Tag:** `Patient Safety — System-wide Standardization`
- **Title:** `Patient Safety Monitor — Closing utilization gaps to reduce fall risk.`
- **URL line:** `3+ hospitals · Utilization evaluation · Standardization`
- **Description:**
  > A multi-site evaluation of Patient Safety Monitor utilization across 3+ hospitals, partnered with patient safety leadership. The work identified workflow gaps in how the monitor was being used and drove system-wide standardization recommendations to reduce inpatient fall risk.
- **Feats list:**
  - Multi-site scope across 3+ hospitals
  - Partnered with patient safety leadership
  - Patient Safety Monitor utilization evaluated
  - Workflow gaps identified
  - System-wide standardization to reduce inpatient fall risk
- **Tools:** `Process Audit`, `Workflow Analysis`, `System Standardization`, `Patient Safety`
- **Visual:** none — text-only treatment

## CSS treatment for text-only cards

Existing `featured-card` layout assumes both `.featured-content` and `.featured-visual` children (the visual area provides width balance on desktop). For the two new IH cards, omit `.featured-visual` and add one CSS rule that targets the new cards specifically so they render correctly:

- New class on the card root: `featured-card--text-only`
- New rule: when a `.featured-card` has the `--text-only` modifier, `.featured-content` expands to full width and visual-related grid/padding rules are neutralized for that card only.
- Do not modify any existing `.featured-card` rule. The modifier class is additive only.
- The card retains the existing `.reveal` animation class and alternates correctly with `.reverse` if needed.

Verify visually at desktop, tablet, and mobile breakpoints before committing.

## Verification checklist

- [ ] About paragraph 1 reads correctly, em dashes render, no orphan apostrophes
- [ ] About paragraph 2 reads correctly, "30,000+ annual patient visits" matches the existing site's number formatting style
- [ ] About paragraph 2 says `Continuous Improvement Consultant` (short form), not `Associate Continuous Improvement Consultant`
- [ ] Experience entry still says full title `Associate Continuous Improvement Consultant` (untouched)
- [ ] Credentials grid (McKinsey Forward, LSS Green Belt, ACHE, Spanish) unchanged
- [ ] Experience bullet says "specialty service line", not "neurology service line"
- [ ] Two new project cards render at the bottom of `.featured-projects`, after PA Tracking
- [ ] Text-only cards do not have a visual area; description and feats span full content width
- [ ] No IH brand assets, hospital names, internal screens, or specific service-line names appear anywhere on the page
- [ ] No regressions elsewhere on the page (hero, stats, projects above PA Tracking, experience entries other than the IH internship bullet, contact, footer)
- [ ] Local preview confirms layout at desktop, tablet, and mobile

## Open items / non-decisions

- None pending. Spec is implementation-ready.

## Out of scope, deferred

- Concept SVGs for the IH cards (decided against; can be added later if recruiter feedback suggests cards feel light)
- Updating the "Continuous Improvement Intern" Experience bullet beyond the one-word redaction (`neurology` → `specialty service line`); the rest of the bullet stays
- Any IH brand-permission outreach; assumes "LinkedIn-public bullets are the floor" remains the operating posture
