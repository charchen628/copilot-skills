# Empty Enterprise Onboarding

Run this workflow immediately after this Skill is triggered by a Xiaohongshu/RedNote-related request and the selected enterprise information is substantially empty.

## Detect an empty enterprise information set

Treat the selected enterprise information as substantially empty when any of these conditions is true:

- `profile_status` is `template`;
- the Profile contains only placeholders or blank brand, product, audience, visual, and compliance fields;
- `supported_tasks` contains only `profile_setup`;
- no ready company Profile exists and `profiles/default/profile.md` is selected.

Do not trigger this workflow for an `active_limited` or `active` Profile merely because its keyword bank or sample library has fewer than 20 records.

## Conversation behavior

- Show the notice below once near the beginning of the current conversation. Do not repeat the full notice on every turn when it has already been shown.
- If the user supplies materials in the triggering request, show a shortened acknowledgement, inventory those materials, and enter `workflows/profile-setup.md`; do not ask them to upload the same files again.
- Use ordinary business language. “企业资料库” may be followed by the parenthetical explanation below; do not expose internal field names unless the user asks.
- Do not ask the user to organize everything first. Accept Word, PDF, PPT, spreadsheets, screenshots, pasted text, website exports, and existing collection tables.

## First-use notice

> 当前是空白企业版本，尚未配置企业资料库（用于保存品牌、产品、目标客户、视觉风格和公开边界的企业档案）。如果直接生成，内容可能比较通用，也可能无法准确体现企业能力和品牌视觉。
>
> 建议先上传现有资料：
> 1. 企业介绍、官网内容或品牌手册；
> 2. 产品或服务介绍及已经确认的能力；
> 3. 目标客户、内容目标和本次主题；
> 4. 如需生成图片，可补充 Logo、品牌色、视觉参考和禁用风格；
> 5. 如有不能公开、不能使用或需要谨慎表达的内容，请一并说明。
>
> 资料不必一次整理完整，直接上传现有的 Word、PDF、PPT、表格、截图或文字即可。我会先提取可用信息，再只询问影响当前任务的缺口。
>
> Skill 内还包含采集表（用于保存和拆解参考小红书图文的样本库）。你可以上传已有采集表，也可以提供参考图文的截图、正文或 OCR，由我按照统一字段完成拆解。企业资料库建立后，有效样本不足 20 条时，符合条件且不重复的拆解结果会默认存入该企业样本库。

## Route after the notice

- Skill usage, workflow explanation, stored deconstruction-prompt delivery, and source-faithful note deconstruction may continue because they do not require company facts. If no eligible company sample library exists, return the deconstruction without saving.
- Profile setup may continue immediately from supplied company materials.
- Company-branded titles, body copy, carousel plans, image plans, generated images, and company-specific compliance conclusions must wait until the Profile Setup Gate validates the requested task.
