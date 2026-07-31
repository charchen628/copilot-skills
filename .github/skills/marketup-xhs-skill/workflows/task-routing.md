# Task Routing and Minimum Delivery

Use this workflow before content analysis or production. Read `workflows/mandatory-production-defaults.md` first. The user's current request determines the task; Profile defaults, task materials, keyword priority, and reference samples must not silently choose the topic or expand the deliverable.

## Mandatory topic gate

For sample analysis, content generation, image-plan design, and image generation, production cannot start until the user states or confirms a topic.

Exception: delivering the stored deconstruction prompt or directly deconstructing user-supplied Xiaohongshu screenshots, OCR, body text, or manual notes does not require a separate production topic. The supplied note is the explicit analysis object. This exception does not authorize content generation.

- Materials being present does not equal a topic.
- Do not derive or choose the topic from supplied materials.
- When the topic is missing, ask only for the topic and stop production.
- Profile setup/update and explicit sample ingestion may proceed without a production topic because they do not produce publishable content.

## Detect the routing signals

Determine:

- `has_topic`: the user explicitly provides or confirms a subject, business problem, campaign direction, or content angle;
- `has_generation_request`: the user explicitly asks to write, create, produce, design, output, or generate a new deliverable;
- `requested_deliverable`: analysis, ingestion, topics, titles, body copy, carousel plan, image plan, images, or compliance review;
- `has_image_generation_request`: the user asks for actual generated images, including “直接出图”.
- `has_deconstruction_prompt_request`: the user asks how to deconstruct another company's Xiaohongshu graphic post or requests a GPT-ready prompt.
- `has_direct_deconstruction_request`: the user asks Codex to deconstruct supplied Xiaohongshu screenshots, OCR, body text, or manual notes.

Materials being present does not equal `has_topic`. A Profile topic preference, high-priority keyword, document title, or reference-note theme does not equal user confirmation.

## Topic and generation routing

### 1. No topic

- Do not select a topic from the Profile, keyword bank, sample library, or highest-priority material.
- Ask what topic the user wants.
- Stop sample analysis and production until the user supplies or confirms a topic.

### 2. Topic but no clear generation request

- Use context to decide whether the user wants topic-based analysis/archiving or new content.
- When the intent remains ambiguous, ask one plain-language question and do not generate meanwhile.

Use:

> 这次是只拆解并整理这些参考内容，还是还要基于它们生成一篇新内容？如果要生成，请告诉我主题。

For users who do not know how to phrase the request, add:

> 你可以直接说：请根据这些资料，生成主题为“XXX”的小红书图文。

### 3. Topic and explicit generation request

- Enter the requested production workflow directly.
- Analyze samples internally as needed.
- Do not expose a long sample-breakdown report unless the user requests it or a material risk must be explained.
- Produce only the requested deliverable.

## Task categories

Use these categories and dependencies:

1. `deconstruction_prompt`
2. `sample_analysis`
3. `sample_ingestion`
4. `profile_setup_or_update`
5. `content_generation`
6. `image_plan_design`
7. `image_plan_approval`
8. `image_generation`
9. `page_quality_review`
10. `compliance_review`

For `deconstruction_prompt` and direct source-faithful `sample_analysis`, read `templates/note_collection_prompt.md`. Deliver the prompt when requested; otherwise execute it internally, then read `workflows/sample-ingestion.md` to apply the 20-sample capacity rule. Do not enter Profile Setup unless the user asks to connect the analysis to an unprepared target company.

`image_generation` is not a direct independent entry. It requires an `approved` image plan. `page_quality_review` follows each generated page.

## Minimum delivery

Return only the smallest useful result that completes the explicit request:

| User asks for | Minimum delivery |
|---|---|
| How to deconstruct / GPT prompt | The stored copyable prompt plus the `granularity_only` collection example |
| Direct note deconstruction | One canonical collection table; no brand draft |
| Titles | Candidate titles only, plus a one-line assumption only when necessary |
| Body copy | Title, body, necessary CTA, and tags |
| Sample breakdown | Structure, motivation, hierarchy, transferable patterns, risks, and fit; no brand draft |
| Topic candidates | 3-5 candidate topics with brief rationale; no full content |
| Carousel plan | Page order and page-level content; no generated images |
| Image plan | Human-readable approval plan; no image generation |
| Compliance review | Findings, severity, and required corrections; do not recreate the full content unless asked |
| Full package | Use all relevant sections of `templates/output_template.md` |

Do not add keywords, sample analysis, source filtering, prompts, carousel pages, or compliance narrative merely because the Skill supports them. Include a supporting section only when it is required to understand or safely use the requested result.

## Image-generation interception

If `has_image_generation_request` is true:

1. Route first to `workflows/image-approval.md`.
2. Build and display the image plan.
3. Set its state to `awaiting_approval`.
4. Stop before any image-generation tool call.
5. Continue only after the user explicitly approves the displayed plan.

An earlier phrase such as “直接出图” expresses the desired final deliverable but does not approve a plan that the user has not yet seen.

## Material readiness handoff

After identifying the task and its minimum deliverable, run `workflows/material-readiness.md` before sample analysis, content-spine creation, content production, image-plan design, image generation, or final delivery.

If this routing workflow has already stopped because the topic, target audience, or deliverable is unclear, treat the unresolved item as `awaiting_material` in the readiness gate. Do not let Profile defaults, document titles, keywords, or sample themes replace the missing user decision.
