# After-action report template (BCP)

Two modes. The exercise is the same; the recording rigor differs.

- **Readiness mode** — informal drill. Lighter. Skip the metadata header and attestation.
- **Evidence mode** — the annual SOC 2 continuity exercise. Built to drop into an evidence repo and survive auditor scrutiny. Include everything below.

Produce a clean standalone document (a Word doc if the environment can produce one, otherwise markdown). Keep styling **plain** — black/near-black text, clean tables, minimal color. It should read like a record and read well to someone who wasn't in the room.

## Structure

### Title
`Business Continuity Tabletop Exercise — After-Action Report`
Subtitle: company name and date.

### 1. Exercise metadata — **evidence mode only**
A compact block at the top; auditors look here first.
- **Date conducted** — the actual date of the session, never estimated
- **Facilitator** — the person who ran the session, not the AI tool. An AI assistant helping run it goes under exercise type.
- **Participants** — name and role for each.
- **Duration** — measured from the session (start and end time), never estimated
- **Scenario** — one-line summary of the disruption exercised.
- **Exercise type** — tabletop (discussion-based); if an AI assistant helped run it, say so and name it, e.g. "AI-assisted (name of the tool)".
- **Critical functions exercised, with RTO / RPO** — the functions the scenario tested and the recovery objectives the team was held against (even if those objectives were established for the first time during the session — note that, because "objectives were undefined before this exercise" is itself a finding).

In readiness mode, a single line (date / who / scenario) is plenty.

### 2. Scenario summary
A short narrative of the disruption as it unfolded, including the injects introduced (e.g., outage duration escalations, a failed restore, an SLA invocation). A few sentences to a short paragraph.

### 3. How the response unfolded
Summarize what the team did well and where they stalled across the phases that were exercised (declare/detect → impact assessment → continuity measures → communication → recovery & restore → return to normal). Factual and specific — name the moments. Don't pad.

### 4. What went well
A short, honest list. Teams need to see what already works. Don't invent strengths.

### 5. Gaps identified
The gaps, and *only* the gaps — fixes live in Section 6. Separating them stops the section reading like a wall of failure.

Record **only gaps the participants confirmed** during the review — a tolerance they admit is undefined, a restore they admit is untested, a dependency they admit has no fallback, a documented fact. Never record a facilitator *assumption*. Unconfirmed suspicions go under a separate **"Areas to verify"** heading, not among findings — in an evidence artifact an unverified finding is worse than a missing one.

**Group the confirmed gaps into *People*, *Process*, and *Technology*.** People gaps are key-person / bus-factor risk — one person who can deploy, holds cloud root, knows the restore steps, or controls the registrar, bank, or billing. Process gaps are about authority, ownership, customer/SLA communication, undefined recovery objectives, vendor management, and documentation. Technology gaps are about systems and capabilities — backups, restore, failover, redundancy, monitoring, runbooks. People is its own category on purpose: for a small team, "only one person can recover us" is the single most dangerous continuity gap, and it disappears if you fold it into "process." Within each group, order by consequence, worst first. For each:

> **Gap:** [what was missing or broke down]  *[severity: High / Medium / Low]*
> **Consequence:** [what this would cost in a real disruption — be concrete, in recovery-time and customer terms]

Frame at the **consequence level**, not as a checklist item. "No tested backups" is a checklist item; "no one has ever run a restore, so a data-loss event means an unknown amount of permanent loss and an unknown time to recover" is the consequence — and the consequence is what makes the team act.

### 6. Recommendations and action items
The fixes, paired one-to-one with the gaps. In **evidence mode**, a table: **Recommendation · Type (People/Process/Technology) · Owner · Target date · Status (Open)**. Owner + date is what auditors scrutinize — it's the difference between "we ran a tabletop" and "we ran one and closed the loop." If the team can't assign an owner or date, that hesitation is worth noting.

For the **Process** gaps, note whether the team opted for targeted edits to their continuity/DR plan or a redraft/first draft (see the plan follow-up step in SKILL.md), so the evidence trail connects each process gap to how the plan was corrected. **People** gaps map to cross-training and access/succession changes; **Technology** gaps (backups, failover, restore, redundancy) are engineering work tracked here, not plan text.

In readiness mode, a simple prioritized list is fine.

### 7. Attestation — **evidence mode only**
A closing line the participants stand behind, e.g.:

> The individuals listed in Section 1 participated in this business continuity tabletop exercise on [date] and reviewed the gaps recorded above. The confirmed gaps and remediation owners reflect the outcomes of that exercise; suspected items that could not be confirmed are recorded separately as Areas to verify.

With a single participant, write it in the singular ("The individual listed in Section 1 participated..."). A small participant / role / date grid underneath works well. This makes the document self-contained as evidence.

### Appendix: gap log — optional
The running gap log kept during the session, as written at the time. It's the contemporaneous record behind Sections 5 and 6, and an auditor may ask for it.

## Tone

Honest over flattering. The report's value is proportional to how truthfully it names gaps and how concretely it states recovery consequences. A clean-looking report that hides the holes fails the team at the worst possible moment.
