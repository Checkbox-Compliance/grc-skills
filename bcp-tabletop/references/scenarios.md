# BCP scenario archetypes and injects

This file helps you (a) pick the disruption that bites hardest for a given business, and (b) escalate it with realistic injects. Unlike the security tabletop, these scenarios are mostly non-adversarial — the enemy is downtime, dependency, and the clock.

## How to choose

Match the scenario to **the single dependency or function that, if lost, stops this business**. The dependency research tells you this. A quick mapping:

| If the business... | The disruption that bites hardest |
|---|---|
| Runs a live service customers depend on minute-to-minute | **Cloud region / provider outage** — the product is simply down |
| Depends on a critical third party in the request path (auth, DB host, payments) | **Critical-vendor outage** — a dependency you don't control goes dark with no ETA |
| Is an AI product (inference, voice, agents) | **Model / inference / telephony provider outage** — the core capability is gone even though your own infra is fine |
| Has a tiny team where one person owns deploys/infra | **Key-person unavailability** — the only person who can fix it is unreachable (the bus-factor test) |
| Holds important customer or operational data | **Data loss / failed restore** — a bad deploy or deletion, and the backup is older or more broken than assumed (the RPO test) |
| Has SLAs or strong uptime promises | **Extended outage / SLA breach** — not catastrophic, but long enough to breach commitments and shake trust |
| Depends on a physical site or region for key staff | **Workspace / connectivity loss** — extended power/internet/office loss for a key location |

When two fit, pick the one with the worst recovery-time story for *this* business, and mention the runner-up so the team knows it's on the menu.

## The archetypes

Each is a starting frame — adapt to the company's real dependencies.

### Cloud region / provider outage
Surfaces as: the product is down, dashboards are dark, the provider's status page shows a regional event. Core tensions: Is there failover to another region/provider, is it actually configured, and has anyone tested it? How long until it's back, and is that within the customers' tolerance? Who decides to wait vs. fail over?

### Critical-vendor / dependency outage
Surfaces as: the product is up but broken — logins fail (auth provider), queries error (database host), payments decline (processor). Core tensions: Did the team even know they had a hard single dependency there? Is there any fallback or degraded mode? The vendor controls the timeline and may give no ETA — what do you tell customers while you wait on someone else?

### Model / inference / telephony provider outage (AI products)
Surfaces as: the core AI capability stops — the agent can't respond, calls can't connect — while your own infrastructure is perfectly healthy. Core tensions: Is there a secondary provider or a graceful degraded mode, or is the product simply non-functional? This is the dependency AI-native teams most often haven't planned a fallback for.

### Key-person unavailability (bus factor)
Surfaces as: something breaks and the one person who knows how to deploy, restore, or access production is unreachable — on a plane, sick, or gone. Core tensions: Can anyone else act? Is access documented and shared (break-glass), or locked in one person's head and credentials? This is the most common and most dangerous early-stage continuity gap.

### Data loss / failed restore (the RPO test)
Surfaces as: a bad migration, an accidental deletion, or corruption — and now you need the backup. Core tensions: Do backups exist, when were they last *tested* (not just configured), how old is the data you'd actually recover (RPO), and how long does a restore take (RTO)? "We have backups" and "we have tested, recent, restorable backups" are very different claims.

### Extended outage / SLA breach
Surfaces as: an outage that isn't catastrophic but drags — hours, not minutes. Core tensions: At what point do SLAs breach, customers churn, or trust erode? Is there a status page and a customer-communication cadence, or silence? When does someone decide this is now a business event, not just an engineering one?

## Injects (escalation library)

Drop these mid-exercise to test muscles the team would rather skip. Pick 3-4 that pressure different phases and the recovery objectives.

**Duration / clock**
- "It's been an hour with no resolution. Your stated RTO — if you have one — just passed."
- "The outage is now into hour eight, crossing into the workday for your biggest customers."

**Dependency / cascade**
- "The vendor's status page still says 'investigating' with no ETA. You don't control the fix."
- "While working the first outage, a second dependency you rely on also degrades."

**Recovery / RPO**
- "You go to restore from backup — the most recent good one is from 26 hours ago. Is that within tolerance?"
- "The restore runs, but it's the first time anyone's actually tried it, and it's failing partway."

**People**
- "The one engineer who set up the failover is unreachable for the next four hours."
- "It's 2am and your entire on-call is one person who's now been awake for 18 hours."

**Customer / business**
- "Your largest customer invokes their SLA and asks, in writing, for a status and an ETA."
- "A customer posts 'is anyone else down?' and it starts gaining traction."
- "It's payroll day / end of quarter, and the disruption touches a function that can't simply wait."

Use injects to manufacture the moments where continuity gaps live: the undefined recovery objective, the untested restore, the single-region or single-vendor dependency, the key-person bottleneck, and the silent-to-customers comms gap. Those are usually the most valuable findings for an early team.
