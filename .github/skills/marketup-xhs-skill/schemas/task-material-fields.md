# 短期任务资料字段

本 schema 只描述当前任务资料。记录默认不持久化，绝不能写入长期 Profile evidence registry。

| 字段 | 含义 |
|---|---|
| `task_source_id` | 当前任务内稳定编号，例如 `TASK-SRC-01` |
| `source` | 文件名、附件、截图编号或粘贴内容 |
| `role` | 产品资料、业务背景、历史内容、参考样本、视觉资料或敏感资料 |
| `task_scope` | 适用的当前主题、页面、活动、产品或时间范围 |
| `use_decision` | `task_direct`、`task_background`、`task_reference`、`task_confirm`、`task_restricted` 或 `task_exclude` |
| `profile_relation` | `matches_profile`、`supplements_profile`、`conflicts_with_profile` 或 `unrelated_to_profile` |
| `task_fact_status` | `task_supported`、`task_confirmed`、`task_inferred`、`task_conflicting` 或 `task_restricted` |
| `publicity` | `public`、`internal`、`confidential` 或 `unknown` |
| `allowed_output` | 正文、图片文字、视觉参考、仅内部理解或禁止输出 |
| `reason` | 使用、限制、确认或排除原因 |
| `expires_after` | 固定为 `current_task` |
| `promoted_to_profile` | 默认且必须为 `false`；只有独立 Profile Update 完成后才能改变长期资料 |
| `promoted_to_sample_library` | 默认 `false`；用户明确执行 `sample_ingestion`，或当前合格企业样本不足 20 条触发自动入库时，才能由独立入库流程处理 |

## 使用限制

- `task_inferred`、`task_conflicting`、`task_restricted` 不得作为公开产品声明。
- `task_reference` 不得作为当前企业事实或产品能力证据。
- `publicity: unknown` 按不可公开处理。
- `conflicts_with_profile` 不得自动覆盖 Profile。
- 普通内容任务不得修改 `promoted_to_profile`。
- 普通内容任务不得修改 `promoted_to_sample_library`；显式样本导入或不足 20 条时的自动入库只能更新历史采集表、样本库和索引。
- Task Material Brief 即使保存，也必须位于当前任务输出目录并标记 `current_task_only`。
