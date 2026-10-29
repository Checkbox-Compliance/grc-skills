---
name: ir-tabletop
description: Facilitate an incident response tabletop exercise for an early-stage startup, grounded in the company's own IR plan and business context, and produce a clean after-action document. Use this whenever the user wants to run a tabletop, IR drill, incident simulation, or practice responding to a security incident — especially when it's tied to SOC 2 (the CC7 incident-response controls) or any audit-evidence need. Trigger even when the user just says "run a tabletop," "let's do an IR exercise," "test our incident response," or "I need evidence we practiced incident response," without naming this skill.
---

# Incident Response Tabletop Facilitator

## What this skill is for

Help an early-stage startup (typically a founder + a couple of engineers) run a realistic incident response tabletop — a discussion-based simulation of a security incident — and walk away with a clean after-action document.

The audience matters and shapes everything. These teams usually do **not** have a mature, battle-tested IR process. So the exercise's real job isn't to *grade* a polished process against a rubric — it's to **discover where the gaps are** and start building reflexes and muscle memory. The most valuable output is an honest list of "here's a moment where we had no answer, and here's what that would cost us in a real incident."

This is often run to satisfy a SOC 2 incident-response control. When it is, the after-action document isn't just a roadmap — it's **audit evidence**, and it has to survive an auditor asking "prove you actually did this, and prove you acted on what you found." That changes the recording rigor, not the exercise itself.

## The shape of a good tabletop here

Aim for **structured-light** facilitation. A full timed facilitator-script tabletop assumes a process exists to test; an open free-for-all discussion meanders and produces nothing concrete. The sweet spot for an early team:

- A realistic scenario, grounded in *this* company's actual business and stack
- Organized around the natural IR phases (detection → triage → containment → eradication/recovery → comms/legal → lessons learned), but walked conversationally, not on a stopwatch
- Punctuated by a few **escalating injects** — new facts dropped mid-exercise ("it's now 9pm and a customer just posted about it on X") that pressure-test the team's reactions
- With **continuous gap-logging**: every time the team hesitates, says "I don't know who'd do that," or invents a process on the spot, that's a finding — capture it in the moment

The facilitator's core move is to keep asking **"okay — specifically who does that, how, and with what?"** until either there's a real answer or a gap is exposed. Surface-level "we'd contain it" answers should be pushed on: contain it *how*, using *what access*, and who has it at 2am?

### Keep it to 15–30 minutes

This is a hard design constraint, not a nice-to-have. A 15-minute exercise a busy founder will actually run beats a 90-minute one they keep deferring — and deferring the annual exercise is the common failure. Treat the time-box as a forcing function:

- **Solo participant, just typing answers: aim for ~15 minutes.** No group deliberation to absorb time, so move briskly.
- **A group discussing answers in a room: aim for ~30 minutes.** Allow deliberation, capture where participants disagree.

Infer which case you're in from who's in the room (you asked first thing in setup), and use that roster to tailor questions to the actual people present. The thing that makes a *short* exercise still bite is **triage**: you cannot slow-walk all six phases in 15 minutes, so don't try. Pick the **3–4 phases where this specific scenario and company will reveal the most**, and pressure only those. Let the remaining phases surface naturally through injects rather than marching through them in order.

For example, in a customer-token-exposure scenario the highest-signal phases are usually triage (can they even scope what was accessed?), containment (can they revoke customer credentials fast?), and comms/legal (the notification clock). Detection and evidence-handling gaps then fall out of well-placed injects without needing their own dedicated phase. Marching all six phases in sequence is what blows the time budget while surfacing the same findings.

## Setup: ask these things first

Before running anything, get these. Ask them together, conversationally — don't interrogate.

1. **Who's in the room.** "Who's taking part, and what are their roles? Even just 'me — founder' and 'Jordan — head of eng' is enough." Ask this *first*, because the roster does three jobs: it sets the time-box (solo ≈ 15 min, a group discussing ≈ 30), it lets you tailor questions to the actual people ("Jordan, you're on-call — what do you do?"), and — importantly — it lets you **expose when the incident needs expertise that isn't in the room.** If it's just eng + founder, the comms/legal phase shouldn't only find a process gap; it should surface "there's no one here who can make this call," which is a finding about *capability and staffing*, not paperwork. The composition of the room is itself diagnostic — note who's missing for the kinds of decisions the scenario will demand (legal, comms, security, on-call coverage).

2. **The IR plan.** "Do you have an incident response plan I can run this against? You can upload it or paste it — or if you don't have one yet, we can run the exercise on general best practices and treat 'you don't have a written plan' as finding #1." Running without a plan is fully supported and genuinely useful for these teams — see "Running without an IR plan" below.

3. **The company + website.** "What does the company do, and what's your website?" Then **actually research it** — see "Research the business" below. This is what makes the scenario land instead of feeling generic.

4. **Is this the annual exercise?** "Is this your annual SOC 2 tabletop — the one you need recorded as evidence — or more of an informal readiness drill?" This is the single switch between **readiness mode** (lighter doc, no attestation) and **evidence mode** (full metadata header, participant attestation, findings with owners and remediation dates). When in doubt, ask; don't assume. If they're doing this for SOC 2 at all, lean toward evidence mode.

## Research the business

Once you have the website, look into it before building the scenario. You're trying to ground the exercise in plausible reality. Look for:

- **What they actually do** and who their customers are (B2B SaaS? consumer? fintech? healthcare? dev tools?)
- **What data they hold** that an attacker would want — customer PII, payment data, health records, source code, model weights, infra credentials. This drives which scenario bites hardest.
- **Their likely stack and surface area** — cloud provider, whether they're API-first, whether they have a customer-facing app, obvious third-party dependencies. Job postings, the engineering blog, and the docs/trust pages are gold for this.
- **Company stage and size** — a five-person team and a fifty-person team have very different realistic answers about who's on call.

Use this to pick the scenario that would be *most consequential for this specific business*, then briefly confirm it with the user before diving in. Propose, don't railroad: "Given you're holding [X], I'd run a [scenario] — that's where you've got the most to lose. Want that, or would you rather drill something else?"

For the menu of scenario archetypes and how to match them to a business, read `references/scenarios.md`. For the library of escalating injects, it's in there too.

If there's no website, or research turns up little (pre-launch, stealth, a thin landing page), don't guess. Ask three questions instead: what data do you hold, what can the product not run without, and roughly how many customers depend on it. Say plainly that the scenario rests on their answers, not on research.

## Running the exercise

1. **Set the scene.** Give a tight, vivid scenario brief — how the incident first surfaces (an alert, a customer email, a weird log line, a GitHub security notice). Keep the opening ambiguous, the way real incidents start. Don't hand them the full picture; make them work to establish what's actually happening.

2. **Walk only the highest-signal phases conversationally.** The full phase set is detection → triage → containment → eradication/recovery → comms/legal → lessons, but per the time-box above, pick the 3–4 that bite hardest for this scenario and company and pressure those. At each, put the team in the moment and ask what they'd *actually* do. Name names where you can ("Sam, you're the only one with prod access and you're on a flight — now what?").

3. **Drop injects to escalate and to cover the phases you skipped.** Every so often, introduce a complication that tests a different muscle: a deadline (regulatory clock), a stakeholder (a big customer, a board member, a journalist), a twist (the backup is also encrypted; the attacker emails you). Injects are how detection, evidence-handling, and comms gaps surface without spending a dedicated phase on each.

4. **Log gaps as they happen — but only real ones.** Keep a running list throughout; don't reconstruct it at the end. A finding is any moment of hesitation, any invented-on-the-spot process, any "we'd figure it out then," any single point of failure (one person, one key, one undocumented step). Note enough context to make it real later.

   **Critical integrity rule:** a gap only becomes a recorded finding if a participant *actually confirmed it* — they said "we don't have that," or they visibly couldn't answer, or the artifact in front of you proves it (e.g., the written plan names a role that doesn't exist). Do **not** promote facilitator *assumptions* into findings. It is tempting, especially when a participant is terse or goes quiet, to fill in "they probably don't have X" — but a tabletop, like any control, is only worth something if it records what's *actually true* about the environment, not what's plausible. Writing down an unverified gap as a finding is fabricating evidence, and in an audit it's worse than having no finding at all.

   So when you suspect a gap but haven't confirmed it: **ask, don't assume.** "Can you actually revoke every customer token in one action right now, or is that a 'we'd figure it out' situation?" Their answer either confirms the gap or removes it. If you must move quickly and can't confirm in the moment, park it in a separate **"to verify"** list — never silently merge it into the findings.

   The same rule covers **legal and regulatory clocks**. Don't state notification deadlines (breach laws, regulators, contract clauses) from memory as fact in the record. If the team or a document they provide gives the deadline, record it with that source; otherwise record the obligation as "to verify with counsel". Whether the team knew who to ask is the finding.

   Be especially careful with **injects**: an inject is a hypothetical you introduce to drive the scenario ("logging shows it was exposed six weeks"). The inject itself is fiction and is never a finding. What's a finding is the team's *real* response to it ("we wouldn't have logs to check that" — confirmed by them). Keep the line between the fictional scenario fact and the confirmed real-world gap sharp.

5. **Close with a short debrief** before writing the document — what felt solid, what surprised them, what they want to fix first.

6. **Review the gaps with the participants before writing anything.** Don't go straight from the exercise to the document. Play the consolidated gap list back to the team and let them respond — confirm, correct, add context, or push back. This step does two jobs. First, it's where parked "to verify" items get resolved into either confirmed findings or non-issues, which is what keeps the eventual report honest (see the integrity rule above). Second, the team's own words about a gap are often better and more accurate than the facilitator's framing — capture them. A gap the team disputes shouldn't be quietly recorded anyway; either they're right and it's not a gap, or you surface the disagreement and let them decide how to record it.

   As you review, **bucket each confirmed gap as either *process* or *technical*.** Process gaps are about who-decides, who's-notified, what's-written-down, escalation, and authority (e.g., "no one owns the customer-notification decision"). Technical gaps are about systems and capabilities (e.g., "can't revoke tokens in one action," "no access logging"). This split matters because it maps cleanly to ownership and to two different kinds of fix: process gaps usually get fixed in the *policy and the org*, technical gaps get fixed in the *codebase and infrastructure*. It also tells you which gaps are candidates for the policy work in the next step — process gaps are; technical gaps generally aren't.

Keep the whole thing humane and energizing, not like an exam. The goal is for the team to *want* to fix the gaps, because they felt the cost during the exercise.

### After the exercise: help them fix the policy — accurately, not wholesale

The exercise almost always exposes a gap between the *written* plan and how the team *actually* operates — template roles that don't exist (a General Counsel, an on-call ISM rotation, an HR Manager), an intake path no one uses, processes sized for a company ten times bigger. This is where the *process* gaps you bucketed come home. Always offer to help close them in the policy — but offer two paths, and default to the lighter one:

- **Recommendations to update the policy themselves** (the default). Give a targeted, section-by-section list of what to change — "replace the ISM-on-call language in §X with your real intake path," "remove the General Counsel / HR Manager / VP Brand sponsors and name the people who actually own the response," "add a customer-notification decision owner." This respects that a policy is a controlled document the team (and their auditor) already know; surgical amendments that make it *accurate* are usually better than a new document.

- **A redraft** (only when warranted). Offer this when the existing plan is so misaligned that patching it section-by-section would be more confusing than starting over — e.g., it describes a fundamentally different company, or it's a generic template they never really adopted. Frame the choice honestly: "I can either give you a list of precise edits to make your current policy accurate, or — if you think it's too far off to patch — redraft it from your real process. For most teams the edit list is the right call; a full redraw is for when the current doc isn't worth keeping."

Whichever path, the principle is the same: the goal is a policy that *accurately describes what the team actually does*, not a longer or more impressive one. Keep their good bones; change only what's untrue. If you do produce a redraft, use a Word/docx skill if one is available (otherwise markdown), mirror the structure of their original so it's recognizably the same document updated, and only touch the *process* content the exercise actually validated — don't invent new procedure.

## Running without an IR plan

If they have no written plan, don't bail — this is the common case and the exercise is arguably more valuable. Run it against general IR best practices (the standard phases above), and treat structural absences as first-class findings: no written plan, no defined on-call/escalation path, no communication tree, no decision authority for "do we notify customers." "You don't have a documented escalation path" is one of the most useful findings an early team can leave with. Frame the absence of a plan as the headline finding, not a blocker.

## The after-action document

Produce a clean, standalone document the user can hand to a colleague or an auditor with no extra explanation. Generate it as a Word document if your environment has a Word/docx skill or tool (auditors and evidence repos expect a real document, not a chat transcript); otherwise write it as markdown, which converts cleanly. Either way, the user can ask for the other format.

Keep the styling **plain and professional** — this is an evidence artifact, not a marketing piece. Black or near-black text, clean tables, at most a single restrained accent. Avoid heavy color or decorative palettes; an auditor wants something that reads as a record.

The structure and the two modes (readiness vs. evidence) are specified in `references/report-template.md`. Read it before writing the document. The essential differences: **evidence mode** leads with a metadata header (date, facilitator, participants with roles, duration, scenario), includes a participant attestation line, and ties every recommendation to an **owner and a target remediation date** — because an auditor scrutinizes whether the loop gets closed, and recommendations with no owner read as "we ran this to check a box." **Readiness mode** can drop the header and attestation and stay lighter.

Crucially, **separate gaps from recommendations** rather than interleaving them per finding. Present the gaps as one set (each: what was missing → what it would cost in a real incident), and the recommendations/action items as a separate set (each: the fix → owner → target date). This keeps the gaps list from reading like a wall of failure, gives the team a clean action list, and gives an auditor a clean list to check against next year. Frame gaps at the **consequence level**, not as a bare checklist — that's what turns a short exercise into a roadmap the team will actually act on.
