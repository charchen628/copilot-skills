# 采集表标准字段

所有采集表在分析前映射到以下字段。缺失字段保留为空，不得推测。

| 标准字段 | 含义 | 必填 |
|---|---|---|
| `sample_id` | 样本编号 | 是 |
| `keyword` | 搜索关键词 | 是 |
| `title` | 笔记标题 | 是 |
| `source_ref` | 链接或截图编号 | 否 |
| `published_at` | 发布时间 | 否 |
| `account_name` | 账号名称 | 否 |
| `account_type` | 账号类型 | 否 |
| `engagement` | 可见互动数据 | 否 |
| `cover_observation` | 封面客观描述 | 否 |
| `title_pattern` | 去除原句后的标题结构公式 | 否 |
| `body_text` | 正文或摘要 | 否 |
| `body_structure` | 正文叙事与论证顺序 | 否 |
| `comment_signals` | 评论区问题和意图信号 | 否 |
| `transferable_pattern` | 可迁移结构 | 否 |
| `do_not_copy` | 禁止复制内容 | 是 |
| `brand_connection` | 与当前企业的连接点 | 否 |
| `risk_notes` | 合规风险 | 否 |
| `extra_notes` | 未映射的其他信息 | 否 |
