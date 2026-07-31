# Validation, Repair, and Recheck Workflow

Use this workflow after producing any requested minimum deliverable, before final delivery, before the first image-generation call, and after each generated image page. It turns existing checks into a repair decision; it does not create a second content workflow.

Read `schemas/material-readiness-fields.md`, `workflows/material-readiness.md`, `schemas/validation-issue-fields.md`, `checklists/compliance_checklist.md`, the active compliance Profile, `workflows/task-routing.md`, `workflows/content-consistency.md`, and, for images, `workflows/image-approval.md`.

## Validation states

Use these states:

```text
draft
→ checking
→ auto_fixing / awaiting_confirmation / blocked
→ rechecking
→ ready
```

- Only `ready` may be delivered as a final result.
- `awaiting_confirmation` may deliver only the smallest blocking question and any safe partial result.
- `blocked` may deliver only the blocking reason, the condition needed to continue, and any safe partial result.
- Image generation additionally requires `image_plan_state: approved`.

## Record and classify every failure

Create a validation issue record for every failed check. Assign exactly one handling level.

### AUTO_FIX

Use `AUTO_FIX` only when the correction is clear and does not change the user's core topic, target audience, primary deliverable, product facts, long-term Profile, publication permission, customer-case authorization, or approved image plan.

Examples:

- delete unsupported performance numbers, rankings, and absolute promises;
- delete real customer names, phone numbers, QR codes, sensitive data, and unapproved logos;
- delete competitor brands, feature names, copied sentences, or clearly imitative expressions;
- rewrite a clearly imitative title into an original title while preserving the approved topic and audience;
- align a mildly inconsistent title, cover line, CTA, or page role with the established content spine;
- correct a numbered title or cover promise when the requested minimum deliverable does not supply that number of supported methods or pages;
- delete or compress an off-topic product paragraph, feature list, or carousel page;
- correct a CTA that violates the active Profile;
- remove unrequested output sections to restore minimum delivery;
- downgrade unsuitable task material to background or reference use;
- remove invented task-specific cases, data, campaign details, or UI claims and show the required readiness assumptions instead;
- repair formatting, duplicate tags, and obvious typos;
- add missing technical image constraints such as 3:4, standalone page, no collage, the approved text-density range, active Profile color codes, brand-color rendering, and area limits;
- regenerate a technical image failure when approved page content, visible text, and visual direction remain unchanged.

Never use weaker wording such as “可能”“助力” or “有望” to preserve an unsupported product capability or effect promise. Remove the product connection, or escalate to `CONFIRM` or `BLOCK`.

### CONFIRM

Use `CONFIRM` when more than one reasonable choice exists or a correction would change the user's core intent.

Examples:

- topic, target audience, or primary deliverable is unclear;
- current-task materials conflict on a function, version, or number;
- a feature's release status is unclear;
- public permission for a case, screenshot, or data is unclear;
- removing risky content would require a different topic;
- the user requests a temporary position that conflicts with the long-term Profile;
- a user-supplied material or permission is needed to materially improve the requested result;
- the requested topic and required product capability cannot form one coherent business path;
- the user gives multiple unrelated topics, or target audience, CTA, and deliverable conflict;
- an image change invalidates the approved plan under `workflows/image-approval.md`.

Ask only the smallest question that blocks the current task. Do not present an unconfirmed alternative as final content.

### BLOCK

Use `BLOCK` when a hard constraint is violated or the requested result cannot be safely completed through ordinary revision.

Examples:

- crawling, scraping, or automated Xiaohongshu access is requested;
- competitor copying is requested;
- the active Profile is wrong or cannot support the requested production capability;
- a core product capability has no Profile or task-local evidence allowed by the current-task isolation rules;
- essential material is confidential;
- the user insists on false performance data or unauthorized customer cases;
- the user insists on displaying real phone numbers, personal information, QR codes, or other sensitive data;
- the article core depends on an unapproved product capability;
- no explainable business spine can be formed and the user does not confirm a new direction;
- image generation is requested without `image_plan_state: approved`;
- image generation is requested while material readiness is `awaiting_material` or `blocked`;
- image generation is requested while validation is not `ready`;
- the same core risk remains after two automatic repair rounds.

Do not return a pseudo-complete result when blocked.

## Repair and recheck loop

1. Set state to `checking` and run only checks relevant to the requested minimum deliverable.
2. Create issue records for failures.
3. If any `BLOCK` exists, set state to `blocked` and stop unsafe production.
4. If `CONFIRM` exists and no `BLOCK` exists, set state to `awaiting_confirmation` and ask the minimum question.
5. If only `AUTO_FIX` issues exist, set state to `auto_fixing`, repair them, then set state to `rechecking`.
6. Perform local recheck on the changed title, body, CTA, tag, page, source decision, or format.
7. Perform critical-item recheck: material readiness and required notice, content spine, Profile boundaries, product facts, sensitive information, originality, long-term/short-term isolation, minimum delivery, and image approval state when applicable.
8. Set state to `ready` only when all relevant critical checks pass.

Allow at most two automatic repair rounds for the same core risk. If that risk remains, classify the next action as `CONFIRM` when user direction could resolve it; otherwise classify it as `BLOCK`.

## Minimum repair scope

Keep repairs within the requested deliverable:

| Requested result | Repair scope |
|---|---|
| Titles | Titles only |
| Body copy | Body, necessary title, CTA, and tags only |
| Sample analysis | Observation/interpretation separation, originality, and enterprise-fact isolation only |
| Compliance review | Findings and revision advice; revise content only when explicitly requested |
| Image plan | Plan content only; never generate before approval |
| Generated image with technical failure | Regenerate only against the unchanged approved plan |
| Generated image requiring material change | Return the plan to `draft` and request approval again |

## Image-specific decisions

Treat collage output, contact sheets, long images, unreadable or garbled Chinese, palette drift, density imbalance, exposed QR codes, customer data, real logos, non-3:4 pages, and obvious deviation from the approved plan as technical failures when correcting them preserves the approved page content, visible text, and visual direction. Use `AUTO_FIX` and regenerate that page.

Also treat these as technical `AUTO_FIX` failures: visible text clearly falls outside the approved range without an approved density override; the plan or prompt omits the text range; the prompt omits or weakens any required Visual Profile value; the output materially deviates from the Profile palette, color proportion, rendering method, area limits, layout preferences, asset rules, or prohibited elements. Regenerate without new approval only when the fix does not change the approved title, key visible text, page topic, page count, or main visual direction. If the active Visual Profile is incomplete or was not loaded, use `BLOCK` rather than guessing or inheriting values.

If a correction changes the topic, page count, order, main title, target audience, product capability, case or data, primary visual direction, page set, or changes an abstract interface to real product UI, return to `draft`. Follow `workflows/image-approval.md` and request plan approval again.

## Final communication

- `ready`: state that self-check passed; mention only important automatic repairs.
- `awaiting_confirmation`: state exactly what needs confirmation.
- `blocked`: state why safe completion is not possible and what condition is needed.

Do not expose the full issue table unless the user asks for an audit. Do not let the repair process modify the long-term Profile or promote temporary task materials.
