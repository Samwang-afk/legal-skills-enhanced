---
name: 法律文章quai味道
description: 检测并去除文章中的AI化表述模式，用于写作润色、文本优化、去AI腔。
---

> **声明**
>
> 本 Skill 基于 [pa1nrui1/legal-skills](https://github.com/pa1nrui1/legal-skills) fork 并继续开发。上游 `legal-skills` 及其原有内容继续遵循其原始 MIT License。
>
> 在此基础上，**Samwang-afk** 引入 Ludus Agent 的问题澄清与反向复核机制。Ludus Agent 为独立开发的闭源框架，其相关原创架构、实现及材料不属于上游 MIT 授权范围；对外授权部分遵循 **PolyForm Noncommercial License 1.0.0**。Ludus Agent 贡献者包括 [@xiayuzizhuo666](https://github.com/xiayuzizhuo666) 与 [@samwang-afk](https://github.com/samwang-afk)。除另有明确授权外，Ludus Agent 相关原创内容保留全部权利。
>
> 本 Skill 的输出仅作为法律工作辅助草稿，不构成正式法律意见。Agent 将尽量区分已核实事实、当事人陈述与模型推断；涉及关键事实、法规、案例或重大判断时，将优先核验现有材料，必要时提出最小必要追问，并对核心结论进行反向复核。
>
> 最终事实认定、法律适用、诉讼策略及正式法律文书，仍应由律师、法务或其他具备相应资格的专业人士复核确认。

## 法律工作总控规则（强制）

执行本 Skill 前，必须先遵循：
- skills/legal/法律工作总控/references/practice-profile.md
- skills/legal/法律工作总控/references/matter-workspace-protocol.md
- skills/legal/法律工作总控/references/document-reading-protocol.md
- skills/legal/法律工作总控/references/source-boundary-protocol.md
- skills/legal/法律工作总控/references/ocr-correction-protocol.md
- skills/legal/法律工作总控/references/pkulaw-mcp-legal-verification-protocol.md

本 Skill 只处理「法律文章quai味道」专业任务；案件隔离、事项路径、文件读取、OCR 复查、来源披露、缺口归档、法规/案例/Wiki 核验和复盘台账更新均按法律工作总控共享协议执行。

## 旧规则废止（强制）

- 旧文中直接写死的客户目录、阶段目录、旧式台账写入、旧本地读取协议均不作为执行规则。
- 事项路径、当前事项、系统记录、业务文件区和复盘台账统一以法律工作总控 `matter-workspace-protocol.md` 为准。
- 不得静默写入复盘台账；确需更新时，先确认属于复盘台账更新并向用户说明。

# De AI Polish

## 轻量入口

本文件是瘦身后的触发入口，只保留任务边界、执行顺序和按需读取索引。完整流程、模板、清单、专项规则和长示例已迁移至 `references/完整流程.md`。

## 何时使用

- 用户明确提到「法律文章quai味道」或本 Skill frontmatter 描述中的任务。
- 用户请求生成、审查、分析、计算、管理或推进与「法律文章quai味道」对应的法律工作成果。
- 法律工作总控或上游 Skill 路由到本 Skill。

## 执行顺序

1. 先按法律工作总控确认当前事项、业务文件区、系统记录区和来源边界。
2. 判断用户任务是否可以用本轻量入口完成；如只是路由、状态判断或简短提示，不默认读取完整流程。
3. 需要生成正式文书、报告、清单、计算结果、可视化、专项审查或复杂分析时，按需读取 `references/完整流程.md` 的相关章节。
4. 读取外置细节时，只读取当前任务需要的章节；不要为一个小问题整篇加载完整流程。
5. 输出前同步披露已读取材料、已核验内容、未核验/存疑内容、法规案例检索状态和需要用户判断事项。

## 按需读取索引

- `references/完整流程.md`：瘦身前完整正文，含详细流程、模板索引、专项规则、交互规范和注意事项。
- `references/`：本 Skill 的专业规则、清单、方法论和外置参考材料。
- `templates/`：文书、报告、表格等输出模板；仅在需要生成对应成果时读取。
- `assets/`、`scripts/`、`checklists/`、`reference/`：如目录存在，仅在完整流程或当前任务明确需要时读取。

## 输出底线

- 不跳过用户提供的材料；读取失败必须说明。
- 不用模型记忆替代法律法规核验；引用法规、案例、Wiki 或网页搜索时必须标注来源和核验状态。
- 材料不足时提示缺口，不悄悄补全。
- 需要写入系统记录、复盘台账、飞书文档或飞书日历时，按总控和对应飞书 Skill 规则执行。
