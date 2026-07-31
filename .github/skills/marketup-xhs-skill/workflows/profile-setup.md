# Enterprise Profile Setup Workflow

Use this workflow to turn unfamiliar company materials into a validated enterprise Profile. Profile Setup is an onboarding and evidence-validation task, not a content-production task.

## Entry Conditions

Run this workflow when:

- `profile_status` is `template` or `draft`;
- the requested task is absent from `supported_tasks`;
- the user explicitly asks to initialize, adapt, create, or update a company Profile.

For an already active Profile, ordinary task materials never enter this workflow merely because they are newer, more detailed, or inconsistent with the Profile. Read `rules/task-material-isolation.md` instead. Only an explicit Profile update request allows task materials to be promoted into long-term Profile evidence.

Tell the user briefly that the Profile must be prepared before publishable content can be generated. Do not ask the user to edit Markdown files or understand Profile terminology.

## Stage 1: Establish Scope

Identify:

- the intended company or brand;
- the supplied folder, attachments, pasted text, or other material scope;
- the task the user ultimately wants to perform;
- any explicit publication, confidentiality, audience, or format limits.

If the material scope is ambiguous, ask for the folder or attachments before continuing. Do not scan unrelated workspace folders merely because they are accessible.

## Stage 2: Inventory Materials

List the supplied materials before extracting claims. Classify each item as:

1. `company_fact`: official brand, product, service, UI, or approved business material;
2. `business_background`: industry reports, definitions, research, or whitepapers;
3. `historical_marketing`: previous posts, campaign copy, sales copy, or old drafts;
4. `reference_sample`: competitor content, Xiaohongshu notes, or visual references;
5. `sensitive_or_unknown`: customer data, contracts, pricing, internal contacts, private dashboards, or unclear material.

Record date or version, authority, publicity, and intended use in the active Profile's evidence registry. Do not assume the newest filename is the newest approved source.

## Stage 3: Extract Evidence

Read `schemas/evidence-fields.md`. For every candidate brand fact, product capability, audience claim, visual rule, or compliance boundary:

- record the claim and its exact source;
- assign `confirmed`, `user_confirmed`, `inferred`, `conflicting`, `missing`, or `restricted`;
- separate observed facts from interpretation;
- keep unsupported helpful guesses as `inferred`, never as approved facts;
- mark competitor and reference materials as `reference_only`.

When sources conflict, prefer the more current and authoritative source only when the difference can be resolved from the materials. Otherwise mark the claim `conflicting` and ask the user.

## Stage 4: Build the Draft Profile

Populate the Profile files only with supported information:

### Brand

Record the official name, positioning, voice, preferred terminology, forbidden expressions, and common brand-confusion risks.

### Product

Separate:

- confirmed capabilities;
- supported business scenarios;
- public and provable value statements;
- capabilities that require softer wording;
- unsupported or forbidden claims.

Every approved capability must have at least one `confirmed` or `user_confirmed` evidence record. Performance, ranking, customer-count, revenue, conversion, and benchmark claims require a `confirmed`, public, formal source; user confirmation alone is insufficient.

### Audience

Distinguish content readers, product users, buyers, decision makers, and influencers. Do not assume the product user is automatically the Xiaohongshu target reader.

### Visual

Record confirmed visual style, palette, color proportion, brand-color rendering, area limits, typography tendency, layouts, assets, and forbidden elements. Use the workflow's brand-neutral text-density default unless the company has a confirmed override. If official visual material is missing, label any neutral fallback as provisional. Do not invent an official palette, logo, product interface, or brand graphic system.

### Compliance

Record CTA rules, data and results-claim rules, customer-case permissions, sensitive information, regulated-industry limits, screenshot permissions, pricing rules, and contact-information rules.

When company-specific compliance information is missing, use the conservative baseline: no customer names, real customer data, effect numbers, rankings, QR codes, direct contact details, or absolute promises.

Set `profile_status` to `draft` after the first extraction pass.

## Stage 5: Validate Task Readiness

Read `schemas/profile-fields.md`. Evaluate the requested task against its minimum conditions.

Do not count blank fields, placeholders, `inferred`, `conflicting`, `missing`, or `restricted` claims as satisfying a readiness condition.

Set:

- `active_limited` when only some tasks are ready;
- `active` when the core Profile is validated and all listed tasks are ready.

List only validated tasks under `supported_tasks`. Also record blocked tasks and their exact missing conditions in the setup report.

An empty keyword bank or sample library does not block basic content generation when the brand, product, audience, and compliance gates pass. In that case, state that topic and sample validation are unavailable, and do not fabricate keyword or reference-pattern findings.

## Stage 6: Ask Only Blocking Questions

Extract everything possible before asking the user questions. Ask at most three high-priority questions per round, using plain business language rather than Profile field names.

Question priority:

1. company or product identity conflicts;
2. unsupported or conflicting product capabilities;
3. primary target reader and buying role;
4. public, internal, and confidential boundaries;
5. permission to use provisional visual defaults.

Ask concrete questions tied to evidence. For example, ask whether a capability found only in an old sales deck is still offered; do not ask the user to “complete the Product Profile.”

If the user cannot answer, keep the item unresolved and restrict the affected task. Do not convert uncertainty into a conservative-sounding product fact.

## Stage 7: Activate and Report

Update `profile_status`, `supported_tasks`, and `last_verified_at` only after validation. Then return a Profile Setup report containing:

1. identified company and material scope;
2. confirmed brand, product, audience, visual, and compliance facts;
3. inferred, conflicting, missing, and restricted items;
4. conservative defaults in use;
5. supported tasks;
6. blocked tasks and reasons;
7. remaining questions;
8. files created or updated.

Do not include candidate Xiaohongshu titles, body copy, carousel pages, or image prompts in the Setup report. After activation, resume the user's original request only if they asked for production and the requested task is now supported.

## Profile Update Boundary

Do not modify or downgrade an active Profile because of materials supplied for an ordinary content task. Task conflicts expire with that task.

When the user explicitly requests a Profile update, treat it as a separate workflow. Record the proposed changes, evidence, conflicts, and affected tasks; validate them before changing long-term Profile files or status. Do not silently promote current-task facts into the Profile.
