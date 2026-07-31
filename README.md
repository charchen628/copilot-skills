# Copilot Skills Repository
企业小红书B2B内容生产Agent仓库

## 项目简介
本仓库托管 GitHub Copilot Custom Skill：marketup-xhs-skill
专为 **B2B中大型企业** 打造的小红书全链路内容智能助手。
区别于C端种草脚本，聚焦B2B客户决策链路，围绕获客、专业信任搭建小红书内容体系。

## 技能能力概述
✅ 企业小红书账号定位、品牌人设搭建
✅ B2B行业小红书选题挖掘、关键词布局
✅ 专业向笔记撰写（干货、案例、解决方案、避坑指南）
✅ 图文文案、标题、首图文案、评论区话术生成
✅ 内容合规自检、行业话术风险审查
✅ 笔记素材库管理、案例库复用
✅ 内容标准化模板输出，适配企业团队批量生产

## 目录结构规范（Copilot Skill标准路径）
.github/skills/marketup-xhs-skill/
├─ SKILL.md # 主技能定义文件
├─ adapters/ # 格式适配、输出转换器
├─ checklists/ # 内容审核清单、合规检查项
├─ profiles/ # 品牌配置、受众画像、产品资料模板
├─ references/ # 行业参考文案、优质案例库
├─ rules/ # 写作规则、B2B 小红书运营规范
├─ schemas/ # 数据结构、输出格式定义
├─ templates/ # 各类笔记模板
└─ workflows/ # 内容生成完整工作流

## 使用方式
1. 将本Git仓库地址接入支持 GitHub Copilot Custom Skills 的平台
2. 分支选择：`main`
3. 平台自动扫描路径 `.github/skills/` 加载 marketup-xhs-skill

## 适用客户
面向B2B中大型企业，覆盖工业制造、生物医药、能源电力、人工智能大数据、芯片、软件服务、企业服务等行业。

## 备注
所有配置文件支持自定义修改：可在 `profiles/default` 录入企业产品、受众、合规要求，实现专属企业定制化输出。
