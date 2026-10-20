# GTM Bot Team Template (by Clayworks)

A reusable template for running signal-based cold outbound (email, LinkedIn and calling) with a team of AI bots and a human in the loop. It is the sanitized version of the setup Joy Victoria runs at [Clayworks](https://clayworks.io). This repo holds roles and instructions only: no credentials, lead data or client data.

## The architecture
- **Chief of Staff bot (the "Taskmaster")** is the only bot that talks to the human operator. It delegates work to eight stage bots, verifies each handoff, and brings the operator only the decisions that matter.
- **Stage bots (Stage 2 to Stage 9)** each own one step of the production line. They take work only from Chief of Staff and report back at every handoff.
- **Per-client Helper bots** hold each client's memory (decisions, holds, open items, context file), so one client's data never leaks into another's work.
- **Human approval gates:** a person approves every launch, every send, every credit or purchase, and every live change. Bots draft; humans decide.

## Roster
| Bot | Folder | Job |
|---|---|---|
| Chief of Staff (Taskmaster) | [chief-of-staff](chief-of-staff/INSTRUCTIONS.md) | Delegates, verifies, talks to the operator, runs the playbook |
| Stage 2 Data Intake | [stage-2-data-intake](stage-2-data-intake/INSTRUCTIONS.md) | ICP, offer, buckets, campaign plan |
| Stage 3 Email Infra | [stage-3-email-infra](stage-3-email-infra/INSTRUCTIONS.md) | Domains, mailboxes, warm-up, DNS |
| Stage 4 Company TAM | [stage-4-company-tam](stage-4-company-tam/INSTRUCTIONS.md) | Build the target company list with dated signals |
| Stage 5 People TAM | [stage-5-people-tam](stage-5-people-tam/INSTRUCTIONS.md) | Find and verify the people at those companies |
| Stage 6 Copywriting | [stage-6-copywriting](stage-6-copywriting/INSTRUCTIONS.md) | Campaign strategy and copy |
| Stage 7 Outreach | [stage-7-multi-channel-outreach](stage-7-multi-channel-outreach/INSTRUCTIONS.md) | Build campaign DRAFTs (never launches) |
| Stage 8 QA | [stage-8-qa](stage-8-qa/INSTRUCTIONS.md) | List, copy, pre-launch and live deliverability QA |
| Stage 9 Skills | [stage-9-skills](stage-9-skills/INSTRUCTIONS.md) | Reply triage, weekly rhythm, reporting, learning loop |

Stage 1 (connecting tools) has no bot; its kickoff is folded into Stage 2.

## How a campaign flows
Chief of Staff -> S2 Intake -> (S3 Infra if no warm inboxes) -> S4 Company TAM -> S5 People TAM -> S8 QA (list) + S6 Copy -> S8 QA (copy) -> S7 Outreach DRAFT -> S8 QA (pre-launch) -> the operator approves and launches -> S9 replies, rhythm and reporting -> feedback to S2, S6 and S8 -> offboarding when a client ends.

Failures go back: S8 sends list problems to S5, copy problems to S6 and infra problems to S3.

Full stage-by-stage detail, approval gates and scenarios: [docs/campaign-process-map.md](docs/campaign-process-map.md).

## How to use this template
1. Create one bot per folder (Chief of Staff, Stages 2 to 9) in your agent platform and paste its `INSTRUCTIONS.md` as the bot's instructions.
2. Replace the placeholders: `<BOT_ID_*>` with your bots' ids, `<WORKSPACE>` with your shared working folder, `<CLIENT>` with a client slug, `<APPROVER>` and `<DELIVERABILITY_LEAD>` with the people on your team, `<SIGNAL_TOOL>` with your signal/monitoring source.
3. Create one Helper bot per client (plus one company-wide Helper) and give each its own client context file.
4. Swap the tool names (Smartlead, Clay, Blitz, Apollo, InboxKit, CloudTalk, Client Hub and so on) for your own stack.
5. Store API keys only as platform secrets. Never put them in these files.
6. Keep the approval gates. Run a 10 to 50 prospect pilot through the whole chain before scaling.

## Rules for every bot
- No sending, launching, buying or credit spend without the operator's explicit approval.
- No API keys, tokens or passwords in files or chat.
- No em or en dashes in output.
- Client data stays inside that client's own account.

## Credit
Built by Joy Victoria, Sr GTM Engineer at [Clayworks](https://clayworks.io). Want help running this for your team? Reach out to Joy or Clayworks. MIT licensed, see [LICENSE](LICENSE).
