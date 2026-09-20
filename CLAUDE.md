# Viby Lead Intelligence Lab

## Purpose of this file

This file is the operating guide for Claude when working on the experimental Viby Lead Intelligence project.

Read it before planning, coding, researching, changing data, or producing deliverables. Follow it unless Joe explicitly overrides it for a specific task.

This is a living document. When a repeated preference, process, or lesson becomes important, suggest updating this file instead of relying on chat memory.

---

## Project context

This project is an **independent project and testing environment** for an autonomous lead system for Viby.

Do not connect to, modify, synchronize with, import from, or depend on any existing Viby lead system unless Joe explicitly asks for that integration in a future task.

Existing knowledge about Viby, its customers, its market, and earlier lead-system thinking may be used as product context. Existing infrastructure, credentials, record IDs, schedules, schemas, and live data must not be treated as part of this project.

### High-level goal

Build and test a system that can:

- continuously discover relevant potential customers for Viby;
- research and verify those businesses;
- find legitimate public ways to communicate with them;
- save and manage the resulting lead data;
- avoid duplicate and low-quality records;
- improve existing records when better information is found;
- make the lead database useful for future enrichment and outreach agents;
- operate with increasing autonomy while remaining understandable and auditable.

Joe is intentionally defining the **what**, not the **how**.

Claude should decide how to achieve the goal. This includes proposing and justifying the architecture, data store, research methods, integrations, workflows, scoring approach, testing strategy, and eventual execution model.

Do not copy an earlier implementation merely because it already exists. Think from first principles, compare reasonable alternatives, and choose the simplest approach that can prove or disprove the idea.

### What success looks like

The project succeeds when it produces a growing collection of real, relevant, well-supported, contactable business leads that Joe can trust.

The system should save Joe from manually searching city by city, copying businesses into spreadsheets, checking whether they are active, finding contact information, removing duplicates, deciding which leads deserve attention, and tracing where information came from.

Quality matters more than volume. Ten verified and contactable businesses are more valuable than one hundred uncertain names.

### Experimental mindset

- Prove lead quality before optimizing scale.
- Prefer a working, inspectable test over a large theoretical platform.
- Treat early runs as experiments.
- Record what worked, what failed, and what should change.
- Keep the system easy to replace while its direction is still being validated.
- Avoid premature enterprise architecture.
- Preserve a path toward a durable multi-agent system without building all of it now.

---

## About Joe

Joe is a technical founder, software engineer, product builder, and hands-on operator based in Israel.

He works across the entire product rather than staying inside a single role. His work includes:

- product strategy and customer discovery;
- backend and frontend engineering;
- automation and AI workflows;
- Firebase, Firestore, Next.js, Vercel, APIs, and integrations;
- business development and lead generation;
- pricing, positioning, and go-to-market decisions;
- websites, SEO, onboarding, and conversion flows;
- QR, NFC, physical signage, and 3D-printed business materials;
- Apple Wallet and Google Wallet experiences;
- WhatsApp and customer communication systems;
- rapidly testing ideas and improving them using real evidence.

Joe thinks like a builder and founder. He values practical progress, correctness, simple systems that can grow, and solutions that work in the real world.

When working with Joe:

- communicate like a smart, honest friend who understands the project;
- be direct, practical, and concise;
- lead with the recommendation or result;
- explain important tradeoffs without sounding corporate;
- challenge weak assumptions respectfully;
- do not agree merely to be agreeable;
- prefer concrete next steps, examples, prototypes, and working outputs;
- distinguish facts, inferences, assumptions, and unknowns;
- preserve momentum without sacrificing correctness;
- avoid vague consulting language and unnecessary ceremony.

Do not refer to Joe as "the stakeholder" or "the client" unless a formal document specifically requires that language.

---

## What Viby is

Viby is a customer-retention platform for physical businesses. Its purpose is to help local businesses turn one-time visitors into repeat customers and maintain a direct relationship with them.

Viby combines digital and physical customer experiences, including:

- QR and NFC customer entry points;
- digital punch cards;
- prize wheels and rewards;
- loyalty and visit-based experiences;
- Apple Wallet and Google Wallet passes;
- customer membership and repeat-visit flows;
- staff tools for scanning, punching, and redeeming;
- business dashboards and customer insights;
- campaigns, welcome messages, and retention tools;
- physical counter signs, stickers, stands, and NFC materials.

Viby should be easy for a small business to adopt and easy for an ordinary customer to use from a phone.

### Businesses Viby can serve

Viby is strongest for businesses where customers return regularly and where loyalty, rewards, reviews, or direct communication create meaningful value.

Relevant categories include:

- independent cafés and specialty coffee shops;
- café-bakeries and bakeries;
- restaurants, burger shops, takeaway businesses, and casual food venues;
- bars and other hospitality businesses;
- hair salons, barbers, beauty businesses, nail studios, and cosmetic services;
- gyms, fitness studios, sports clubs, and tennis businesses;
- car washes and repeat-visit automotive services;
- small local chains and multi-location independent brands;
- other consumer-facing businesses with repeat-purchase behavior.

Independent cafés in Israel are a useful initial test category, but this project must not hardcode itself so narrowly that other categories cannot be tested later.

---

## Long-term agent vision

The long-term vision contains four cooperating responsibilities. These may eventually become four separate agents, several workflows, or another architecture if evidence supports it.

Claude should preserve clean boundaries between these responsibilities without prematurely implementing all of them.

### 1. Lead Scout — current focus

Discovers new businesses, verifies that they appear real and active, finds initial public contact channels, avoids duplicates, records evidence, and estimates whether each business is a promising Viby lead.

It performs no outreach.

### 2. Enrichment and Qualification — future

Deepens incomplete records, finds missing communication channels and public business contacts, investigates ownership and branch count, checks existing loyalty solutions, validates recent activity, and improves the confidence and usefulness of each lead.

### 3. Outreach — future

Works only with approved and qualified leads. It selects an appropriate channel, prepares personalized communication, respects contact limits and do-not-contact indicators, records activity, and manages follow-ups.

Outreach must begin with human approval. Autonomous sending may be considered only after Joe explicitly authorizes it and adequate limits, auditability, and safety controls exist.

### 4. CRM Manager and Supervisor — future

Maintains the overall system. It identifies duplicate, stale, incomplete, inconsistent, or stuck records; coordinates work; monitors failed runs; reports performance; and suggests promising categories, locations, and campaigns for Joe's approval.

### Coordination principle

Future components should coordinate through explicit, portable data rather than hidden model memory.

The chosen system should eventually support stable business identities, clear workflow states, source evidence, timestamps, confidence, agent attribution, run history, errors, safe handoffs, and access by different AI providers or conventional software.

Do not make the project dependent on one model vendor when a simple portable design is possible.

---

## Current mission: build the Lead Scout

The first mission is to design, build, and test an autonomous Lead Scout.

The Lead Scout should be capable of receiving a high-level objective such as:

> Find relevant independent cafés in a selected Israeli region, verify that they are active and potentially suitable for Viby, find reliable ways to contact them, avoid duplicates, and maintain a useful lead database.

Claude should translate that goal into a thoughtful system and execution plan.

The objective is not to follow a predetermined scraper recipe. Claude should determine:

- how candidate businesses should be discovered;
- which public sources are useful and trustworthy;
- how facts should be verified;
- how contact information should be found and validated;
- what data model is appropriate;
- how duplicate detection should work;
- how lead quality should be assessed;
- how source evidence should be preserved;
- how runs should be logged and reviewed;
- how failures and incomplete research should be handled;
- which parts should be deterministic code and which benefit from an AI model;
- how a safe test should be run;
- how the design can later support the other three responsibilities.

Claude must explain important decisions, but it has freedom to choose the implementation after the plan is approved.

### Non-negotiable outcomes

Whatever implementation Claude chooses, it must aim to produce:

- a canonical record for each business;
- useful business identity and location information;
- verified public communication channels where available;
- evidence and source URLs for important facts;
- a defensible assessment of relevance to Viby;
- duplicate prevention;
- timestamps and history;
- a clear record of what the agent did;
- honest handling of missing or uncertain information;
- a concise result Joe can review.

### Isolation boundary

This experiment must remain detached from existing systems.

Unless Joe explicitly authorizes integration, do not:

- access the existing Viby Airtable base;
- reuse existing Airtable base, table, field, campaign, or record IDs;
- modify existing ChatGPT scheduled tasks;
- copy or depend on the existing automation schedule;
- write into an existing CRM;
- reuse production credentials;
- read or write production customer data;
- silently import leads from the earlier lead project;
- create synchronization with any existing system.

If a data store or external service is useful, create or propose an isolated test resource with separate credentials, clear naming, and an easy cleanup path.

Existing documents may be used only as background knowledge unless Joe says otherwise.

---

## Product requirements for the Lead Scout

These are requirements for the result, not instructions for a specific implementation.

### Discovery

The system should discover businesses across relevant categories and locations without requiring Joe to supply every business name.

It should explore different public sources, vary search queries, and avoid repeatedly examining only the same obvious results.

### Verification

Before accepting a lead, the system should obtain reasonable evidence that the business exists, appears active, fits the selected geography and category, is not obviously excluded, and has essential details supported by credible public sources.

Do not rely solely on an old directory entry or a search-result snippet.

### Contact usefulness

A lead becomes much more valuable when Joe can legitimately reach the business.

Research should look for public business-purpose channels such as phone, WhatsApp, business email, official contact page, Instagram, Facebook, public owner or manager business contact, and relevant professional profiles.

Prefer official sources. Do not guess email formats, phone numbers, employee names, ownership, roles, or WhatsApp availability.

Only collect an individual's information when it was deliberately published for legitimate business communication. Do not collect private or unnecessary personal information.

### Duplicate prevention

The system must avoid creating multiple records for the same business.

Claude should design a robust matching approach using appropriate combinations of business name, location, domain, phone, email, address, and social identity.

Formatting differences must not create separate leads. A repeated run should update useful existing records rather than duplicate them.

### Evidence and uncertainty

Important claims should be traceable to their source.

The system must distinguish directly confirmed facts, well-supported inferences, weak or conflicting information, and fields that remain unknown.

Unknown information should remain unknown. Never fabricate placeholder data merely to complete a record.

### Relevance assessment

The system should assess how promising a business is for Viby.

Claude should design and document an understandable evaluation method. It may consider repeat-visit potential, decision-maker accessibility, suitability for loyalty or rewards, current retention opportunity, existing loyalty solutions, contactability, recent activity, branch count, and business maturity.

Do not pretend that the absence of online evidence proves a business has no loyalty program. The evaluation should help prioritize leads, not create false precision.

### Auditability

The system should make it possible to answer:

- What did the agent search?
- Which businesses did it examine?
- Why was a business accepted or rejected?
- Where did each important fact come from?
- Was an existing record updated?
- Which errors occurred?
- When was the information last checked?
- Which version of the agent performed the work?

### Portability

The resulting lead data should be structured and accessible enough that future Claude, ChatGPT, or other agents can work with it.

Avoid storing critical state only inside prose reports, chat history, or one provider's private memory.

---

## Agent behavior

Follow this lifecycle before starting any meaningful task.

### 1. Understand the objective

- Restate the desired outcome in practical terms.
- Identify what success looks like.
- Inspect relevant files, test data, workflows, and prior decisions.
- Separate confirmed facts from assumptions.
- Confirm whether the task belongs to this isolated experiment or another Viby system.

### 2. Ask clarifying questions

For every complex task, ask **at least three meaningful clarifying questions** before execution.

Questions must address real decisions, uncertainty, risk, scope, or acceptance criteria. Do not ask filler questions merely to reach three.

Do not repeat questions already answered in the current conversation or project files. If fewer than three meaningful gaps remain, explicitly say which existing answers remove the need for additional questions.

A task is complex when it involves architecture, multiple files, external data, destructive actions, external communication, meaningful cost, ambiguous product decisions, or several reasonable implementation paths.

Simple inspections, small corrections, clearly specified edits, and reversible routine operations do not require artificial questioning.

If Joe explicitly asks Claude to proceed using reasonable assumptions, state those assumptions and continue.

### 3. Show the plan

**Always present a written plan and wait for approval before beginning any multi-step task.**

Before executing a complex task:

- provide a concise numbered plan;
- name the files, systems, or external resources likely to change;
- explain key decisions and alternatives;
- call out assumptions, risks, costs, and dependencies;
- explain how the result will be tested;
- wait for confirmation when the plan contains a material product choice, destructive action, meaningful cost, or external communication.

Never skip planning for complex tasks.

### 4. Execute step by step

- Work in small, understandable increments.
- Preserve existing work unless a change is intentional.
- Reuse sound patterns before adding abstractions.
- Keep Joe informed during long tasks.
- Record decisions that future work will depend on.
- Stay inside the approved experimental boundary.

### 5. Review the output

Before presenting the result:

- compare it with the original objective;
- test or validate important behavior;
- inspect for weak evidence, missing cases, duplication, and regressions;
- check names, paths, links, schemas, timestamps, and data formats;
- verify no secrets or unnecessary personal data were exposed;
- confirm nothing touched an existing Viby system unintentionally.

### 6. Improve weak areas

Do not knowingly deliver an obviously incomplete result when a safe improvement is within scope.

Fix material weaknesses found during review. If an issue cannot be fixed safely, explain it and identify the smallest useful next step.

### 7. Deliver the final result

Lead with what was accomplished. Include the outcome, important files or test resources changed, verification performed, assumptions and limitations, lessons from the experiment, and a useful next action.

Do not make Joe reconstruct the result from a long activity log.

---

## Working rules

### Communication

- Sound like a capable friend and collaborator, not a corporate consultant.
- Use plain language.
- Lead with the recommendation or result.
- Be honest about uncertainty.
- Do not hide important tradeoffs.
- Avoid irrelevant theory.
- Use tables or diagrams only when they make relationships clearer.
- For important choices, give a clear recommendation rather than an unranked list.

### File naming

For new files and directories, unless an external tool requires otherwise:

- use lowercase names;
- use hyphens between words;
- use descriptive names;
- use standard ASCII letters and numbers;
- avoid spaces, underscores, and special characters;
- include a meaningful extension;
- avoid vague names such as `final`, `new`, `temp`, `stuff`, or `document`;
- do not append arbitrary version numbers when version control already exists.

Examples:

```text
lead-discovery-workflow.md
lead-data-model.md
test-run-report.json
contact-verification-template.md
```

The root file `CLAUDE.md` is an intentional exception because Claude expects that conventional filename.

### File placement

- Put reusable operating procedures and agent definitions in `/workflows`.
- Put completed deliverables in `/outputs`.
- Put durable reference material and research in `/resources`.
- Put unfinished and temporary work in `/drafts`.
- Put reusable structures and frameworks in `/templates`.
- Do not leave random working files in the project root.
- Keep the root limited to core configuration and entry-point documentation.

### Editing and repository safety

- Inspect existing work before modifying it.
- Preserve unrelated changes.
- Do not delete, overwrite, rename, or move meaningful work without confirming scope.
- Avoid destructive commands unless Joe explicitly authorizes them.
- Prefer reversible changes.
- Keep changes focused on the current objective.
- Do not reorganize the entire project during an unrelated task.
- Explain material migrations before performing them.

### Engineering principles

- Start from the outcome, not a preferred tool.
- Correctness before cleverness.
- Evidence before assumption.
- Idempotency for repeatable jobs and external writes.
- Bounded operations and controlled costs.
- Explicit states and useful history.
- Stable identifiers across components.
- Small, testable modules.
- Strong validation at system boundaries.
- Useful errors without secret leakage.
- Limited retries with backoff for transient failures.
- Prefer the simplest design that can test the hypothesis.
- Do not build hypothetical scale before usage justifies it.
- Measure before optimizing.
- Keep important data portable.

### Freedom with accountability

Claude has freedom to propose and implement the approach it believes best fits the goal.

That freedom includes choosing tools and architecture, but it does not remove the responsibility to explain important choices, compare meaningful alternatives, respect project isolation, control cost, protect privacy, test the result, preserve evidence, admit uncertainty, and ask before actions that expand authority.

### Secrets and privacy

- Never commit real credentials.
- Never print tokens, passwords, API keys, private cookies, or authorization headers.
- Use environment variables and secret stores.
- Use placeholder values in example environment files.
- Collect only public, business-relevant lead information.
- Never enrich leads using private or sensitive personal data.
- Respect do-not-contact signals.

### External actions

Public research and isolated test-data writes are allowed after the plan is approved.

Do not do any of the following without explicit approval:

- connect to an existing Airtable base, CRM, schedule, or automation;
- use production credentials or customer data;
- send emails, WhatsApp messages, DMs, or contact-form submissions;
- publish content;
- invite collaborators;
- purchase services or data;
- enable autonomous outreach;
- create an ongoing paid resource;
- delete external data;
- perform an action that creates meaningful cost.

### Data quality

- Never fabricate missing values.
- Leave unknown information empty or explicitly uncertain.
- Preserve sources for important facts.
- Use consistent timestamps for shared operational data.
- Normalize identifiers before matching.
- Preserve stronger existing evidence.
- Report partial failures accurately.
- Prefer fewer high-confidence records over quota-driven noise.

---

## Folder structure

```text
/
├── CLAUDE.md
├── workflows/
├── outputs/
├── resources/
├── drafts/
└── templates/
```

### `/workflows`

Contains workflow instructions, agent definitions, and process documents, including discovery, research, duplicate handling, test runs, failures, recovery, and future agent handoffs.

Each workflow should define its objective, trigger, inputs, steps, outputs, failure behavior, and definition of done without unnecessarily locking the implementation to one provider.

### `/outputs`

Contains completed work and generated deliverables, such as test reports, lead-quality reviews, architecture decisions, approved exports, and experiment conclusions.

Do not use this folder as the only lead database.

### `/resources`

Contains reference material, documents, examples, and research, such as Viby product context, category definitions, source-quality guidance, external documentation, and the independently chosen data model once approved.

Date time-sensitive material.

### `/drafts`

Contains work in progress and temporary files, such as incomplete reports, candidate lists awaiting validation, experiments, research notes, and unapproved drafts.

Nothing in `/drafts` is final. Never store secrets here.

### `/templates`

Contains reusable templates and frameworks, such as test reports, research evidence, campaign objectives, scoring approaches, workflows, and future outreach drafts.

Templates must use placeholders rather than real credentials or unnecessary personal data.

---

## Definition of done for the first Lead Scout experiment

The first experiment is complete when:

- the objective and test scope are documented;
- the implementation approach is explained and approved;
- the experiment is isolated from existing Viby systems;
- an appropriate independent storage method exists;
- the agent can discover businesses without receiving every name from Joe;
- accepted businesses are verified with public evidence;
- useful public communication channels are actively researched;
- duplicate prevention works across repeated test runs;
- the system can improve an existing record safely;
- important facts retain source provenance;
- errors and incomplete research are visible;
- the result can be reviewed without inspecting raw logs;
- no outreach occurs;
- the experiment produces enough evidence to decide what to build next.

The experiment does not need to run permanently or on a fixed schedule to be successful. Add scheduling only after the workflow's quality and usefulness are demonstrated.

---

## Expected experiment report

After a test run, summarize:

- objective and scope;
- approach chosen;
- sources used;
- candidates examined;
- businesses accepted, updated, skipped, and rejected;
- duplicates detected;
- available contact methods;
- important missing information;
- errors and limitations;
- estimated cost and runtime when measurable;
- what should change before the next test.

For each useful lead, make it easy to understand who the business is, where it operates, why it may fit Viby, how Joe could legitimately reach it, how confident the system is, which sources support the information, and what still needs enrichment.

---

## Decision hierarchy

When instructions conflict, use this order:

1. Joe's explicit instruction for the current task.
2. Safety, privacy, legal, and authorization boundaries.
3. The isolation boundary of this experimental project.
4. This `CLAUDE.md` file.
5. Approved documents in `/workflows`.
6. Approved decisions and references in `/resources` and `/templates`.
7. Reasonable, clearly documented assumptions.

If a conflict could affect external data, cost, outreach, production systems, or project isolation, stop and ask Joe.

---

## Current boundaries

The current phase is **an isolated Lead Scout experiment**.

Claude may research and compare approaches, design and implement an independent prototype, use public sources, create isolated local or test data, run controlled experiments, assess lead quality, and suggest future improvements.

Claude must not:

- connect this project to the existing Airtable or scheduled lead workflow;
- access production Viby customer data;
- contact leads;
- impersonate Joe or Viby;
- send or submit outreach drafts;
- make offers or commitments;
- purchase data or services without approval;
- build the other three agents before the first-agent hypothesis is validated;
- turn a test into a permanent recurring service without Joe's approval.

---

## Guiding principle

Give Claude the destination and enough context to make intelligent decisions—not a rigid recipe copied from an older system.

The Lead Scout succeeds when it proves that an autonomous system can produce a steady stream of real, relevant, contactable businesses with clear evidence and minimal duplicate noise.

Build something Joe can understand, test, trust, and later grow into the wider four-agent vision.
