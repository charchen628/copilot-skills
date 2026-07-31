# Image Plan Approval Workflow

Every request for actual image generation must pass this workflow before the first image-generation tool call. This includes single images, covers, carousels, and requests such as “直接出图”. Read `workflows/mandatory-production-defaults.md` first.

## States

Use exactly these plan states:

- `draft`: the plan is being prepared or has materially changed;
- `awaiting_approval`: the complete human-readable plan has been shown to the user;
- `approved`: the user explicitly approves the currently displayed plan.

Silence, an earlier request to generate, approval of a different version, or approval of only the written article does not set the image plan to `approved`.

Track an `image_plan_version`. Any material change creates a new version and returns the state to `draft`.

## Required plan content

Read the active visual Profile before drafting the plan. Default to abstract visuals without real product UI or customer cases. Check availability and permission only when the user explicitly requests a real product UI, screenshot, logo, customer material, or brand asset.

Before requesting approval, show at least:

- total page count;
- carousel narrative order;
- what each page communicates;
- the cognition or decision each page should change;
- each page's main title;
- key visible text;
- main visual;
- layout type;
- brand visual direction;
- visible-text range and density, including page-level exceptions;
- color proportion or perceived color-emphasis ratio, plus how the brand color will appear;
- prohibited content.

Use `templates/image_plan_template.md`.

For ordinary users, show only the human-readable plan: what each page says, its main text, and its visual direction. Do not require the user to review technical prompt syntax.

Show complete image-generation prompts only when the user requests deep prompt review or needs to audit implementation details.

## Approval request

After showing the complete plan, set the state to `awaiting_approval` and ask the user to approve or request changes. Do not call an image-generation tool in the same step.

Only an explicit approval of the displayed `image_plan_version` changes the state to `approved`.

## Changes that invalidate approval

Return to `draft`, update the version, show the changed plan, and request approval again when any of these changes:

- topic;
- total page count;
- page order;
- any main title;
- added or removed product capability;
- target audience;
- customer case or data;
- primary visual direction;
- added or removed page;
- abstract interface changed to real product UI.

Technical additions do not require another approval when they preserve the approved content and visual direction. Examples include `3:4 vertical`, `single standalone page`, no collage, exact approved color codes, safe-area wording, or tool-specific rendering instructions.

## Automatic technical attachment

The image plan shown to ordinary users confirms page meaning, main visible text, main visual, layout, and prohibited content. It does not require the user to choose default density, color codes, brand-color area limits, or rendering syntax.

After the plan is approved, reload the active Visual Profile and append its complete technical attachment to every final page prompt. Set `visual_profile_state: ready` only when visual style, palette, color proportion, brand-color rendering, area limits, layout preferences, brand-asset rules, and prohibited elements are explicit and confirmed. Otherwise stop and run the Profile Setup Gate.

Append these brand-neutral production constraints after the Profile attachment:

- `3:4 vertical Xiaohongshu image`; `single standalone page`; and `单独生成第X张小红书3:4竖版分页图，不要拼图，不要合集`;
- default medium density: about 80-130 visible Chinese characters, normally 1 top label, 1 dominant title, a 30-50-character explanation, and 3-6 short labels or nodes;
- prevent text that is too sparse like an empty cover or too dense like a PPT screenshot;
- prohibit collage, compilation, long image, real QR code, real customer data, real customer logo, and unverified numbers.

Copy every confirmed Profile value at full specificity. Do not summarize the attachment, omit inconvenient restrictions, or inherit values from another Profile. The density ranges above remain the brand-neutral default unless the user, approved plan, or active Visual Profile explicitly overrides them.

Override medium density only when the user explicitly requests a minimal/strong-visual page, a high-density checklist/method/field page, or the approved plan explicitly assigns another density. State the override in the final prompt: low density is normally 30-60 visible Chinese characters; high density is normally 130-180 visible Chinese characters. This technical attachment does not need another approval unless it changes approved content or visual direction.

Technical regeneration after a failed page does not require another approval when it only fixes garbled text, aspect ratio, collage output, readability, density, or palette drift without changing approved content.

## Generation and review

After state `approved`:

1. confirm current material readiness is `complete` or `proceed_with_assumptions`, and content validation is `ready` under `workflows/validation-repair.md`;
2. add the required technical prompt constraints without changing approved meaning;
3. generate one standalone page per call;
4. review and validate each page before continuing;
5. regenerate technical failures against the same approved plan;
6. stop and return to `draft` if a material content or visual change is needed.

After all requested pages pass review, immediately ask whether the user wants the pages named in order and packaged on the desktop, unless the user already supplied destination and naming instructions.

Never interpret image quality review as permission to redesign the approved narrative silently.
