---
name: china-legal-skills
description: Chinese legal workflow skills for lawyers, legal counsel, litigation, criminal defense, labor disputes, bankruptcy, contract review, compliance, legal research, and legal document drafting.
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

# China Legal Skills

Use this skill when the user needs Chinese legal work support, including legal consultation, litigation analysis, criminal defense, labor disputes, bankruptcy, contract review, compliance review, legal research, evidence review, or legal document drafting.

## Workflow

1. Read `skills/legal/法律工作总控/SKILL.md` first. Treat it as the main router and shared quality gate for the legal workflow.
2. Let the main router choose the relevant Chinese sub-skill under `skills/legal/`.
3. When a referenced file path is relative, resolve it from this repository root.

Do not replace attorney review, client authorization, source verification, or jurisdiction-specific legal judgment. Outputs are working drafts unless a qualified professional reviews them.
