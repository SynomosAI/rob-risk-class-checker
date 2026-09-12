# rob-risk-class-checker

> **状态：RESERVED（占位 · 开放认领）** — 本仓已按平台协议规范建好行业接入四件套骨架，
> 等待具备本域资质的运营方认领并填充真实规则。

把「这台机器人风险几级、防护措施到不到位」拆成可核验的属性，让 AI 只做提示，不下运行结论。

## 这个域管什么

机器人系统风险等级与安全防护措施核验

机器人的风险评估、防护装置、急停功能直接关系人身安全，协作场景尤甚。AI 能做的是把风险要素与防护配置摆清楚，风险评估须由具备资质人员完成并留档。

## 域标识

| 项 | 值 |
|---|---|
| 域 ID | `rob`（全局唯一，一经分配不复用） |
| 域名称 | 机器人 · 风险等级与安全防护 |
| Profile 版本 | `domain/1.0` |
| 当前状态 | `RESERVED` |
| 占位时间 | 2026-09-12 |

## 属性清单

| 属性键 | 类型 | 说明 |
|---|---|---|
| `rob.risk_class` | enum | 风险等级，须由具备资质人员完成风险评估后填注 · 取值 low/medium/high/very_high/undetermined |
| `rob.safeguard_measure` | enum | 主要安全防护措施类型 · 取值 fixed_guard/interlocked_guard/speed_and_separation/power_and_force_limiting/none |
| `rob.emergency_stop_status` | enum | 急停功能当前状态与最近测试时间 · 取值 functional/untested/faulty/unknown |
| `rob.collaborative_operation` | boolean | 是否存在人机协同作业场景 |
| `rob.human_oversight` | enum | 人工监督强度 · 取值 none/monitored/supervised/human_decides |

## 本域红线（不可逾越，机器可读）

1. 风险等级须由具备资质人员完成风险评估并留档，AI 不得代为定级
2. 不得在未确认安全防护措施有效时输出可投入运行的表述
3. 不得建议解除、旁路或弱化安全功能（含急停、联锁、限速）

> 红线在 `gate-map.json` 中均有对应阻断规则。平台校验器会检查「每条红线都有规则覆盖」，
> 缺失即校验失败——**制度与系统不允许不同步**。

## 行业接入四件套

| 文件 | 作用 |
|---|---|
| `domain.manifest.json` | 本域声明：属性清单、签发方要求、有效期、红线 |
| `gate-map.json` | 本域「什么动作要多少摩擦」：silent / warn / confirm / block / require-owner |
| `privacy.json` | 本域隐私声明：默认关闭、最小必要、可撤回、可删除 |
| `checker` | 本域核验器（MCP 工具，**只出示核验，不下判定**） |

## 核心原则

**平台只当擂台，不当货架。** 本域的核验器只回答「这条声明是否可核验、缺什么要件」，
不回答「这件事是否合规、该不该做」。判定权在本域的资质方、监管方与人。

**隐私是准入条件，不是整改事项。** 缺失 `privacy.json` 或任一必填字段不符，
符合性校验直接失败——不是警告，是拒绝接入。

## 参考依据

- GB 11291.1 工业机器人 安全要求
- GB/T 36530 机器人与机器人装备 协作机器人（参照）
- ISO 10218（参照）

> 上列依据仅用于说明本域属性的来源与口径，不构成法律意见。具体适用以现行有效文本与主管部门解释为准。

## 认领方式

本域面向具备相应资质的机构开放。认领后请：

1. Fork 本仓，填注 `operator` 与 `checker_endpoint`
2. 按本域现行有效规则校准属性取值与红线表述
3. 跑平台侧校验器自测（五项判据全过方可提交）
4. 提 PR，附资质证明与规则依据

## 许可与署名

代码与配置按 MIT 许可使用。文档的知识版权归 SynomosAI 所有。

© 2026 SynomosAI. All rights reserved.
