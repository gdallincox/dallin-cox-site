# About Rewrite + Intermountain Internship Projects — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Update the About section to reflect the IH/RVSU role transition, redact "neurology" from the Experience bullet for consistency, and append two text-only Intermountain Internship project cards to the Projects section.

**Architecture:** All edits land in a single static HTML file (`index.html`). One additive CSS rule introduces a `featured-card--text-only` modifier so the two new cards render without a `.featured-visual` block. Content stays strictly inside the LinkedIn-bullet boundary on Intermountain Health work.

**Tech Stack:** Static HTML + inline `<style>` block. No build pipeline. Vercel deploys whatever is committed. Local preview via `open index.html`.

## Global Constraints

- File touched: `/Users/dallin/dallin-cox-site/dallin-cox-site/index.html` only. Do not edit other files, asset paths, or images.
- Title-naming rule: only the Experience section uses the full LinkedIn title `Associate Continuous Improvement Consultant`. Every other reference on the page uses the shortened `Continuous Improvement Consultant`.
- Confidentiality posture: strict LinkedIn-public boundary on Intermountain Health content. No hospital names, no IH branding, no internal screens, and no specific service-line names — use `specialty service line` only.
- Hero, stats, credentials grid, all existing Projects entries above PA Tracking, all other Experience entries, contact section, footer, metadata, and pre-existing CSS rules: untouched.
- Preview locally at desktop (>= 1024px), tablet (768px), and mobile (390px) widths before committing each task.
- Do not run `git push` at any point in this plan. Only commit locally.
- Use `&mdash;` for em dashes and straight apostrophes consistent with surrounding text in `index.html`.

## File Map

| File | Action | Lines affected (current) | Responsibility |
|---|---|---|---|
| `index.html` | Modify (CSS) | Insert just before line 2049 (`</style>`) | New `featured-card--text-only` modifier rule |
| `index.html` | Modify (About) | Replace lines 2124–2126 (three `<p>` blocks) | Two-paragraph rewrite of About copy |
| `index.html` | Modify (Experience) | Line 2495 (single `<li>`) | One-word redaction: `neurology` → `specialty` |
| `index.html` | Modify (Projects) | Insert after line 2444 (end of PA Tracking `<article>`, before line 2445 blank line / closing `</div>`) | Append two new `featured-card` entries |

Line numbers are based on the state of the file at the time this plan was written. If earlier tasks change line counts, search for the anchor strings shown in each task rather than trusting absolute line numbers.

---

### Task 1: Add `featured-card--text-only` CSS modifier

**Files:**
- Modify: `/Users/dallin/dallin-cox-site/dallin-cox-site/index.html` (CSS block, just before `</style>` on line 2049)

**Interfaces:**
- Consumes: existing `.featured-card` rule (line 980) with `display: grid; grid-template-columns: 1fr 1.1fr;` and `.featured-card.reverse` rule (line 1009) with `grid-template-columns: 1.1fr 1fr;`
- Produces: a single additive class `.featured-card--text-only` that downstream tasks (Task 4, Task 5) apply to the two new article elements

- [ ] **Step 1: Locate the insertion point**

Open `index.html` and find the last existing rule before `</style>`:

```
2041:  @media (max-width: 480px) {
2042:    .featured-tools, .hero-pills { gap: 0.35rem; }
...
2048:  }
2049: </style>
```

The new rule goes between line 2048 (closing `}` of the 480px media query) and line 2049 (`</style>`).

- [ ] **Step 2: Insert the CSS rule**

Insert the following block immediately before `</style>`:

```css
  /* Text-only featured card variant (no .featured-visual block) */
  .featured-card--text-only {
    grid-template-columns: 1fr;
  }
  .featured-card--text-only .featured-content {
    max-width: 720px;
  }
```

Rationale:
- `grid-template-columns: 1fr` collapses the two-column grid to one column so the missing visual area does not leave empty space.
- `max-width: 720px` on `.featured-content` keeps description and feature-list line lengths readable on wide screens. No `margin: 0 auto` — content stays left-aligned, matching the existing left-aligned cards.
- No mobile override needed; the existing `@media (max-width: 900px)` rule (line ~1982) already forces all `featured-card` to a single column on small screens.

- [ ] **Step 3: Save and preview**

```bash
open /Users/dallin/dallin-cox-site/dallin-cox-site/index.html
```

Expected: All six existing project cards (Scheduler, Insights, Patient Growth, Supply Chain, Utah Retina Website, PA Tracking) render identically to before. The CSS rule has no effect yet because no element uses `featured-card--text-only` yet.

- [ ] **Step 4: Visual regression check**

Resize the browser window to 1024px, 768px, and 390px widths. Confirm all six existing project cards still alternate left/right (where applicable), the visuals still appear, and nothing has shifted.

- [ ] **Step 5: Commit**

```bash
cd /Users/dallin/dallin-cox-site/dallin-cox-site
git add index.html
git commit -m "css: add featured-card--text-only modifier for cards without visuals"
```

---

### Task 2: Rewrite About section paragraphs

**Files:**
- Modify: `/Users/dallin/dallin-cox-site/dallin-cox-site/index.html` (replace three `<p>` blocks inside `.about-text`)

**Interfaces:**
- Consumes: existing `#about` section structure (`section#about > div.about-grid > div.about-text > p × 3`)
- Produces: same wrapper structure, but with two `<p>` blocks instead of three. Downstream tasks do not depend on this output.

- [ ] **Step 1: Locate the existing About paragraphs**

Search for the anchor: `I'm Dallin Cox, Director of Strategic Operations`

Confirm the three current `<p>` blocks live inside the `<div class="about-text">` block, starting around line 2124 and ending at line 2126 (one block per line).

- [ ] **Step 2: Replace the three `<p>` blocks with two new ones**

Replace this entire block:

```html
      <p>I'm Dallin Cox, Director of Strategic Operations at Retina and Vitreous Surgeons of Utah, where I oversee four clinics, four outreach sites, 25+ clinical and administrative staff, and 2,500+ monthly patient visits across Salt Lake County, Utah County, and surrounding rural areas.</p>
      <p>I started as a medical assistant at the practice, took on every operational problem that came up, until that became my entire job. The work has compounded into real numbers: $350K+ in total savings &mdash; including $50K+ from reimbursement renegotiation &mdash; and a 40% lift in web traffic after bringing digital marketing in-house.</p>
      <p>What I build from here sits at the intersection of operations and analytics &mdash; the systems, models, and tools behind decisions a practice can actually act on. AI is a meaningful part of how I work: a practical tool for analysis, design, and decisions, not a buzzword. I&rsquo;ve completed formal Anthropic coursework in prompt engineering, agent design, and MCP to sharpen how I apply it.</p>
```

With this exact replacement:

```html
      <p>I'm Dallin Cox. I began college with the intent to attend medical school, until a singular healthcare leadership class at BYU pulled me toward the business side of medicine instead. Trying to learn all I could, I started taking on operational problems at Retina and Vitreous Surgeons of Utah. I ultimately grew into the Strategic Operations Director role, and from there earned a Continuous Improvement internship at Intermountain Health. This eventually led to a full-time offer to return as a Continuous Improvement Consultant. Along the way, analytics, process design, and AI-augmented systems became the operational tools that built how I work, not as buzzwords, but as the tools behind operational decisions that hold up.</p>
      <p>Today, I'm at Intermountain Health as a Continuous Improvement Consultant, supporting process redesign, operational efficiency, and quality initiatives across the system. I also continue to advise Retina and Vitreous Surgeons of Utah on contract &mdash; an 8-location retinal specialty practice with 30,000+ annual patient visits. I work on process improvement, operational workflows, and the analytics behind both.</p>
```

Notes for the implementer:
- The new ¶2 says `Continuous Improvement Consultant` (no "Associate"). This is intentional per the Global Constraints title-naming rule.
- Use straight apostrophes (`'`) — match the existing file style (the original P2/P3 used `&rsquo;` only inside `I&rsquo;ve`, while P1 used `I'm`. Default to straight `'` everywhere here).
- Em dashes use `&mdash;` (no surrounding spaces inside the entity, but with a literal space on each side: `practice &mdash; an 8-location`).

- [ ] **Step 3: Preview and verify content**

```bash
open /Users/dallin/dallin-cox-site/dallin-cox-site/index.html
```

Scroll to the About section. Confirm:
- Exactly **two** paragraphs appear (not three, not one)
- ¶1 reads as the career arc starting with "I'm Dallin Cox. I began college..."
- ¶2 reads as the current state, says "a Continuous Improvement Consultant" (with the article "a", and without "Associate")
- Em dashes render correctly (long dash, not literal `&mdash;`)
- The credentials grid on the right (McKinsey Forward, LSS Green Belt, ACHE, Spanish) is unchanged

- [ ] **Step 4: Cross-section visual regression**

Hero, stats section, projects section, experience section, and contact: spot-check that none of them changed.

- [ ] **Step 5: Commit**

```bash
cd /Users/dallin/dallin-cox-site/dallin-cox-site
git add index.html
git commit -m "content: rewrite About section as arc + current state, drop Director framing"
```

---

### Task 3: Redact "neurology" from Experience bullet

**Files:**
- Modify: `/Users/dallin/dallin-cox-site/dallin-cox-site/index.html` (single `<li>` inside the `Continuous Improvement Intern` Experience entry, currently line ~2495)

**Interfaces:**
- Consumes: existing Experience entry HTML structure
- Produces: same bullet with one word changed. No downstream dependency.

- [ ] **Step 1: Locate the bullet**

Search for the anchor: `Redesigned referral intake workflows for a neurology service line`

Confirm it appears exactly once in the file, inside the `Continuous Improvement Intern` Experience entry (date `Jan 2026 — Apr 2026`).

- [ ] **Step 2: Make the one-word change**

Replace:

```html
          <li>Redesigned referral intake workflows for a neurology service line supporting 9 providers, eliminating a backlog of 100+ unaddressed referrals and improving patient access and throughput</li>
```

With:

```html
          <li>Redesigned referral intake workflows for a specialty service line supporting 9 providers, eliminating a backlog of 100+ unaddressed referrals and improving patient access and throughput</li>
```

Only the word `neurology` becomes `specialty`. Everything else (numbers, surrounding wording, the second bullet about Patient Safety Monitor) stays exactly as-is.

- [ ] **Step 3: Verify only one match and only one change**

Run a search for the word `neurology` (case-insensitive) across `index.html`. Expected: zero matches after the edit.

- [ ] **Step 4: Preview**

```bash
open /Users/dallin/dallin-cox-site/dallin-cox-site/index.html
```

Scroll to the `Continuous Improvement Intern` Experience entry. Confirm the first bullet now reads "for a specialty service line" and the second bullet (Patient Safety Monitor) is unchanged.

- [ ] **Step 5: Commit**

```bash
cd /Users/dallin/dallin-cox-site/dallin-cox-site
git add index.html
git commit -m "content: redact neurology from IH internship Experience bullet"
```

---

### Task 4: Append project card 1 — Referral Intake Redesign

**Files:**
- Modify: `/Users/dallin/dallin-cox-site/dallin-cox-site/index.html` (insert one new `<article>` inside `.featured-projects`, after the Prior Authorization Tracking `<article>`, currently ends around line 2444)

**Interfaces:**
- Consumes: the `featured-card--text-only` CSS modifier added in Task 1
- Produces: a new `featured-card` entry whose layout pattern Task 5 will mirror (alternating `reverse` modifier)

- [ ] **Step 1: Locate the insertion point**

Search for the anchor: `PA_FutureState_Portfolio.svg` (the last image inside the PA Tracking card). The PA Tracking `<article>` closes shortly after that, with a `</article>` tag. The new card goes immediately after that `</article>` and before the closing `</div>` of `.featured-projects`.

The current end of `.featured-projects` looks like this:

```html
        </div>
      </div>
    </article>

  </div>
</section>
```

(The blank line before `</div>` is where new cards go.)

- [ ] **Step 2: Insert the Referral Intake card**

Insert this block immediately after the closing `</article>` of the PA Tracking card and before the closing `</div>` of `.featured-projects`. Keep the blank line above and below for readability matching the existing pattern between cards.

```html
    <!-- Referral Intake Redesign — IH Internship -->
    <article class="featured-card featured-card--text-only reveal">
      <div class="featured-content">
        <div class="featured-status">Internship Project</div>
        <div class="project-tag">Process Redesign &mdash; Specialty Service Line</div>
        <h3 class="featured-title">Referral Intake Redesign &mdash; Cutting the backlog, restoring access.</h3>
        <div class="featured-url">9 providers &middot; 100+ referrals &middot; Workflow redesign</div>
        <p class="featured-desc">A referral intake workflow redesign for a specialty service line supporting 9 providers. The existing intake process had accumulated a backlog of 100+ unaddressed referrals &mdash; patients waiting on care while the routing gap grew. The redesign reworked the intake workflow end-to-end, eliminating the backlog and improving access and throughput across the service line.</p>
        <ul class="featured-feats">
          <li>Specialty service line supporting 9 providers</li>
          <li>100+ unaddressed referrals in backlog at start</li>
          <li>Referral intake workflow redesigned end-to-end</li>
          <li>Backlog eliminated</li>
          <li>Patient access and throughput improved</li>
        </ul>
        <div class="featured-tools">
          <span class="tool-tag">Process Mapping</span>
          <span class="tool-tag">Workflow Redesign</span>
          <span class="tool-tag">Healthcare Operations</span>
          <span class="tool-tag">Continuous Improvement</span>
        </div>
      </div>
    </article>
```

Critical structural choices:
- Class list: `featured-card featured-card--text-only reveal`. No `reverse` modifier (this card is on the same side as existing odd-indexed cards). No `.featured-visual` child (modifier handles layout).
- Uses `&middot;` between URL-line segments, consistent with how `featured-url` is composed elsewhere in the file (e.g., the PA Tracking card uses `&middot;`).
- Uses `&mdash;` for em dashes inside descriptive text.
- No `featured-cta` block — there is no live demo or external link to point to.
- Status pill: `Internship Project` (exact casing).

- [ ] **Step 3: Preview**

```bash
open /Users/dallin/dallin-cox-site/dallin-cox-site/index.html
```

Scroll to the bottom of the Projects section. Confirm:
- A new card appears below PA Tracking
- It renders as a single-column text-only card (no laptop/phone visual, no empty right-side gap)
- Status pill shows `INTERNSHIP PROJECT` (uppercase from CSS) with the animated mint dot
- All five feature bullets render with the accent-colored dash markers
- The four tool tags appear at the bottom

- [ ] **Step 4: Responsive check**

Resize to 768px and 390px. The card should remain single-column with all content readable and no horizontal scroll. The existing project cards above should still alternate correctly.

- [ ] **Step 5: Commit**

```bash
cd /Users/dallin/dallin-cox-site/dallin-cox-site
git add index.html
git commit -m "content: add Referral Intake Redesign project card (IH internship)"
```

---

### Task 5: Append project card 2 — Patient Safety Monitor

**Files:**
- Modify: `/Users/dallin/dallin-cox-site/dallin-cox-site/index.html` (insert one new `<article>` inside `.featured-projects`, after the Referral Intake card from Task 4)

**Interfaces:**
- Consumes: `featured-card--text-only` CSS modifier from Task 1; same card pattern as Task 4
- Produces: no downstream dependencies

- [ ] **Step 1: Locate the insertion point**

Search for the anchor: `<!-- Referral Intake Redesign — IH Internship -->` (added in Task 4). The new card goes immediately after the closing `</article>` of that card, and before the closing `</div>` of `.featured-projects`.

- [ ] **Step 2: Insert the Patient Safety Monitor card**

Insert this block immediately after the closing `</article>` of the Referral Intake card and before the closing `</div>` of `.featured-projects`:

```html
    <!-- Patient Safety Monitor Utilization — IH Internship -->
    <article class="featured-card featured-card--text-only reverse reveal">
      <div class="featured-content">
        <div class="featured-status">Internship Project</div>
        <div class="project-tag">Patient Safety &mdash; System-wide Standardization</div>
        <h3 class="featured-title">Patient Safety Monitor &mdash; Closing utilization gaps to reduce fall risk.</h3>
        <div class="featured-url">3+ hospitals &middot; Utilization evaluation &middot; Standardization</div>
        <p class="featured-desc">A multi-site evaluation of Patient Safety Monitor utilization across 3+ hospitals, partnered with patient safety leadership. The work identified workflow gaps in how the monitor was being used and drove system-wide standardization recommendations to reduce inpatient fall risk.</p>
        <ul class="featured-feats">
          <li>Multi-site scope across 3+ hospitals</li>
          <li>Partnered with patient safety leadership</li>
          <li>Patient Safety Monitor utilization evaluated</li>
          <li>Workflow gaps identified</li>
          <li>System-wide standardization to reduce inpatient fall risk</li>
        </ul>
        <div class="featured-tools">
          <span class="tool-tag">Process Audit</span>
          <span class="tool-tag">Workflow Analysis</span>
          <span class="tool-tag">System Standardization</span>
          <span class="tool-tag">Patient Safety</span>
        </div>
      </div>
    </article>
```

Structural choices:
- Class list: `featured-card featured-card--text-only reverse reveal`. The `reverse` modifier maintains the alternating-side pattern used by all the existing project cards. Because `featured-card--text-only` overrides `grid-template-columns` to `1fr`, the `reverse` class does not produce any visible side flip on this card — but keeping the class preserves the alternation pattern and lets the modifier be removed later (if a visual is ever added) without rewriting the class list.
- No `.featured-visual` child.
- No `featured-cta` block.
- Status pill: `Internship Project` (exact casing).
- No IH hospital names, no internal screens, no specific service-line names — stays inside the LinkedIn-bullet boundary.

- [ ] **Step 3: Preview**

```bash
open /Users/dallin/dallin-cox-site/dallin-cox-site/index.html
```

Scroll to the bottom of the Projects section. Confirm:
- Two new text-only cards now sit below PA Tracking, in this order: Referral Intake Redesign → Patient Safety Monitor
- Both render single-column text-only with no visual area
- Status pills, project tags, descriptions, feature bullets, and tool tags all display correctly
- No references to "neurology" remain anywhere on the page
- No hospital names, IH branding, or internal screens

- [ ] **Step 4: Full-page regression sweep**

Reload the page from top. Confirm hero, stats, About (two paragraphs, correct copy), Projects (eight cards total now: six existing + two new), Experience (with `specialty service line` in the IH internship bullet), and Contact all render correctly.

Resize to 1024px, 768px, and 390px. Confirm no layout breaks at any breakpoint.

- [ ] **Step 5: Commit**

```bash
cd /Users/dallin/dallin-cox-site/dallin-cox-site
git add index.html
git commit -m "content: add Patient Safety Monitor project card (IH internship)"
```

---

## Self-Review

**Spec coverage**

| Spec requirement | Task |
|---|---|
| Replace About section with two paragraphs (arc + current) | Task 2 |
| Title-naming rule applied to About ¶2 ("Continuous Improvement Consultant", not "Associate ...") | Task 2 |
| Em dashes via `&mdash;` consistent with site | Tasks 2, 4, 5 |
| Experience bullet redacts "neurology" → "specialty service line" | Task 3 |
| Append two project cards at end of Projects section (after PA Tracking) | Tasks 4, 5 |
| Status pill `Internship Project` on both | Tasks 4, 5 |
| Text-only treatment — no `.featured-visual` block | Tasks 4, 5 |
| CSS modifier `featured-card--text-only` so layout doesn't break | Task 1 |
| Strict LinkedIn-bullet boundary — no hospital names, no service-line names, no IH branding | Tasks 4, 5 (and Task 3 ensures Experience matches) |
| Hero, stats, credentials grid, other Projects entries, other Experience entries, Contact, footer, metadata: unchanged | Enforced by each task's insertion-point precision and regression checks |
| Local preview at desktop/tablet/mobile before commit | Every task |
| Do not push | Global constraints |

No gaps.

**Placeholder scan**

No "TBD", "TODO", "fill in later" in any step. All HTML and CSS code is shown literally. All commit commands are concrete.

**Type / name consistency**

- CSS class `featured-card--text-only` introduced in Task 1, used in Tasks 4 and 5 — identical spelling.
- HTML class names (`featured-card`, `featured-content`, `featured-status`, `project-tag`, `featured-title`, `featured-url`, `featured-desc`, `featured-feats`, `featured-tools`, `tool-tag`) match the existing site convention shown by the earlier project cards in `index.html`.
- Title-naming rule applied consistently: About ¶2 uses short form; Experience entry (untouched in this plan beyond the one-word redaction) keeps the full LinkedIn title.

No issues found.
