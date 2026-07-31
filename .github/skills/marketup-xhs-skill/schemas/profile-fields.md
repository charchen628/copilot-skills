# 企业 Profile 字段与可用状态

每个企业目录必须包含 `profile.md`。执行任何任务前先读取以下控制字段：

- `profile_status`：`template`、`draft`、`active_limited` 或 `active`。
- `supported_tasks`：当前 Profile 已验证并允许执行的任务。
- `last_verified_at`：最近一次人工或资料验证日期；未知时留空，不得编造。

状态含义：

| 状态 | 含义 | 允许行为 |
|---|---|---|
| `template` | 未初始化的空壳 | 只能执行 `profile_setup` |
| `draft` | 已抽取部分资料，但存在关键缺失或冲突 | 继续 Setup、输出缺口与待确认项 |
| `active_limited` | 仅满足部分任务门槛 | 只执行 `supported_tasks` 中列出的任务 |
| `active` | 核心 Profile 已验证 | 执行已列出的完整任务 |

`profile.md` 还必须提供以下文件路径：

- `brand`：品牌定位、名称、语气、术语和禁用表达。
- `product`：产品事实、能力边界、可证明价值和禁用声明。
- `audience`：目标读者、使用场景、决策角色和认知水平。
- `visual`：视觉风格、色号、颜色比例、品牌色表现方式、面积限制、字体倾向、布局、品牌资产规则和禁用元素。文字密度使用工作流通用默认值；只有企业存在明确差异时才记录覆盖值。
- `compliance`：企业附加合规规则、CTA 和敏感信息边界。
- `evidence_registry`：Profile 事实、来源和证据状态登记文件；所有新建或经 Profile Setup 更新的 Profile 必须提供。既有已批准 Profile 可在下次资料维护时补建。
- `keywords`：关键词 CSV。
- `search_terms`：可选的搜索词映射 CSV。
- `collection_adapter`：采集表字段映射文件。
- `historical_collection`：可选的企业采集主表；提供时作为有效样本计数和默认追加位置。
- `sample_index`：可选的参考样本索引。

## 任务开放门槛

| 任务 | 最低条件 |
|---|---|
| `profile_setup` | Profile 目录和 manifest 存在 |
| `content_generation` | 品牌名称与定位、至少一项经确认的产品能力、主要读者、基础合规边界 |
| `image_plan_design` | `content_generation` 条件，加视觉风格、色板、颜色比例、品牌色表现方式、面积限制、布局、禁用元素和资产使用规则 |
| `image_generation` | `image_plan_design` 条件，加完整可附加的视觉技术配置，以及允许使用的品牌资产或明确的抽象视觉规则 |
| `sample_ingestion` | 品牌、产品和受众边界已明确，采集适配器可用 |
| `compliance_review` | 品牌、产品声明边界和企业合规规则已明确 |

关键词库或样本库为空时，可以开放基础 `content_generation`，但必须明确说明选题未经关键词或参考样本验证，不得输出虚假的样本结论或“高价值关键词”判断。

`image_plan_approval` 和 `page_quality_review` 是 `image_generation` 内部状态，不单独写入 `supported_tasks`。

`visual_profile_state` 是每次图片任务重新计算的运行状态，不写回 Profile：只有当前 Visual Profile 的视觉风格、色板、颜色比例、品牌色表现方式、面积限制、布局、品牌资产规则、禁用元素和完整技术附件均明确且已确认时，才设为 `ready`；否则设为 `incomplete` 并进入 Profile Setup Gate。

不能因为文件存在就判定 Profile 可用。字段为空、只有占位文字、证据状态不是 `confirmed` 或 `user_confirmed` 时，均不计入任务开放条件。

切换企业后，不得继续读取上一企业目录中的事实或资产。
