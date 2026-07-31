# 默认采集表适配器

适用于 `templates/note_collection_template.md` 或已经使用标准字段的 CSV、Markdown 表格。

| 常见中文字段 | 标准字段 |
|---|---|
| 编号 / 笔记编号 | `sample_id` |
| 搜索关键词 / 关键词 | `keyword` |
| 笔记标题 / 标题 | `title` |
| 链接 / 截图编号 | `source_ref` |
| 发布时间 | `published_at` |
| 账号名称 | `account_name` |
| 账号类型 | `account_type` |
| 互动数据 / 可见互动数据 | `engagement` |
| 封面结构 / 封面描述 | `cover_observation` |
| 标题结构 / 标题公式 | `title_pattern` |
| 正文 / 正文摘要 | `body_text` |
| 正文结构 / 叙事路径 | `body_structure` |
| 评论信号 / 用户反馈 | `comment_signals` |
| 可迁移结构 / 值得借鉴的点 | `transferable_pattern` |
| 不能复制的点 | `do_not_copy` |
| 产品连接点 / 可迁移方向 | `brand_connection` |
| 合规风险 | `risk_notes` |

未匹配但有价值的列合并到 `extra_notes`，不要丢弃原始信息。
