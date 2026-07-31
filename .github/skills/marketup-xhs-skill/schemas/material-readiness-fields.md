# 资料准备度字段

本 schema 记录当前任务的资料是否足够。它是通用任务状态，不属于任何企业 Profile，也不得将当前任务资料写入长期 Profile。

| 字段 | 说明 |
|---|---|
| `material_readiness` | `complete`、`proceed_with_assumptions`、`awaiting_material` 或 `blocked` |
| `available_materials` | 当前任务可用的用户请求、附件、短期资料、已批准 Profile 基线和参考样本 |
| `missing_materials` | 缺少的资料、事实、授权、审批或用户决定 |
| `impact` | 缺失对当前最小交付的影响 |
| `assumptions` | 在 `proceed_with_assumptions` 下使用的保守假设 |
| `next_action` | 直接继续、展示资料提示、询问最少问题、等待资料或阻断说明 |
| `task_scope` | 本次任务类型、主题、目标受众、最小交付物和是否涉及图片 |
| `profile_used_as_baseline` | 使用的长期 Profile 名称及其仅作为边界/事实基线的角色 |

`available_materials` 中的 Profile 不能证明当前活动、客户、案例、截图、数据或临时功能资料存在。`material_readiness` 不得修改 Profile 状态、长期证据、关键词库或样本库。
