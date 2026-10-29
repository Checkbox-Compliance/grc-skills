# After-action report template

Two modes. The exercise is the same; the recording rigor differs. Decide mode from the "is this the annual exercise?" setup question.

- **Readiness mode** — informal drill. Lighter. Skip the metadata header and attestation; keep it useful and honest.
- **Evidence mode** — the annual SOC 2 exercise. Built to be dropped into an evidence repo and survive auditor scrutiny. Include everything below.

Produce it as a clean standalone document (a Word doc if the environment can produce one, otherwise markdown). Keep the styling **plain** — black/near-black text, clean tables, minimal color. It should read like a record, not a brochure, and read well to someone who wasn't in the room.

## Structure

### Title
`Incident Response Tabletop Exercise — After-Action Report`
Subtitle: company name and date.

### 1. Exercise metadata — **evidence mode only**
A compact block at the top. Auditors look here first to confirm the exercise actually happened with real people.
- **Date conducted** — the actual date of the session, never estimated
- **Facilitator** — the person who ran the session, not the AI tool. An AI assistant helping run it goes under exercise type.
- **Participants** — name and role for each (e.g., "Sam Rivera, CTO"). This is what makes it defensible that the right people were in the room.
- **Duration** — measured from the session (start and end time), never estimated
- **Scenario** — one-line summary
- **Exercise type** — tabletop (discussion-based); if an AI assistant helped run it, say so and name it, e.g. "AI-assisted (name of the tool)"

In readiness mode, a single line ("Date / who was there / scenario") is plenty.

### 2. Scenario summary
A short narrative of the scenario as it unfolded, including the injects introduced. Enough that a reader understands what the team was responding to. A few sentences to a short paragraph.

### 3. How the response unfolded
Summarize what the team did well and where they stalled across the phases that were exercised. Keep it factual and specific — name the moments. This is the narrative spine; don't pad it.

### 4. What went well
A short, honest list. Early teams need to see what's already working, not just the gaps. Don't invent strengths — if it was thin, say so briefly.

### 5. Gaps identified
The gaps, and *only* the gaps — keep the fixes out of this section (they live in Section 6). Separating them this way stops the section from reading like a wall of failure and lets the team see the recommendations as a clean, ownable action list rather than a list of indictments.

**Only record gaps that were actually confirmed during the exercise** — something a participant couldn't answer, an invented-on-the-spot process, or a documented fact (e.g., the plan names a role the company doesn't have). Never record a facilitator *assumption* as a gap. In an evidence artifact, a fabricated or unverified finding is worse than a missing one. If the exercise surfaced suspicions that couldn't be confirmed in the room, list them under a clearly separate **"Areas to verify"** heading — not as findings — so the record stays honest about what is known versus what is suspected.

Where a gap is really about **missing expertise in the room** (no one who can make the legal/breach call, no security or comms owner), say so plainly — that's a capability/staffing finding, distinct from a broken process, and often the most important thing an early team learns.

Order gaps by severity / consequence, worst first. **Group them into *Process* and *Technical*** — process gaps are about authority, ownership, notification, and what's written down; technical gaps are about systems and capabilities. The split makes ownership obvious and maps the two kinds of fix (policy/org vs. code/infra), and it tells the reader at a glance which gaps the policy update in the follow-up will address. For each:

> **Gap:** [what was missing or broke down]  *[severity: High / Medium / Low]*
> **Consequence:** [what this would cost in a real incident — be concrete]

Frame every gap at the **consequence level**, not as a bare checklist item. "No mass token-revocation capability" is a checklist item; "every hour exposed tokens stay valid, anyone holding one can act as our customers in the systems we connect to" is the consequence — and the consequence is what makes the team want to fix it.

### 6. Recommendations and action items
The fixes, paired one-to-one with the gaps above. In **evidence mode**, present as a table: **Recommendation · Owner · Target date · Status (Open)**. The owner + date is the part auditors scrutinize hardest — it's the difference between "we ran a tabletop" and "we ran a tabletop and closed the loop." A recommendation with no owner reads as box-checking. If the team can't assign an owner or date in the room, that hesitation is itself worth noting.

In readiness mode, a simple prioritized list of fixes is fine.

For the **process** gaps specifically, note in the report whether the team opted for a set of targeted policy edits or a full redraft (see the policy follow-up step in SKILL.md), so the evidence trail connects each process gap to how the policy was corrected.

### 7. Attestation — **evidence mode only**
A closing line the participants stand behind, e.g.:

> The individuals listed in Section 1 participated in this incident response tabletop exercise on [date]. The gaps and remediation owners recorded above reflect the outcomes of that exercise.

With a single participant, write it in the singular ("The individual listed in Section 1 participated..."). This makes the document self-contained as evidence rather than something needing external corroboration. A small participant/role/date grid underneath works well.

### Appendix: gap log — optional
The running gap log kept during the session, as written at the time. It's the contemporaneous record behind Sections 5 and 6, and an auditor may ask for it.

## Tone

Honest over flattering. The report's value is proportional to how truthfully it names gaps — a clean-looking report that hides the holes helps no one and, in evidence mode, fails the team at the worst possible moment. Frame gaps as cheap-to-fix-now rather than as failures.
