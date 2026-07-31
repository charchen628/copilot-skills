# Material Readiness Gate

Run this workflow after task routing identifies the requested minimum deliverable and before sample analysis, content-spine creation, production, image-plan design, image generation, or business-result delivery. Read `workflows/mandatory-production-defaults.md` first.

This is a generic current-task decision. It is outside every enterprise Profile. Profile files provide long-term identity, approved product facts, defaults, visual rules, and compliance boundaries; they do not prove that this task has current campaign, customer, case, screenshot, or data material.

Read `schemas/material-readiness-fields.md`, `workflows/task-routing.md`, `rules/task-material-isolation.md`, the active Profile, and the requested task's workflow.

## Assess in order

1. Confirm task scope: requested minimum deliverable, explicit topic, target audience when relevant, and whether the user explicitly overrides the default abstract-visual treatment.
2. Inventory only materials supplied or explicitly scoped to this task, plus the active Profile as a long-term baseline.
3. Separate missing inputs into: optional detail, material that materially improves quality, core fact, publication permission, confidentiality boundary, user decision, or required approval.
4. Determine whether the missing input can be handled by a conservative assumption without inventing facts or changing the requested result.
5. Set one readiness state and, unless it is `complete`, prepare the short user-facing readiness notice.

Do not use a document title, keyword priority, reference sample, or Profile default to silently fill a missing topic, audience, deliverable, activity, data, or authorization.

By default, real product UI, screenshots, and customer cases are not required. Their absence is not a missing-material condition and must not trigger a readiness notice or follow-up question. Use abstract visuals unless the user explicitly requests real assets.

## States

### `complete`

Current materials are sufficient for the requested minimum deliverable. Continue without a readiness notice.

### `proceed_with_assumptions`

Some material is missing, but the task can be safely completed without it. Before generation, show:

```text
资料提示：
- 当前可用：……
- 当前缺少：……
- 影响：……
- 本次处理：直接继续并采用……
```

Use conservative assumptions. Use only the user topic, relevant portions of current-task materials, and approved Profile facts; do not invent activity data or unverified feature details.

When the user says “直接生成”, do not ask non-blocking questions. Still show this notice and preserve all fact, authorization, confidentiality, validation, and image-approval hard constraints.

### `awaiting_material`

Use when user-supplied material or a user decision is missing and would materially affect the requested result. Ask only for the smallest blocking item. Do not create a pseudo-complete result.

Examples:

- sample analysis is requested but no sample is supplied;
- a real product asset is explicitly requested but no source or permission is supplied;
- evidence-dependent public content is explicitly requested but no supporting material or publication permission is supplied;
- topic, target audience, or deliverable cannot be determined after task routing.

### `blocked`

Use when a core fact, publication permission, confidentiality boundary, or required approval makes safe completion impossible.

Examples:

- a core product capability has no approved Profile or current-task evidence;
- required material is confidential;
- the user insists on unsupported or unauthorized public claims;
- image generation lacks an approved image plan or ready content validation.

## Minimum materials by task

| Task | No current-task material behavior |
|---|---|
| Titles | `proceed_with_assumptions`: generate from user topic and Profile, and say no current case or data is used |
| Body copy | `proceed_with_assumptions`: generate from user topic and Profile, without current cases, data, or specific campaign details |
| Topic candidates | `proceed_with_assumptions`: offer 3-5 directions and say they were not validated against current materials or samples |
| Sample analysis | `awaiting_material`: cannot analyze a sample that was not supplied |
| Carousel plan | Use abstract visuals by default; missing real UI does not lower readiness |
| Image plan | Use abstract visuals by default; describe style, text density, and color proportion before approval |
| Image generation | Require `complete` or `proceed_with_assumptions`, plus `validation_state: ready` and `image_plan_state: approved` |
| Explicit evidence-dependent content | `awaiting_material` or `blocked` when formal material or public permission is missing |

Missing material does not automatically stop a task. Stop only when it affects the topic, core facts, authorization, confidentiality boundary, or required approval.

## Output and persistence

Show no readiness output for `complete`.

For every other state, show only the short readiness notice. Do not expose an internal material table unless the user asks for an audit.

Task materials remain short-lived under `rules/task-material-isolation.md`. This gate must not modify the active Profile or promote current materials into long-term facts.
