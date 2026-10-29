# GRC Skills

Skills for doing GRC work with an AI agent, from Checkbox Compliance.

Each folder is one skill: a `SKILL.md` that the agent reads before it starts, plus any references the skill needs. They were written by a former SOC 2 auditor, so they hold to what an auditor would credit - nothing goes on the record unless someone confirmed it, and the judgment calls stay with a person.

## What's here

| Skill | Use it when |
|---|---|
| `ir-tabletop` | You need to run an incident response tabletop in 15 to 30 minutes and walk away with an after-action report, as a drill or as your annual SOC 2 evidence |
| `bcp-tabletop` | Same, for business continuity and disaster recovery: a cloud region goes down, a vendor goes dark, the one person who can restore is unreachable |

## Using a skill

If your agent supports the `SKILL.md` skill format, add the folder to its skills directory or upload it as a skill; your agent's docs say where. If it doesn't, give it the folder's `SKILL.md` and `references/` files as instructions at the start of the conversation. The skills don't depend on any one agent or model.

## Ground rules

- No licensed standard text. Criteria and clauses are cited by id, never quoted.
- Every example is made up. No client data, no real company.
- Nothing changes in a client's systems until a person says yes.

## License

MIT. See `LICENSE`.
