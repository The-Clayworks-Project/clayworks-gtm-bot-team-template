# Clayworks Campaign Process Map (stage by stage)

Prepared 15 Oct 2026 for the operator, to be turned into a shareable Miro board.
Sources: cold-outbound TEAM.md, PLAYBOOK.md, house-rules/ (common, stage-2 to stage-9, lead-magnets), bots/stage-N.full.md, the Clayworks Knowledge Base (6 Oct 2026) and Offboarding_Process.md (13 Oct 2026).
This file describes the process only. It has no client data, prices or credentials. Times are in the operator's timezone.

## 0. Big picture

Clayworks runs "pipeline as a service": signal-based outbound across email, LinkedIn and calling, handing clients qualified meetings, not leads.

One-line flow:

Intake (S2) -> Infra (S3, in parallel, only if no warm inboxes) -> Company TAM (S4) -> People TAM (S5) -> List QA (S8) + Copywriting (S6) -> Copy QA (S8) -> Outreach DRAFT (S7) -> Pre-launch QA (S8) -> the operator approves and launches herself -> Skills, replies and rhythm (S9) -> loop back to S2 / S6 / S8 -> Offboarding when a client ends.

Stage 1 (connecting tools) has no bot. Its kickoff skill is folded into Stage 2.

### Who runs it
- **Chief of Staff bot** is the delegator (the repo's "Taskmaster"). Every stage bot gets work only from it and reports back to it at each handoff. Stage bots never message clients, prospects or <APPROVER> directly.
- **Stage bots (S2 to S9)** own a step of the production line and keep working files in `<WORKSPACE>/profiles/<client-slug>/`.
- **Client Helper bots** (one per client, plus one company-wide) own client memory: decisions, holds, open items, the client's context file. Ask the Helper first for any client task, then brief the stage bot with what it said. After a stage changes the client's state, ask the Helper to log it.
- **People:** The operator approves every send, launch, live change and spend. <APPROVER> is final copy reviewer and approves live-campaign changes, mailbox rests and client-relationship calls. The relevant team lead must OK naming a client in copy and the scarcity line. <DELIVERABILITY_LEAD> leads deliverability investigations. The client approves its own copy or proof points where its file says so.

### Rules that apply at every stage
- No sending, launching, resuming, pausing, buying, importing to Client Hub, or credit spend without the operator's explicit approval relayed by Chief of Staff. Read-only lookups and drafts are fine.
- Spend is held for the operator: estimate credits first, run only after approval. Check each tool's pricing on your plan; Pronto, Apollo company search, Clay and similar cost credits.
- No API keys, tokens or passwords in files or chat (box secrets only).
- No em dashes or en dashes anywhere, including documents.
- One client's name, data or results never appear in another client's work.
- Newer dated decisions and Fireflies calls beat older files; say so and ask before acting.
- Every number in a document has a source and date; re-pull before quoting; unverified items are marked "to confirm".
- Each stage ends by saving its output file, handing to the next bot by id with a short brief (client, campaign, file paths, open questions), and reporting to Chief of Staff. Chief of Staff gives the operator one line: stage done, file path, next stage, what she must approve.

### Approval gates at a glance (the operator decides each, every time)
1. Mailbox or domain purchase (S3)
2. Any credit spend or paid enrichment (S4, S5)
3. Client Hub import, blacklist add, campaign plan stage move (S5, S7)
4. Copy approval (the operator, then <APPROVER> as final reviewer, client where required) (S6)
5. Creating the Smartlead DRAFT, adding leads, changing inbox settings (S7)
6. Launch: The operator presses Start herself (after S8 pre-launch pass)
7. Any live edit, pause, resume or adding leads to a live sequence (<APPROVER>'s OK too)
8. Send to a prospect: every reply, LinkedIn message or lead magnet to a prospect is sent by a person on the team, never a bot (S9)
9. Any change to a house rule

---

## Stage 2: Data Intake (ICP, offer, buckets, campaign plan)

**Purpose:** Turn a new client or new bucket into a complete profile and a campaign plan (who, why now, what offer), so every later stage has clear targeting.

**Inputs:** Request from Chief of Staff; client context file; Client Hub (tenant, campaign plans, contacts, blacklist, signals); Fireflies transcripts (sales call, internal syncs, client calls); Gmail and Drive; the client's onboarding form; the client Helper's history.

**Ordered steps:**
1. Read house-rules common.md, stage-2.md and the client's file in house-rules/clients/.
2. Pre-fill from existing sources before asking anything (Client Hub, Fireflies, Drive, Gmail). Decisions made on calls beat files.
3. Run the kickoff flow (folded Stage 1): infrastructure status (do warm inboxes exist?), profile, lead magnet, strategy.
4. Capture the profile: the client's definition of "qualified" (three things, from the onboarding form), meeting target and pilot terms, market and geography with hard exclusions, ICP firmographics and personas, exclusions (customers, hot pipeline, competitors, DNC, delivery geography, anyone already in a live sequence), cleared and not-cleared proof points, client language rules (banned words), channels (calling is always in scope), CRM for meeting sync.
5. Segment the market into slices (sub-industry, size, geography, stage, problem). One slice = one bucket = one signal or audience. Name with `<Client> - Bucket <N> - <Mon YYYY> - <signal or audience>`. Prefer real intent signals (open jobs, events, ranking data, competitor audiences); corporate news alone is weak.
6. Design the offer. Every campaign needs one. Reuse the client's existing lead magnet if it has one; otherwise design with Hormozi rules and leave room to escalate across touches.
7. Mark assumptions, list only what is missing, and ask the operator those questions in one message.
8. Write the outputs and propose the Client Hub campaign plan entry in the report (the operator or <APPROVER> creates or moves plans).

**Tools:** Client Hub, Fireflies, Gmail, Google Drive, web fetch for the client's site, client context files. Prospeo is not connected; record Apollo, Blitz and Clay friendly filters instead.

**Outputs:** `profiles/<client>/client-profile.yaml`, `lead-magnets.md`, `campaign-strategy.md` (if run), `campaign-plan.md`.

**Handoff:** To Stage 3 if new sending infrastructure is needed (in parallel), and to Stage 4 Company TAM. Report to Chief of Staff.

**Gates and rules:** Never invent client decisions, prices or cleared claims. Never mark calling out of scope. Always include an offer. Client Hub plan writes are proposed, not made. Warm-up must finish before launch.

---

## Stage 3: Email Infrastructure (domains, mailboxes, warm-up), only if needed

**Purpose:** Make sure enough warmed, healthy sending capacity exists for the campaign's volume before launch.

**Inputs:** Campaign plan and volume from Stage 2; existing mailbox health (InboxKit, Smartlead notes); client file blockers (rested mailboxes, open tickets).

**Ordered steps:**
1. Check existing capacity first. Skip this stage if warm mailboxes already exist.
2. Size the build by hand: contacts per month x emails per contact, at 2 mailboxes per domain, then domains and mailboxes needed. Standard new-client build is about 12 domains and 24 mailboxes on subdomains or lookalikes of the client's domain, with a dedicated sending server.
3. Generate candidate domain names and check availability (no approval needed). Names must not contain words the client bans.
4. Write the DNS checklist (SPF, DKIM, DMARC aligned) and the warm-up plan (2 to 3 weeks, so start at the same time as Stage 2).
5. Present sizing and cost to Chief of Staff. Wait for the operator's approval before anything is bought.
6. After approval: buy and set up through InboxKit, connect to Smartlead, run warm-up.
7. Default send limit is 25 a day per mailbox unless the client file says otherwise. Keep risky lists off the domains that book meetings.

**Tools:** InboxKit (domains, mailboxes), Smartlead (warm-up, connection), DNS checks. Dynadot, Zapmail and Primeforge are not our stack.

**Outputs:** `profiles/<client>/infra-plan.md` (sizing math, domain names, inbox count, DNS checklist, warm-up plan, cost estimate, what needs approval).

**Handoff:** Inbox setup (warm-up, signatures, tags) to Stage 7; domain auth check to Stage 8; sending capacity to Stage 4 so list size matches. Report to Chief of Staff.

**Gates and rules:** Buying any domain or mailbox needs the operator's approval after pricing. No Gmail mailboxes back in campaigns without a placement test. Resting or removing mailboxes is a live change (<APPROVER>'s OK plus the operator). Sender identity follows the client file.

---

## Stage 4: Company TAM (accounts and signals)

**Purpose:** Build the list of qualified target companies, each with a dated, sourced signal.

**Inputs:** `client-profile.yaml` and `campaign-plan.md` from Stage 2; sending capacity from Stage 3.

**Ordered steps:**
1. Read house rules and client file. Pick the source by asking "where do these prospects live?" (LinkedIn, job boards, event pages, app stores, registries, competitor audiences).
2. Search in tool order: Blitz, then Apollo, then Clay (credits, ask first), then free public sources (job boards, charts, event speaker pages, case studies, filings). <SIGNAL_TOOL> is for monitoring signed clients only. Competitor follower lists are pulled manually (LeadsForge).
3. Apply hard gates from the client's offer first, then size, country and exclusions (customers, competitors, government, delivery geography).
4. Separate buyers from partners, vendors and rival agencies by reading company descriptions, not industry labels. Partners go to a separate list.
5. Confirm a real signal with a dated source link. Intent signals qualify; supporting signals only add weight.
6. Assign tiers A, B, C by strength of evidence (tier drives the touch 1 hook).
7. Dedupe against Client Hub (contacts, lists, blacklist) and every other bucket for the client.
8. Export the master account list with sources for the operator's own QA before contacts are enriched. Qualify before enriching.

**Tools:** Blitz MCP (company search, enrichment, jobs, TAM sizing), Apollo, Clay, Client Hub signal accounts, web fetch. Event buckets use free public pages first; respect list terms.

**Outputs:** `profiles/<client>/companies.csv` (domain, company, LinkedIn URL, headcount, industry, geography, qualification reason, signal, evidence URL and date, tier) and `tam-report.md` (sources, filters, counts, rejects).

**Handoff:** `companies.csv` to Stage 5 People TAM. Report to Chief of Staff.

**Gates and rules:** Credit-spending searches need an estimate and the operator's approval. Corporate news is not a signal. Dated evidence only. Zero-credit rule applies where a client file sets it. Event buckets: confirm the attendee list can be pulled and check pass costs; paid passes are the client's call above the cheap threshold.

---

## Stage 5: People TAM (contacts, emails, phones, Client Hub import)

**Purpose:** Find the right people at each qualified account, with verified emails and phones, ready for sequencing and calling.

**Inputs:** `companies.csv` from Stage 4; titles, seniority and geography from the client profile.

**Ordered steps:**
1. Read house rules and client file. Enrich only accounts that already passed qualification.
2. Waterfall: Blitz first (email and phone, MCP only), then Pronto for top-ups (credits), then Apollo (people search is free), then Clay, LeadsForge or Pipecorn for gaps (credits, ask first). Estimate credits before any paid step.
3. Pick up to about 3 contacts per company, budget owner first (2 per account for lead magnets). Exclude titles that cannot buy and anyone in a delivery geography.
4. Never guess an email. Mark emails on a previous employer's domain as not_found. Verify every email before upload and flag catch-alls.
5. Dedupe against Client Hub contacts, the blacklist and people already sequenced for this client.
6. Re-check that each account still meets criteria after enrichment; replace failures.
7. Pull phones as a normal step (calling is always in scope). Say how low phone coverage is in the report. Screen UK numbers against TPS/CTPS before any call.
8. Write the leads CSV in the Smartlead leads schema and prepare the Client Hub import CSV (first_name, last_name, email, linkedin_url, title, company, phone, mobile_phone, country, website, note). The note holds the BDR note in <APPROVER>'s format. Split WithPhones and NoPhone where useful.
9. Pilot first: run the chain on the first 10 to 50 prospects before loading the rest.

**Standing step: post-launch phone CSV (the operator's standing process):** After a campaign is launched, Stage 5 builds a phone CSV through Blitz for the contacts that are in the campaign, then uploads it to the matching Client Hub contact list so BDRs can call. Prepare the file, split WithPhones and NoPhone, and run the Client Hub import only with the operator's OK. Some clients may set exceptions (for example, phones enriched only on request, or imports only after the client reviews the list).)

**Tools:** Blitz MCP (employee finder, find people, work email, phone), Apollo, Clay, Pronto, Client Hub (contacts, lists, blacklist, import), Smartlead leads schema.

**Outputs:** `profiles/<client>/leads.csv` (source and verification status per row) plus the Client Hub CSV; later, the post-launch phone CSV.

**Handoff:** `leads.csv` to Stage 8 for list QA and to Stage 6 for copy. Report to Chief of Staff.

**Gates and rules:** Paid enrichment needs the operator's approval. Importing into Client Hub and adding to the blacklist are writes that need the operator's OK. 100% verified emails before upload.

---

## Stage 6: Copywriting (email, LinkedIn, call openers, BDR notes)

**Purpose:** Write the sequences and personalization that turn the qualified list into replies, in the client's voice and offer.

**Inputs:** Client profile, campaign plan, `leads.csv`, the client's past copy and results, client banned terms and cleared claims.

**Ordered steps:**
1. Read house rules, client file and campaign strategy. Learn from what has and has not worked for that client.
2. Template gate: choose 3 to 4 recommended email templates before writing.
3. Write the email sequence of 3 to 5 touches. Every follow-up is a NEW thread with its own lowercase, internal-looking subject. Each touch has a new angle and a stronger offer and CTA (soft ask, yes or no, one-word reply or specific time, clear final choice). Offer on every touch. No backstory opener, no filler, no emojis on touch 1, no prices, no client names without OK, no competitor-follow mentions, no outcome promises the client has not cleared.
4. Write LinkedIn DMs if in scope: profile view, connection request (A/B test blank vs short note), about 4 short messages, each with a stronger ask. Never say "I saw you follow X".
5. Write call openers and BDR notes in <APPROVER>'s format (header, ACCOUNT SIGNAL, Caution, WHY REACH OUT, WHAT THE SIGNAL MEANS TO THEM, PITCH ANGLE, OPENER). Internal evidence goes in BDR notes only, never in emails.
6. Personalize with real dated facts using the subagent pattern: sample 1 lead, then rounds of 10, until 2 rounds come back with no edits, then scale. No external AI API keys.
7. A/B variants change one thing only (subject, hook or offer), 50/50, at least 100 per version.
8. Write copy in the Smartlead field shape (`{{email_N_subject}}`, `{{email_N_body}}`, then signature) so Stage 7 can map it.
9. Self-check: no-em-dashes, spam-word checker, reading level, client banned terms, ask gets stronger each touch.

**Tools:** copy skills (campaign-strategy, campaign-copywriting, cold-email-templates, linkedin-dm-framework, no-em-dashes, personalization-subagent-pattern, spam-word-checker), Client Hub (reply metrics), client files.

**Outputs:** `profiles/<client>/variants.yaml`, `copy.md` for the operator's review, `linkedin-dms.md` if in scope, and a personalized leads CSV if per-lead variables are used.

**Handoff:** To Stage 8 for copy QA, then (after QA passes and approval) to Stage 7. Report to Chief of Staff.

**Gates and rules:** Copy is a draft until the operator approves it. <APPROVER> is final reviewer; some clients approve their own copy. Using a proof point or claim not marked cleared needs the operator's OK. Existing live campaigns are not rewritten; new rules apply to new or not-started leads.

---

## Stage 7: Outreach (Smartlead DRAFT, Prosp, CloudTalk, Client Hub prep)

**Purpose:** Assemble the approved list and copy into a ready-to-launch DRAFT across channels. Never launches.

**Inputs:** Approved `variants.yaml` and copy, QA-passed `leads.csv`, infra plan and mailbox details, client file notes (rested mailboxes, tickets).

**Ordered steps:**
1. Read house rules and client file; check Smartlead notes before choosing inboxes.
2. Pre-upload checks: blacklist check against Client Hub and every other campaign for the client; leads verified; mailboxes attached and warmed; signatures present; schedule set; send-gating items cleared (DNC, customers, live conversations).
3. Prepare the Smartlead settings: plain text on, open and click tracking off, stop lead on reply, Monday to Friday 09:00 to 18:00 in the prospects' timezone, about 20 minutes between emails, AI ESP matching and out-of-office handling on.
4. Map sequence steps to per-lead custom fields, each with its own subject, spintax only for small greeting variations.
5. Preview the copy for 2 or 3 specific leads to check merge fields (a test email to the operator's inbox is a send, so offer it and wait).
6. Load a pilot cohort first (10 to 50), get the chain approved, then prepare the rest.
7. Prepare other channels: LinkedIn in Prosp (webhooks for reply tracking; session expiries are flagged to Chief of Staff), calling in CloudTalk, and the Client Hub list and BDR notes import file.
8. Write the launch pack with the Smartlead campaign link. Recount leads after upload because Smartlead can drop a few.
9. Create the DRAFT campaign only after the operator's approval, named `<Client> - Bucket <N> - <Mon YYYY> - <signal>`.

**Tools:** Smartlead (API via box secret, never printed), Prosp, CloudTalk, Client Hub, smartlead-api, smartlead-campaign-upload, smartlead-inbox-manager and smartlead-spintax skills.

**Outputs:** `profiles/<client>/launch-pack.md` (campaign name, inbox tags, schedule, sequence with spintax, lead count, exact steps to create the DRAFT) and the DRAFT campaign once approved.

**Handoff:** Launch pack to Stage 8 for pre-launch checks. After the operator launches, tell Stage 9 the campaign ids. Report to Chief of Staff.

**Gates and rules:** Creating a draft, changing inbox warm-up or signatures, adding leads, calls, SMS and any send need the operator's approval. Stage 7 never presses Start. Rollout rule: new copy goes only to new or not-started leads. Adding leads to, pausing, resuming or editing a live campaign is a live change (the operator plus <APPROVER>'s OK).

---

## Stage 8: QA (the gate, three checkpoints plus live audits)

**Purpose:** Independent quality gate. Checks and reports; fixes go back to the stage that owns them.

**Inputs:** `leads.csv` (list QA), `variants.yaml` and `copy.md` (copy QA), launch pack and infra (pre-launch), live campaign metrics (audits).

**Ordered steps:**
1. **List QA (after Stage 5, before copy is merged):** list-quality-scorecard. Check 100% verified emails, no guessed emails, previous-employer domains marked not_found, blacklist and cross-campaign dedupe, exclusions applied, buyer vs partner split, signals dated and sourced.
2. **Copy QA (after Stage 6):** every Stage 6 rule: no dashes, ninth-grade reading level, new thread and lowercase subject per follow-up, offer on every touch, stronger CTA each touch, no filler or backstory opener, no client names or prices, no follow mentions or competitor bashing, emojis only late, client banned terms, spam words. A/B variants change one thing only. Merge fields render.
3. **Pre-launch QA (after Stage 7 draft):** signatures on every mailbox; every contact and company passes qualification; merge fields render in a per-lead preview; DNS checks (SPF, DKIM, DMARC); inbox health and bounce data; pilot pass rate. Placement tests may cost credits, so ask first.
4. Write the QA report with pass or fail and blockers.
5. **Live audits (ongoing):** watch bounce by campaign and by shared domain. House alert line is 2% bounce (second line 3% list problem, 5% either type); spam rate promise is under 1%. Diagnose list vs mailbox cause; <DELIVERABILITY_LEAD> investigates; Smartlead and InboxKit support are the escalation.

**Tools:** list-quality-scorecard, spam-word-checker, email-deliverability-audit, deliverability-incident-response skills; Client Hub metrics; InboxKit; DNS checks; Smartlead inbox health where available.

**Outputs:** `profiles/<client>/qa-report.md` (list grade, copy issues with fixes, deliverability status, pass or fail, blockers).

**Handoff:** List fail goes back to Stage 5. Copy fail goes back to Stage 6. Infra fail goes to Stage 3. Pass goes to Stage 7 and Chief of Staff says it is ready for the operator's approval. Live-audit findings go to Stage 9. Report to Chief of Staff every time.

**Gates and rules:** Nothing moves forward on a fail. QA reports and sends nothing and changes nothing live. Any pause, rest or removal that follows an incident needs <APPROVER>'s OK and the operator's approval.

---

## Standing step: Launch (the operator does it herself)

**Purpose:** The human go decision.

**Ordered steps:**
1. Stage 8 pre-launch pass is in hand and Chief of Staff gives the operator one message: campaign link, what changed, QA result, what she is approving.
2. The operator reviews the DRAFT in Smartlead (and Prosp or CloudTalk assets where relevant). <APPROVER> has signed off copy.
3. The operator presses Start herself in Smartlead. Bots never launch, resume or pause.
4. Stage 7 tells Stage 9 the campaign ids; the client Helper logs the launch and campaign plan moves (the operator or <APPROVER> moves the Client Hub stage: planning, copy_assets, ready, live, winding_down, finished).
5. Post-launch phone CSV via Blitz is prepared and, with the operator's OK, uploaded to the Client Hub contact list (see Stage 5).

---

## Stage 9: Skills (reply triage, weekly rhythm, reporting, learning)

**Purpose:** Run the live campaign day to day, score results, and turn what worked into reusable skills.

**Inputs:** Live campaign ids from Stage 7; Client Hub (email threads, metrics, meetings, activities); Smartlead replies; Fireflies call outcomes; client Helper context.

**Ordered steps:**
1. **Reply triage (daily or on request):** separate human replies from out-of-office, bounces and unsubscribes. Unsubscribes are removed and blacklisted, never replied to. Classify buyer vs partner. Check that "Interested" really is interested. Draft replies and BDR call hand-offs. Hot list goes to the operator first, same-day ones on top.
2. **Hand interested leads to the phone:** the client's BDR calls (most meetings are booked by phone, even after an email yes). The operator sends replies; BDRs call.
3. **Weekly rhythm:** Monday numbers before the weekly team meeting; refresh before each client call (read the last client call, check meetings and outcomes, update A/B results); log meeting outcomes in Client Hub; flag changes to rules, offers or tools so client files and house rules get updated.
4. **Reporting to <APPROVER>:** one page, actions, blockers with owner and days open, every number sourced (Client Hub metrics, email only unless stated), unverified items marked "to confirm".
5. **Results write-up:** positive reply rate (north-star metric), reply breakdown, what to change, saved per client and date.
6. **Learning loop:** when a pattern repeats across 2 or more runs, write it up as a skill draft or proposed house-rule change and send it to Chief of Staff. After a full run, write "everything we did" as a reusable skill draft.
7. **Feed back:** new campaign ideas to Stage 2, copy changes to Stage 6, deliverability concerns to Stage 8. This is the loop.

**Tools:** Client Hub, Smartlead, Fireflies, cold-email-weekly-rhythm, positive-reply-scoring and auto-research skills (reference only until its extra tools exist; its live step stays DRAFT).

**Outputs:** `profiles/<client>/results-<date>.md`; skill drafts in `<WORKSPACE>/skills-drafts/` (approved ones in `skills-custom/`).

**Handoff:** Learnings back to Stages 2, 6 and 8. Reminders go to Chief of Staff, who reminds the operator. Stage 9 never messages the operator or prospects directly.

**Gates and rules:** Draft replies only; every reply is sent by the operator. Never reply to an unsubscribe. No price numbers in replies (price questions go to the founders or the client call). The operator approves before a skill draft becomes a team skill. Bot-proposed house-rule changes need the operator's approval.

---

## Standing step: Client offboarding (agreed with <APPROVER>, 13 Oct 2026)

**Purpose:** Cleanly stop everything for a client that is leaving: deactivate tenants, close mailboxes and inboxes, cancel Prosp accounts, and give client data only when they ask.

**Timeline and ordered steps:**
1. **Notice day (D-30 or the contract notice period):** confirm the owner, build the inventory of everything running for the client, and ask the client whether they want a data export or the domains and LinkedIn transferred. Freeze new builds (no new lists, credits or campaigns).
2. **D-14 to D-1, final sends:** live sequences run to the end or are paused at D-1. Leave drafts unlaunched. Hand positive replies and booked meetings to the client.
3. **D-day, deactivation, recurring paid items first:**
   - A. Recurring paid items: mailboxes (stop warm-up, remove from Smartlead, cancel licences), warm-up tools, sending domains and DNS (turn off auto-renew; transfer only on request), Prosp seat and LinkedIn sender (and Sales Navigator if we pay), CloudTalk numbers and campaigns, Smartlead client sub-account, data tool subscriptions bought for the client (stop scheduled tables and monitors).
   - B. One-off cleanup: pause or archive Smartlead campaigns (never launch drafts), Client Hub (stop syncs, export if asked, clear signal accounts, keep the blacklist, set the tenant inactive, never delete), archive Prosp lists and campaigns, remove the client from bot nudges, reports and Helper scope and archive its house-rules client file, remove Drive sharing, send an approved goodbye in shared channels, cancel recurring calls, revoke the client's Fireflies access (keep recordings internally), move the client's box folder to `_archive/` after sign-off.
4. **Data export (only on written request):** CSVs of leads and contacts per campaign, campaign stats, positive replies and meetings, shared through Drive with the client contact only. Never share other clients' data, the blacklist or internal notes.
5. **D+7:** check next invoices for leftover charges, then sign-off.

**Owners:** <APPROVER> (mailboxes, domains, Prosp, CloudTalk, Slack and WhatsApp, invoices), the operator (Smartlead, Client Hub, Prosp lists, data tools, Drive, Fireflies, box files, sign-off), Stage 3 (warm-up and mailboxes), Chief of Staff bot (bots and routines).

**Sign-off checklist:** every recurring item cancelled with confirmation; no sends in the 7 days after D-day; next invoices checked; export delivered or confirmed not wanted; Client Hub tenant inactive. Signed by the operator and <APPROVER>.

**Gates:** Goodbye messages go only after approval. Nothing is deleted from Client Hub.

---

## Handy variants (scenarios from the playbook)

| Scenario | Order | The operator approves |
|---|---|---|
| New client | Helper/CW-H notes -> S2 + S3 in parallel -> S4 -> S5 -> S8 list -> S6 -> S8 copy -> S7 draft -> S8 pre-launch -> the operator launches -> S9 | Mailboxes, credits, copy, Client Hub import, launch |
| New bucket, existing client | Helper -> S2 (bucket plan) -> S4 -> S5 -> S8 -> S6 -> S8 -> S7 draft -> S8 -> the operator -> S9 (S3 only if no free warm mailboxes) | Credits, copy, import, launch |
| List refresh | Helper -> S4 and/or S5 -> S8 list -> S7 prepares upload only | Credits; adding to a live campaign |
| Copy rewrite | Helper -> S6 -> S8 copy -> S7 prepares new sequence or cohort | Copy approval; any live edit (<APPROVER> too) |
| Deliverability incident | S8 diagnose -> S3 fixes -> S7 prepares pause or rest plan -> CW-H logs | Any pause or rest; <APPROVER>'s OK; <DELIVERABILITY_LEAD> investigates |
| Reply triage | S9 -> Helper for context -> BDR hand-off via the operator | Every reply sent; blacklist adds |
| Weekly reporting | S9 numbers -> Helpers confirm -> Chief of Staff assembles | Before anything goes to <APPROVER> or a client |
| Lead magnet (25 accounts) | CW-H context -> S4 discover, verify, score -> S5 2 contacts per account -> S8 quality gates -> the operator gets files | Credits; upload and send (a person on the team, never a bot) |

## Suggested Miro layout
- Left to right swimlane per stage (S2 to S9), with Launch as a diamond between S8 and S9 and Offboarding as a closing lane.
- Under each stage: Purpose, Inputs, Steps, Tools, Outputs, Handoff, Gates (colour the gate boxes red).
- A feedback arrow from S9 back to S2, S6 and S8; fail arrows from S8 back to S3, S5 and S6.
