# Mandatory Production Defaults

Run this workflow before every `sample_analysis`, `content_generation`, `image_plan_design`, or `image_generation` task. These defaults override older optional production behavior unless the user explicitly requests a different current-task treatment.

## 1. Topic gate and material selection

- Require the user to state or confirm the topic before production starts.
- Treat attached documents, document titles, Profile defaults, sample themes, and keyword files as materials, never as topic confirmation.
- After the topic is confirmed, inventory the supplied materials and decide independently what is directly useful, background-only, structural reference, or excluded for that topic.
- Do not ask the user to pre-sort mixed or partially relevant materials. Ask only when a core fact, permission, conflict, or deliverable decision cannot be resolved safely.
- Do not run keyword selection or output keyword analysis by default. Use keyword resources only when the user explicitly requests keyword research, search intent, or topic candidates.

## 2. Default image source and visual language

- Default to no real product interface and no customer case.
- Do not treat the absence of real UI, screenshots, customer material, or cases as missing material.
- Use abstract business flows, nodes, relationship diagrams, typographic information posters, and generic non-identifying SaaS components by default.
- Use real UI, screenshots, or customer material only when the user explicitly requests them and their source and permission are clear.

## 3. Required style preview before image generation

Before requesting approval for an image plan, always state:

- the overall visual style and page structure;
- the default visible-text range and any page-level density exceptions;
- the color proportion or perceived color-emphasis ratio;
- how the dominant brand color appears, including whether it is a background, block, line, brush stroke, arrow, keyword, or small graphic.

Read these values from the active Visual Profile and reproduce them exactly in the style preview. Do not replace specific color codes, proportions, rendering methods, area limits, layout preferences, asset rules, or prohibited elements with a generic phrase such as “follow the brand style.” If a required value is missing, do not request image-plan approval; return to the Profile Setup Gate.

## 4. Post-generation desktop handoff

After all requested images are generated and page-quality review passes, ask:

> 图片已生成完成，需要我按顺序命名并打包放到桌面上吗？

- Ask this immediately after the final image unless the user already supplied a destination and naming/package instructions.
- Do not write to the desktop before the user confirms.
- After confirmation, preserve the reviewed originals, copy the deliverables, name them in page order, and verify the packaged file list.
