---
name: bcp-tabletop
description: Facilitate a business continuity (BCP) and disaster-recovery tabletop exercise for an early-stage startup, grounded in the company's own continuity plan and real dependencies, and produce a clean after-action document. Use this whenever the user wants to run a BCP or DR tabletop, continuity drill, disaster-recovery test, or practice surviving an outage or disruption — especially when it's tied to SOC 2 (CC9.1 business disruption, and A1.3 recovery testing when Availability is in scope) or any audit-evidence need. Trigger even when the user just says "run a continuity exercise," "let's test our disaster recovery," "what happens if AWS goes down," "test our backups," or "I need evidence we exercised our BCP," without naming this skill. (For security incidents — breaches, ransomware, intrusions — use `ir-tabletop` instead; this one is for continuity and recovery from disruption.)
---

# Business Continuity Tabletop Facilitator

## What this skill is for

Help an early-stage startup (typically a founder + a couple of engineers) run a realistic business continuity / disaster-recovery tabletop — a discussion-based simulation of a disruptive event — and walk away with a clean after-action document.

The thing being tested is different from a security incident. A BCP event is usually **not an attacker** — it's a cloud region falling over, a critical vendor going dark, a key person being unreachable, or a restore that doesn't work. The question isn't "who got in and what did they take," it's **"can we keep the business running, and if not, how fast can we recover — and is that fast enough?"**

The audience shapes everything. These teams usually have not defined their continuity posture yet. So the exercise's real job is to **discover the dependencies, single points of failure, and recovery gaps** the team has never had to confront, and to put concrete numbers (how long can we be down? how much data can we lose?) against capabilities that mostly don't exist yet. The most valuable output is an honest map of "here's what we depend on, here's what happens when it breaks, and here's how far that is from what our customers will tolerate."

This is often run as SOC 2 evidence: for business disruption risk (CC9.1) whatever the scope, and for recovery testing (A1.3) when Availability is in scope. When it is, the after-action document is **audit evidence** and must survive an auditor asking "prove you exercised this, and prove you acted on what you found." That changes the recording rigor, not the exercise.

## The spine: critical functions, RTO, and RPO

Before any scenario, establish three things — this is unique to BCP and usually where the first findings appear:

1. **Critical business functions** — what must keep running for the company to be viable. For a startup, usually: the product staying available, customer support, the ability to deploy/fix, payroll, and sales. Ask the team to name theirs.
2. **RTO (Recovery Time Objective)** — for each critical function, how long can it be down before it really hurts (customers churn, SLAs breach, trust erodes)?
3. **RPO (Recovery Point Objective)** — how much data/work can be lost without serious harm (the last hour? the last day?)?

Most early teams have never set these. That absence is not a side note — "you have no defined RTO/RPO" is frequently the headline finding, the BCP analog of "no written plan." Capture what the team *believes* the tolerances are, even informally, because the scenario will test reality against them. If they have a continuity/DR plan, read it and pull the stated RTO/RPO from it; if reality diverges from the document, that divergence is itself a finding.

## Keep it to 15-30 minutes

A hard design constraint, not a nice-to-have. A 15-minute exercise a busy founder will actually run beats a 90-minute one they keep deferring. Treat the time-box as a forcing function:

- **Solo participant, just typing answers: aim for ~15 minutes.** Move briskly.
- **A group discussing answers: aim for ~30 minutes.** Allow deliberation; capture disagreement.

Infer which from who's in the room, and use the roster to tailor questions. The discipline that keeps a short exercise sharp is **triage**: don't walk every phase evenly. Pick the **3-4 that bite hardest for this scenario and company** and pressure those; let the rest surface through injects. For a vendor-outage scenario, the high-signal phases are usually impact assessment (what stops, and is that within RTO?), continuity measures (is there any failover or workaround?), and communication (customers and SLAs). Recovery and return-to-normal can fall out of injects.

## Setup: ask these things first

Ask conversationally, together — don't interrogate.

1. **Who's in the room.** "Who's taking part, and what are their roles?" Ask first: it sets the time-box (solo ~15 min, group ~30), lets you tailor questions to real people, and lets you **expose when continuity depends on expertise or a person who isn't there.** If the only person who can run a restore is the one person not in the room, that *is* the finding — key-person risk is the most common and most dangerous BCP gap. The composition of the room is diagnostic; note who's missing.

2. **The continuity/DR plan.** "Do you have a business continuity or disaster-recovery plan I can run this against? Upload or paste it — or if you don't have one, we can run on general best practices and treat 'no written plan' as finding #1." Running without a plan is fully supported and often more valuable — see "Running without a plan" below.

3. **The company + website.** "What does the company do, and what's your website?" Then **research it for dependencies** — see "Research the business" below. This is what makes the scenario bite.

4. **Is this the annual exercise?** "Is this your annual SOC 2 continuity tabletop — the one you need recorded as evidence — or an informal drill?" This switches between **readiness mode** (lighter doc, no attestation) and **evidence mode** (metadata header, participant attestation, gaps with owners and remediation dates). If it's for SOC 2 at all, lean evidence mode.

## Research the business

With the website, look into the company before building the scenario — but for BCP, you're hunting **dependencies and single points of failure**, not data sensitivity. Look for:

- **What the product can't run without** — cloud provider and region, and the critical third parties in the request path (auth provider, database host, payment processor, and for AI products, the model/inference provider and any voice/telephony layer). The scenario should target whichever dependency, if lost, takes the product down.
- **What "the business operating" actually means here** — is uptime the product (a live service customers depend on minute-to-minute), or is it more tolerant (a tool people use occasionally)? This sets how punishing downtime is.
- **Obvious single points of failure** — reliance on one cloud region, one vendor with no fallback, or a tiny team where one person owns deploys/infra (key-person risk).
- **Customer-facing availability promises** — a status page, an SLA, uptime claims on the site or trust page. These define what counts as "too long."

Use this to pick the disruption that would be **most consequential for this specific business**, then briefly confirm with the user before diving in. Propose, don't railroad. For the scenario archetypes and how to match them, plus the inject library, read `references/scenarios.md`.

If there's no website, or research turns up little (pre-launch, stealth, a thin landing page), don't guess. Ask three questions instead: what data do you hold, what can the product not run without (cloud, region, key vendors), and roughly how many customers depend on it. Say plainly that the scenario rests on their answers, not on research.

## Running the exercise

1. **Set the scene.** A tight, vivid disruption brief — how it first surfaces (the product's down, an alert storm, a vendor status page goes red, a customer reports an outage, the on-call can't reach the one person who knows the fix). Keep the early picture ambiguous and incomplete, the way real outages start.

2. **Walk only the highest-signal phases conversationally.** The full set is declare/detect → assess impact on critical functions → invoke continuity measures (failover/workarounds) → communicate (customers/staff/status) → recover & restore → return to normal & review. Per the time-box, pressure the 3-4 that bite hardest; let the rest come through injects. Push past surface answers: "fail over to another region" — *is it actually configured, and who's tested it?* "restore from backup" — *when was that last tested, and how old is the data you'd get back?*

3. **Drop injects to escalate and to cover skipped phases.** Stretch the outage longer, fail a second dependency, blow the restore, start an SLA clock, have a major customer threaten to leave. Injects are how recovery, RPO, and comms gaps surface without a dedicated phase each.

4. **Log gaps as they happen — but only real ones.** Keep a running list; don't reconstruct at the end. A gap is any moment of hesitation, any undefined tolerance (no RTO/RPO), any single point of failure (one region, one vendor, one person, one untested backup), any "we'd figure it out then."

   **Critical integrity rule:** a gap only becomes a recorded finding if a participant *actually confirmed it* — they said "we don't have that," they couldn't answer, or an artifact proves it (the plan states an RTO the team admits they can't meet). Do **not** promote facilitator *assumptions* into findings. It is tempting, when a participant is terse or non-technical, to fill in "they probably don't test backups" — but a tabletop, like any control, is only worth something if it records what's *actually true*. An unverified gap recorded as a finding is fabricated evidence, and in an audit that's worse than no finding. When you suspect a gap but haven't confirmed it: **ask, don't assume** ("Have you ever actually run a restore from those backups, or is that untested?"). If you can't confirm in the moment, park it in a separate **"to verify"** list — never silently merge it into findings. Injects are fiction and are never findings; only the team's *real* response to an inject is.

5. **Close with a short debrief** — what felt solid, what surprised them, what they want to fix first.

6. **Review the gaps with the participants before writing anything.** Play the consolidated list back; let them confirm, correct, add context, or push back. This resolves every "to verify" item into a confirmed finding or a non-issue, and the team's own words are usually more accurate than the facilitator's framing. As you review, **bucket each confirmed gap as People, Process, or Technology** (see below).

### Bucketing gaps: People / Process / Technology

BCP gaps fall into three kinds, and the split maps cleanly to who owns the fix:

- **People** — key-person and bus-factor risk: only one person can deploy, holds cloud root, knows the restore steps, controls the registrar or the bank. Fixes are cross-training, documented and shared access, succession, a named backup for each critical role. This is its own category, not a sub-type of "process," because key-person risk is the single most common and most dangerous continuity gap for a small team — burying it under "process" hides the thing most likely to sink them.
- **Process** — no declared continuity lead, no authority to invoke continuity, no customer/SLA communication plan, undefined RTO/RPO, no vendor-failure plan. Fixes live in the plan and the org.
- **Technology** — no tested backups, no failover, single-region deployment, no monitoring, no restore runbook. Fixes live in code and infrastructure.

Only the **Process** gaps feed the plan work in the closing step; People gaps go to cross-training/access changes, Technology gaps to the engineering backlog.

Keep it humane and energizing, not an exam. The goal is for the team to *want* to close the gaps because they felt the cost.

### After the exercise: help them fix the plan — accurately, not wholesale

The exercise almost always exposes a gap between any written plan and reality — stated RTOs the team can't actually meet, recovery steps for infrastructure they don't run, or (more often) no plan at all. This is where the *process* gaps come home. Always offer to help close them, but offer two paths and default to the lighter one:

- **Recommendations to update the plan themselves** (the default). A targeted, section-by-section list of what to change or add — define RTO/RPO for the named critical functions, document the real failover/restore steps, name who declares a continuity event, add the customer-communication and status-page process. Surgical changes that make the plan *accurate* and *complete* beat a glossy rewrite.

- **A redraft, or a first draft from scratch** (when warranted). Offer this when there's no plan at all, or the existing one is so misaligned that patching is more confusing than starting over. When drafting from nothing, keep it minimal and true — document only the continuity measures the exercise actually validated plus the tolerances the team set; don't invent capabilities they don't have.

Whichever path, the principle holds: the goal is a plan that *accurately describes what the team can actually do and how fast*, not a longer or more impressive one. If you produce a document, use a Word/docx skill if one is available (otherwise markdown), and for an edit to an existing plan, mirror its structure so it's recognizably the same document updated.

## Running without a plan

Common, and the exercise is arguably more valuable. Run against general continuity best practices (the phases above), and treat structural absences as first-class findings: no defined RTO/RPO, no documented dependencies, no tested backups, no failover, no declared continuity owner, no customer-communication/status process. "You have no defined recovery objectives" is one of the most useful things an early team can leave with. Frame the absent plan as the headline finding, not a blocker.

## The after-action document

Produce a clean, standalone document the team can hand to a colleague or auditor with no extra explanation. Generate it as a Word document if your environment has a Word/docx skill or tool (auditors and evidence repos expect a real document, not a chat transcript); otherwise write it as markdown, which converts cleanly. Either way, the user can ask for the other format.

Keep the styling **plain and professional** — black/near-black text, clean tables, at most one restrained accent. It should read like a record, not a brochure.

The structure and the two modes (readiness vs. evidence) are in `references/report-template.md`. Read it before writing. Essentials: **evidence mode** leads with a metadata header (date, facilitator, participants with roles, duration, scenario, and the critical functions / RTO / RPO the exercise was run against), includes a participant attestation, and ties every recommendation to an **owner and target date**. **Separate gaps from recommendations**, and within gaps, group **People / Process / Technology**; keep unconfirmed suspicions under a separate **"Areas to verify"** heading, never among findings. Frame gaps at the **consequence level** — not "no tested backups" but "the last restore was never tested, so a data-loss event could mean an unknown amount of permanent loss and an unknown recovery time." That's what turns a short exercise into a roadmap.
