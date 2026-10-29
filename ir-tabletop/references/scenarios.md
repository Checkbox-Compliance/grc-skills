# Scenario archetypes and injects

This file helps you (a) pick the scenario that bites hardest for a given business, and (b) escalate it with realistic injects.

## How to choose

Match the scenario to **what the company would most hate to lose or explain**. The research you did on the business tells you this. A quick mapping:

| If the business... | The scenario that bites hardest |
|---|---|
| Holds customer PII / runs a consumer or B2B app | **Data breach / exfiltration** — attacker accessed the customer DB |
| Is fintech, payments, payroll, or holds financial data | **Data breach** or **business email compromise** (fraudulent payment) |
| Is healthcare / holds PHI | **Data breach** with regulatory clock (notification deadlines) |
| Ships software / is a dev tool / holds source code | **Source code or CI/CD compromise** — leaked secret, poisoned dependency, prod access via a CI token |
| Runs critical customer-facing infra (uptime is the product) | **Ransomware / destructive intrusion** — systems encrypted or wiped |
| Is small with heavy SaaS reliance and few engineers | **Account takeover** — phished Google/Okta admin, or a key engineer's laptop compromised |
| Handles money movement or vendor payments | **Business email compromise** — spoofed founder asks finance to wire funds |
| Ships AI features on customer content (assistants, agents, summaries) | **AI feature abuse** — prompt injection, a leaked model-provider key, or an agent acting outside its scope |

When two fit, pick the one with the worst *consequence-level* story for their specific customers, and mention the runner-up so they know it's on the menu.

## The archetypes

Each is a starting frame — adapt the specifics to the company's real stack and data.

### Data breach / exfiltration
Surfaces as: a security researcher emails claiming they can access customer records; or unusual egress in logs; or a customer asks why their data showed up somewhere. Core tensions: *Can you even confirm what was accessed?* (most early teams can't — that's the finding). Scope of affected customers. Notification obligations and timing. Evidence preservation vs. the urge to "just fix it."

### Ransomware / destructive intrusion
Surfaces as: systems unresponsive, a ransom note, or prod data gone. Core tensions: Do backups exist, are they current, and are they *also* reachable by the attacker? Who decides whether to pay? How long can the product be down before customers leave? Restoring vs. preserving forensic evidence.

### Source code / CI-CD compromise
Surfaces as: GitHub flags an exposed secret; or a dependency ships malicious code; or someone notices an unfamiliar commit / deploy. Core tensions: What did that leaked credential have access to? Can you tell what the attacker did with prod access? Rotating secrets at speed. Whether the malicious code already reached customers.

### Account takeover (identity)
Surfaces as: an impossible-travel login alert; a teammate locked out; or MFA prompts no one initiated. Core tensions: Blast radius of one compromised identity (especially an admin). Whether you can force a global session/credential reset. What that account could reach — and whether you have logs to know what it did.

### Business email compromise / fraud
Surfaces as: finance gets a wire request "from the founder," or a vendor's bank details "changed." Core tensions: Out-of-band verification (is there a process, or just trust?). Who can authorize payments. Whether it's purely fraud or paired with an actual account compromise.

### AI feature abuse
Surfaces as: a customer reports the assistant showed them another customer's data; the model provider's bill spikes overnight; an agent or connected tool made changes nobody asked for. Core tensions: Can you tell which prompts, tools and customers were involved, or are prompts and outputs not logged? Can you turn the feature off for one customer, or only for everyone? Was the model-provider key scoped and capped, and who can rotate it? Does the provider's own data handling make this their incident as well as yours?

## Injects (escalation library)

Drop these mid-exercise to test muscles the team would rather skip. Pick 3–4 that pressure different phases. Time them for when the team is getting comfortable.

**Time / pressure**
- "It's now 9pm on a Friday and the one person with prod access is unreachable."
- "You're 18 hours in and still can't confirm scope. Your biggest customer's security team just emailed asking for a status update."

**Public / comms**
- "A customer just posted about the outage on X and it's getting traction."
- "A journalist emails asking to confirm a breach. You have 2 hours before they publish."

**Stakeholder**
- "A board member heard secondhand and is asking the founder directly what's going on."
- "Your largest customer's contract has a 24-hour breach notification clause. The clock may have already started."

**Twist / deepening**
- "The backups you were about to restore from are also encrypted / also compromised."
- "The attacker emails you directly, proving they still have access."
- "While investigating, you find this isn't new — the earliest suspicious activity is three weeks old."

**AI features**
- "The model provider emails: your API key was used from an unknown network, and usage is 40 times normal."
- "A screenshot is circulating of your assistant answering one customer with text from another customer's documents."
- "You find the agent integration has had write access to customers' connected tools the whole time, not the read-only access you assumed."

**Legal / regulatory**
- "Your largest customer's counsel asks whether this triggers notification obligations in [the relevant jurisdiction/regulation for their business]. Does anyone know the answer — or who would?" (Record the deadline only if the team can source it; otherwise it's "to verify with counsel".)
- "You realize you need to preserve evidence, but someone already started wiping and rebuilding the affected box."

Use injects to manufacture the moments where gaps live: the comms gap, the legal/notification gap, the evidence-preservation gap, the single-point-of-failure gap. Those are usually the most valuable findings for an early team.
