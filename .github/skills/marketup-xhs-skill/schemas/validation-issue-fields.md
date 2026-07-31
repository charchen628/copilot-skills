# 验证问题记录字段

每个未通过的验证项都必须有一条问题记录。问题记录供内部决策和复检使用，普通用户默认只看到必要的结论。

| 字段 | 说明 |
|---|---|
| `issue_id` | 当前任务内稳定编号，例如 `VAL-001` |
| `category` | 路由、最小交付、事实、合规、原创、任务资料、视觉、图片方案、图片质量或格式 |
| `location` | 标题、正文、CTA、标签、资料筛选、图片方案、第 N 页或输出结构 |
| `problem` | 观察到的具体问题 |
| `severity` | `AUTO_FIX`、`CONFIRM` 或 `BLOCK` |
| `evidence` | 对应 Profile、任务资料、样本、检查项或已确认图片方案 |
| `action` | 删除、改写、降级资料、技术重生成、询问用户、停止交付等 |
| `status` | `detected`、`fixed`、`awaiting_confirmation`、`blocked` 或 `passed` |
| `repair_summary` | 已执行的修复及其范围 |
| `recheck_result` | 局部复检和关键项复检的结论 |

问题记录不得将临时资料提升为长期 Profile 事实，也不得代替用户对主题、受众、授权、资料公开权限或图片方案的确认。
