---
name: marketup-xhs-skill
description: Create or explain Xiaohongshu/RedNote graphic-note and carousel workflows for any company by loading a replaceable enterprise profile, filtering company materials, reconstructing original brand content, and writing or generating independent 3:4 image pages. Use for any request that explicitly mentions Xiaohongshu, RedNote, 小红书, or asks to load or use this Xiaohongshu skill. When the selected enterprise information is substantially empty, first show the stored material-upload and sample-collection onboarding notice before routing the request.
---

# Xiaohongshu Brand Content

## Version

- `skill_version: 2026.07.20`
- `release_date: 2026-07-20`

Turn manually collected Xiaohongshu reference notes and company source materials into original brand content. Keep the workflow brand-neutral; load all company-specific facts from one active profile.

Do not crawl Xiaohongshu, automate platform access, copy competitor content, or invent product claims.

## Select the active profile

1. Use the profile named by the user.
2. Otherwise use `profiles/default/profile.md` as the default profile.
3. Read the active profile manifest first, including `profile_status` and `supported_tasks`, then every file it marks as required.
4. Do not fall back to facts from another company when the selected profile is empty or incomplete.
5. If the manifest is missing `profile_status`, treat the profile as `draft` until it is validated.
6. If a required profile field is missing, follow the Profile Setup Gate below. Do not silently replace missing brand or product facts with another profile's defaults.

Treat the active profile as the only source for:

- brand positioning, voice, terminology, and forbidden expressions;
- product facts, approved capabilities, and evidence boundaries;
- audience and buying context;
- palette, typography, layout preferences, and brand assets;
- enterprise-specific compliance rules;
- keyword bank, search-term mappings, collection adapter, and sample library.

To add another company, copy `profiles/_template/` to `profiles/<company-id>/` and replace only that package.

## Empty enterprise onboarding gate

Immediately after reading the selected Profile manifest, read `workflows/empty-profile-onboarding.md` when the enterprise information is substantially empty. Run this gate before task routing, topic selection, sample analysis, content generation, or image planning.

- Show the onboarding notice once near the beginning of the current conversation, even when the user asks only a short Xiaohongshu question.
- Use plain-language “企业素材库” and explain it in parentheses. Do not require the user to understand Profile terminology or edit Markdown.
- Mention the built-in reference-note collection table and how supplied screenshots, OCR, body text, or an existing collection table can be handled.
- For generic Skill explanations or source-faithful note deconstruction, show the notice and then continue with the safe task.
- For company-branded content, image plans, or image generation, stop production and run the Profile Setup Gate until the requested task is supported.

## Profile Setup Gate

Read `workflows/profile-setup.md`, `schemas/profile-fields.md`, and `schemas/evidence-fields.md` when:

- the selected profile has `profile_status: template` or `profile_status: draft`;
- the requested production capability is not listed under `supported_tasks`;
- the user explicitly asks to create, adapt, initialize, or update a company profile.

While the gate is active:

- do not generate publishable brand content, image prompts, or images;
- inventory and classify the supplied materials before extracting profile facts;
- record each material claim as `confirmed`, `user_confirmed`, `inferred`, `conflicting`, `missing`, or `restricted`;
- never place `inferred`, `conflicting`, `missing`, or `restricted` claims in approved product capabilities or public claims;
- extract useful facts before asking questions, then ask only for unresolved inputs that block the requested task;
- activate only the tasks supported by the completed and validated profile.

Profile Setup returns a setup report and profile draft, not Xiaohongshu content. Resume the requested production workflow only after the profile reaches `active_limited` or `active` and the requested task appears in `supported_tasks`.

Image-plan approval and page quality review inherit the `image_generation` capability; they are workflow states and do not need separate `supported_tasks` entries.

## Profile Persistence Boundary

During ordinary content, prompt, image, or compliance tasks, treat the active Profile and its evidence registry as read-only.

- Temporary PPTs, whitepapers, screenshots, campaign briefs, drafts, and reference notes belong only to the current task.
- Temporary task materials must not modify, downgrade, expand, or overwrite the active Profile, its status, supported tasks, evidence registry, keyword bank, or sample library, except through the narrowly scoped explicit or under-20 `sample_ingestion` path defined below.
- A conflict between task material and the Profile affects only the current task. It does not trigger Profile Setup or Profile downgrade.
- Only an explicit user request to create or update the Profile authorizes general writes under `profiles/<company-id>/`.
- Read `workflows/sample-ingestion.md` after direct note deconstruction. When the active eligible Profile has fewer than 20 distinct effective samples, automatic `sample_ingestion` may update only its configured historical collection, sample library, and sample index. At 20 or more samples, require an explicit ingestion request. Neither path may change brand, product, audience, visual, compliance, evidence, keywords, search terms, profile status, or supported tasks.
- If the user explicitly requests a Profile update during production, pause production and run `workflows/profile-setup.md` as a separate Profile update step.

## Normalize collection inputs

Read `schemas/collection-fields.md` and the adapter selected by the active profile.

- Accept Markdown, CSV, spreadsheet exports, or pasted tables.
- Map source columns to the canonical fields before analysis.
- Preserve unknown useful columns as `extra_notes`.
- Never invent missing engagement figures, dates, links, or account information.
- Use `adapters/collection/default.md` when the incoming table already matches the canonical schema.

## Deconstruct external Xiaohongshu notes

Read `templates/note_collection_prompt.md` whenever the user asks how to deconstruct another company's Xiaohongshu graphic post, requests a GPT-ready deconstruction prompt, asks Codex to perform that deconstruction, or uses an equivalent expression. Before executing a deconstruction, read `templates/note_collection_granularity_example.md` only to calibrate field detail.

- If the user asks how to do it or requests a prompt, return the stored copyable prompt plus the granularity example as the minimum deliverable. Clearly label the example as detail calibration only. Do not require a Profile, production topic, or Profile Setup.
- If the user asks Codex to deconstruct supplied screenshots, OCR, body text, or manual notes, execute the stored prompt internally and return its table. Do not expose the prompt unless requested.
- If the user provides only a link, ask for screenshots, OCR, or body text. Do not crawl or pretend to have inspected the note.
- Treat the supplied note itself as the analysis object; this branch does not require a separate production topic.
- Treat the granularity example as `granularity_only`: never use it for topic selection, sample analysis, content generation, layout transfer, brand adaptation, sample indexing, or the 20-sample capacity count.
- Leave brand connection blank unless the user supplies a target Profile or explicitly requests adaptation to the active Profile.
- After direct deconstruction, read `workflows/sample-ingestion.md`. Automatically save non-duplicate results while the active eligible company has fewer than 20 effective samples; at 20 or more, save only when the user explicitly requests collection, ingestion, archiving, saving, or sample-library storage.

## Explain this Skill

Read `references/standard-workflow-case.md` only when the user asks about this Skill's workflow, usage, expected inputs, file handling, revision process, or another matter concerning how this or a related Skill works. You may share the case with the user and must identify it as a normative workflow example.

Do not read or apply this case during ordinary content production, sample collection, image planning, image generation, or quality review. It is an explanation example only, not a topic source, content template, visual template, reference sample, or source of enterprise facts.

## Mandatory production defaults

Before every sample-analysis, content, image-plan, or image-generation task, read and apply `workflows/mandatory-production-defaults.md`.

The required order is:

1. obtain an explicit user topic;
2. independently filter all supplied materials against that topic;
3. default to abstract visuals without real UI or customer cases;
4. describe image style, text density, and color proportion before image approval;
5. after image generation and quality review, ask whether to package the ordered images on the desktop.

Do not run keyword selection by default. Read keyword resources only when the user explicitly requests keyword research, search intent, or topic candidates.

## Workflow

### 1. Identify intent

Read `workflows/task-routing.md`. Classify the request as profile setup/update, sample analysis, sample ingestion, content generation, image-plan design, image-plan approval, image generation, page quality review, or compliance review.

Apply the Profile Setup Gate before all production branches. Then apply the mandatory topic gate in `workflows/mandatory-production-defaults.md`. Do not treat company documents, reference samples, Profile defaults, or keyword priority as an implicit topic.

Information responsibilities are fixed:

- the user's request determines the current task goal, topic, and deliverable;
- current-task PPTs, PDFs, articles, screenshots, and briefs determine what may be used in this task only;
- the active Profile supplies long-term brand, product-fact, audience, voice, visual, and compliance boundaries, but does not choose the current topic;
- reference samples supply structure, motivation, hierarchy, and visual-organization patterns only, never company facts.

Use the minimum-delivery rules in `workflows/task-routing.md`. Do not run or expose the full workflow when the user requested only one smaller deliverable.

### 2. Material readiness gate

Before analyzing samples, establishing the content spine, producing a plan, generating content, or delivering any business result, read `workflows/material-readiness.md` and `schemas/material-readiness-fields.md`.

Assess whether current-task materials are sufficient for the requested minimum deliverable. Treat the Profile only as a long-term baseline; do not treat it as evidence that current campaign, customer, case, UI, or data materials exist.

- `complete`: continue without a readiness notice;
- `proceed_with_assumptions`: show the short readiness notice before generation, then continue with stated conservative assumptions;
- `awaiting_material`: ask only for the smallest material or information that materially affects the requested result; do not deliver pseudo-complete output;
- `blocked`: state the hard missing condition and do not continue unsafe production.

When the user says “直接生成”, skip only non-blocking follow-up questions. Do not skip the readiness notice, fact boundaries, permissions, confidentiality checks, validation, or image approval.

### 3. Analyze reference notes

Read the active profile's sample index when available. Select 1-2 primary samples by topic and quality. Analyze transferable structure, motivation, information hierarchy, proof style, save/share triggers, and CTA style. Separate observations from interpretation.

### 4. Filter company evidence

Read `rules/task-material-isolation.md` and `schemas/task-material-fields.md` before using materials supplied for the current task.

Keep task materials separate from the long-term Profile. Classify each item as:

- `task_direct`: usable in this task within its verified scope;
- `task_background`: context only, not product evidence;
- `task_reference`: structure or visual reference only;
- `task_confirm`: requires current-task confirmation;
- `task_restricted`: may help internal understanding but cannot appear in output;
- `task_exclude`: off-topic, unsafe, unsupported, or unusable.

Record whether each item matches, supplements, conflicts with, or is unrelated to the Profile. Profile hard constraints remain authoritative. Explicit current-task requirements may override Profile defaults such as topic, audience emphasis, format, page count, or campaign theme, but they do not persist after the task.

Tie final product claims to approved Profile capabilities or clearly scoped current-task evidence. Do not treat softer wording as a substitute for evidence. Do not write task materials into the Profile unless the user separately authorizes a Profile update; the only exception is the narrowly scoped sample ingestion allowed by `workflows/sample-ingestion.md`, which cannot change Profile facts.

### 5. Reconstruct original content

Read `workflows/content-consistency.md`, `schemas/content-spine-fields.md`, `rules/xiaohongshu-transfer-rules.md`, and any enterprise-specific transfer rules named by the active profile. Establish the content spine before writing titles, body copy, carousel pages, or image plans. Use `templates/output_template.md`. Apply the active brand voice, audience, product facts, visual profile, and compliance rules. Do not reuse titles, sentences, cases, screenshots, compositions, palettes, or distinctive phrasing from other sources. Run the content-consistency check after drafting and before image-plan approval or final validation; send failures to `workflows/validation-repair.md`.

### 6. Build the carousel

For 6-9 pages, use this default narrative:

1. Topic and user problem.
2. Scenario, misconception, or consequence.
3. Problem breakdown.
4. Method or decision path.
5. Product-supported solution.
6. Business value and natural next step.

Vary page layouts. Avoid making every page a card grid.

### 7. Design and approve the image plan

Read `workflows/image-approval.md` and use `templates/image_plan_template.md` for every image-generation request, including requests such as “直接出图”.

Before showing the plan, read the active visual Profile. Default to abstract visuals without real UI or customer cases. Check asset availability and permission only when the user explicitly requests a real product UI, screenshot, logo, or customer asset.

The human-readable plan must state the visual style, visible-text range or density, and color proportion before it can move to `awaiting_approval`.

Image generation has four ordered phases:

1. image-plan design;
2. image-plan approval;
3. page-by-page image generation;
4. page-by-page quality review.

The plan state must move from `draft` to `awaiting_approval` to `approved`. Do not call an image-generation tool unless the current plan is `approved`.

Before the first image call, run `workflows/validation-repair.md` against the approved plan and its page content. An image call requires both `image_plan_state: approved` and `validation_state: ready`.

An image call also requires `material_readiness: complete` or `proceed_with_assumptions`.

### 8. Generate, review, and hand off images

After approval, reload the active visual Profile before producing final technical prompts. Do not rely on an earlier summary or memory of it. Each page must preserve the approved goal, visible text, main visual, layout, and exclusions.

Build every final page prompt from the approved human-readable page plan plus the complete technical attachment from the active Visual Profile. Do not ask ordinary users to review or choose the attachment. Before generation, set `visual_profile_state` to `ready` only when the active Visual Profile explicitly supplies visual style, palette, color proportion, brand-color rendering, area limits, layout preferences, brand-asset rules, and prohibited elements. If any required field is blank, missing, provisional without permission, or inherited from another Profile, stop image generation and run the Profile Setup Gate.

Every final prompt must include these brand-neutral production constraints:

- `3:4 vertical Xiaohongshu image` and `single standalone page`;
- Generate independent 3:4 vertical Xiaohongshu single page separately; no collage, no combined long image;
- default medium information density: about 80-130 visible Chinese characters, usually 1 top label, 1 main title, a 30-50-character explanation, and 3-6 short labels or nodes;
- do not make an empty text-light cover or an overfull PPT-like page;
- no collage, compilation, long image, real QR code, real customer data, real customer logo, or unverified number.

Append every confirmed value from the active Visual Profile with the same specificity recorded there. Do not summarize away color codes, proportions, rendering methods, area limits, layouts, asset rules, or prohibited elements. Do not inherit visual values from another Profile. The text-density ranges above are brand-neutral defaults unless the user, approved image plan, or active Visual Profile explicitly overrides them.

Override default medium density only when the user explicitly requests a minimal/strong-visual page, a high-density checklist/method/field page, or the approved image plan explicitly assigns another density to that page. The final prompt must always state the chosen density and visible-text range.

When generating images:

- create one independent `3:4 vertical Xiaohongshu image` per call;
- state `single standalone page`, no collage, no spliced long image;
- judge every page before continuing;
- reject collages, garbled text, off-profile colors, unreadable density, copied visuals, unsupported claims, real QR codes, or sensitive data.
- regenerate technical failures without another approval only when the approved content and visual direction remain unchanged;
- return to `draft` and request approval again when any material plan change listed in `workflows/image-approval.md` occurs.

Run validation and recheck after each generated page. A page may be technically regenerated only under the unchanged-plan conditions in `workflows/image-approval.md` and `workflows/validation-repair.md`.

After the final requested image passes page-quality review, follow the desktop handoff in `workflows/mandatory-production-defaults.md`. Ask whether the user wants the pages named in order and packaged on the desktop unless destination instructions were already provided.

## Output order for a full-package request

Use this order only when the user explicitly asks for a complete content package. Otherwise return only the minimum sections required by `workflows/task-routing.md`.

1. Active profile and assumptions
2. Reference-pattern summary
3. Current-task material filtering
4. Content direction and titles
5. Cover copy and prompt
6. Carousel narrative and page prompts
7. Body draft, CTA, and tags
8. Compliance self-check

## Validation, repair, and recheck

Read `workflows/material-readiness.md`, `schemas/material-readiness-fields.md`, `workflows/validation-repair.md`, `schemas/validation-issue-fields.md`, `checklists/compliance_checklist.md`, the active compliance profile, and any enterprise-specific checklist named by the profile before delivering any requested result.

Use `draft` → `checking` → `auto_fixing` / `awaiting_confirmation` / `blocked` → `rechecking` → `ready`.

- classify every failed check as `AUTO_FIX`, `CONFIRM`, or `BLOCK`;
- automatically repair only issues that do not change the user's core topic, audience, product facts, deliverable, long-term Profile, permissions, or approved image plan;
- after every automatic repair, perform local and critical-item rechecks;
- allow at most two automatic repair rounds for the same core risk;
- deliver a final result only when `validation_state` is `ready`;
- when `awaiting_confirmation`, deliver only the smallest blocking question or a safe partial result;
- when `blocked`, deliver only the reason, required condition, and any safe partial result.

## Encoding

Files are UTF-8. On Windows PowerShell, read Chinese Markdown and CSV files with `Get-Content -Encoding UTF8` before diagnosing corruption.
