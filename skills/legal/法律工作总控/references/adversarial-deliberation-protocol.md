# 对抗审议协议

仅对 L2/L3 强制。第一阶段不要求启动多个模型，可以由同一个 Agent 执行严格角色隔离；关键是 Advocate 与 Challenger 的任务定义必须不同，不能只是"分析两遍"。

可执行参照实现：`skills/legal/法律工作总控/scripts/reasoning_control.py challenge-check` 和 `judge`。

## 一、角色定义

### Advocate

任务：在已知事实、证据和已核验法律来源边界内，为当前候选结论构建 strongest case。

必须逐项回答：

- 当前结论是什么？
- 依赖哪些法律规则（必须已核验）？
- 依赖哪些法律要件？
- 每个要件由什么事实支持？每条事实是什么认知状态？
- 每个 ESTABLISHED 事实由什么证据支持？
- 哪些只是当事人陈述？哪些是推断？哪些环节仍然薄弱？

禁止：隐藏不利事实；把未知写成已知；虚构证据、案例、法条；为了"赢"跨越来源边界。

### Challenger

任务：尝试 falsify Advocate 的结论。不是再分析一次。

必须主动检查：

1. 最强相反事实解释；
2. 最强对方抗辩；
3. 缺失法律要件；
4. 举证责任失败；
5. 不利证据；
6. 证据真实性/证明力问题；
7. 相反法律规则；
8. 不利案例；
9. 相反裁判思路；
10. 程序障碍；
11. 时效；
12. 管辖；
13. 主体资格；
14. 当前分析依赖的隐藏假设；
15. 能使结论失败的最小条件集合。

禁止这种低价值反驳：

```text
"仍存在一定风险"
"法院可能有不同观点"
"结果存在不确定性"
```

必须指出**具体失败机制**：在哪个要件、因为哪个证据或哪个法条、以什么方式导致结论不成立。

## 二、Minimum Failure Set

Challenger 必须回答：使当前结论不成立所需要否定、改变或无法证明的最小条件是什么？

```yaml
failure_conditions:
  - id: FC-001
    condition: 无法证明借款合意
    type: fact            # fact | evidence | law | procedure
    current_support: 仅有转账记录
    weakness: 转账本身无法必然证明款项性质
    impact: fatal         # low | medium | high | fatal
    consequence: 民间借贷关系不成立，诉请基础丧失
    mitigation:           # 可空
    needed: 借条 / 还款承诺 / 明确借款聊天 / 部分还款行为
```

无实质争议时如实说明：

```text
未发现有实质分量的竞争性法律解释
```

不得为了制造"正反双方"而虚构不存在的争议。

注：`reasoning_control.py challenge-check` 用正则拦截常见泛化表述（如"存在风险""结果不确定"），只是机器启发式；Challenger 的实质要求是：condition 必须能指明是哪一要件、哪一证据或哪一法条导致结论不成立，不得因通过脚本校验而放松实质检查。

## 三、L3 的反向检索

L3 中，Advocate 与 Challenger 的检索方向必须区别（沿用 `法规案例检索` 与 `pkulaw-mcp-legal-verification-protocol.md`，不新建检索工具）：

- Advocate：寻找支持当前路径的法律规则和裁判。
- Challenger：寻找不利案例、反向法律解释、不同裁判路径、关键例外、法条适用边界。

检索结果必须进入来源边界；Challenger 测试 hypothetical 时必须显式标识 `Hypothetical`，不得加入 established facts。

## 四、防止 Confirmation Bias

已形成初步结论时，Challenger 必须在不承担"维护初步结论"任务的情况下，以推翻该结论为任务。

```text
Advocate → strongest support
Challenger → strongest falsification
Judge → comparison
```

禁止：

```text
初步结论 → 找理由证明初步结论 → 再假装反思
```

## 五、输出

L3 审议结果写入系统记录区 `推理记录/deliberation.md`，至少包含：

- Advocate 论证（结论、规则、要件、事实、证据、弱点）；
- Challenger 逐项检查结果（15 项中每一项的结论：成立 / 不成立 / 无法检验）；
- failure_conditions 列表；
- 未解决的竞争性解释；
- residual uncertainty 说明。
