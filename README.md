"# predict_sc_strategy"  
# Football Value Analysis Skill / 足球价值分析 Skill

## 中文介绍

`football-value-analysis` 是一个面向足球比赛研究、赔率价值判断、盘口策略评估和实时比赛决策辅助的 ChatGPT Skill。它的目标不是简单给出“买谁”或“预测比分”，而是用一套更系统的方法，把**足球基本面分析、数学概率建模、赔率价值判断、盘口结算规则和风险控制**结合起来，帮助用户更理性地理解一场比赛、一个盘口或一组投注方案的风险收益结构。

该 Skill 特别适合用于世界杯、欧洲杯、联赛、杯赛等足球赛事的赛前分析、临场复盘、盘口解释、投注单收益计算、同场复式评估、亚洲让球/大小球结算、正确比分概率分析，以及多场串关的风险拆解。

它强调一个核心原则：

> 足球上最可能发生的事情，不一定是赔率上最值得选择的事情。

因此，该 Skill 会始终区分三件事：

1. **足球层面：什么结果最可能发生？**
2. **数学层面：这个概率是否超过赔率要求的盈亏平衡点？**
3. **策略层面：这个选择是否改善整体风险/收益结构？**

---

## 核心能力

### 1. 足球基本面分析

该 Skill 会从足球研究员的角度分析比赛，包括：

* 球队实力与风格
* 阵型与战术对位
* 首发阵容与替补深度
* 核心球员作用
* 伤停、停赛和轮换影响
* 前场创造力、终结能力、防线稳定性
* 边路对位、中场控制、反击空间
* 定位球、高空球、身体对抗
* 门将质量和后场出球
* 近期比赛内容，而不仅仅是比分结果

例如，一支球队虽然上一场赢了，但如果射门、控球、xG、机会质量都落后，那么 Skill 会提醒用户：这个胜利可能并不稳定。反过来，一支球队虽然只打平，但如果过程数据明显占优，Skill 会把这种“过程优势”纳入分析。

---

### 2. 小组形势与比赛动机判断

在世界杯或小组赛环境中，Skill 会特别分析：

* 当前积分
* 净胜球
* 进球数
* 剩余赛程
* 是否必须赢球
* 平局是否可以接受
* 是否存在“默契平局”或“保平争胜”剧本
* 是否有刷净胜球动力
* 第三名出线规则对比赛节奏的影响

Skill 不会简单认为“强队一定会猛攻”或“需要净胜球就一定大胜”，而是会结合比赛阶段、对手防守方式、体能消耗和盘口价格一起判断。

例如：

* 两队都已经有 3 分时，平局可能对双方都可以接受；
* 强队首轮未赢、第二轮面对弱队时，刷净胜球动力更强；
* 0 分球队之间交手时，比赛可能更开放；
* 小组赛最后阶段，领先方可能更重视控节奏和避免受伤。

---

### 3. 阵容与球员影响分析

该 Skill 会将球员作用映射到比赛概率，而不是只看名气。

它会关注：

* 组织核心是否首发
* 爆点边锋是否在场
* 中锋是支点型、抢点型还是反击型
* 后腰是否能保护防线
* 中卫是否怕速度
* 边后卫是否压上过深
* 门将是否稳定
* 替补席是否有改变比赛的球员

例如：

* 创造型中场缺阵，会降低球队破密集防守能力；
* 主力中卫缺阵，会提高对手反击和定位球进球概率；
* 边锋首发，会提高边路突破、造点、传中和反击威胁；
* 领先后核心被换下，后续进球概率可能下降。

---

### 4. 气候、场地与时间因素

Skill 会考虑比赛环境，包括：

* 温度
* 湿度
* 降雨
* 风速
* 高海拔
* 草皮条件
* 当地时间
* 旅途与时差
* 主场观众
* 球队对环境的适应程度

这些因素会影响比赛节奏、体能下降、传球质量、冲刺强度和下半场失误概率。

例如：

* 高温高湿可能降低节奏；
* 高海拔可能降低持续冲刺能力；
* 雨战可能增加随机性和定位球价值；
* 舒适天气更有利于技术型球队发挥。

---

## 数学与赔率分析

### 1. 隐含概率与盈亏平衡

Skill 会把赔率转化为隐含概率：

```text
隐含概率 = 1 / 赔率
```

例如：

```text
赔率 1.67 → 1 / 1.67 ≈ 59.9%
```

这意味着，只有当模型认为该选项真实命中率高于约 59.9% 时，它才可能具备理论价值。

这一步可以避免常见误区：

> “这个结果很可能发生” 不等于 “这个赔率值得选择”。

---

### 2. 去水概率与市场边际

对于胜平负、大小球、让球等市场，Skill 会估算庄家抽水：

```text
q_i = 1 / odds_i
R = Σ q_i
market margin = R - 1
fair probability_i = q_i / R
```

通过去水处理，可以更接近市场真实概率，再与模型概率比较。

---

### 3. 期望值 EV 判断

Skill 会用以下公式判断理论价值：

```text
EV = 模型概率 × 赔率 - 1
```

判断逻辑：

* `EV > 0`：有理论价值
* `EV ≈ 0`：接近公平盘
* `EV < 0`：方向可能对，但赔率不够好

这可以帮助用户避免只看强弱，不看赔率价格。

---

### 4. 泊松比分模型

Skill 支持用泊松思路估算比分分布：

```text
主队进球 ~ Poisson(lambda_home)
客队进球 ~ Poisson(lambda_away)
```

再从比分矩阵映射到：

* 胜平负
* 亚洲让球
* 总进球大小球
* 正确比分
* 双方进球
* 净胜球
* 球队进球数
* 同场复式条件

例如，若模型认为巴西进球均值为 2.8，海地进球均值为 0.4，则会进一步分析：

* 巴西胜概率
* 巴西赢 3 球以上概率
* 3:0、4:0、3:1 等比分概率
* 巴西 -2.5 是否有价值
* 巴西 & 否是否比让球盘更稳

---

## 盘口解释与结算

该 Skill 内置常见足球盘口解释，包括：

### 亚洲让球

* `+0.75`
* `-0.75`
* `-1`
* `-1.25`
* `-1.5`
* `-2`
* `-2.25`
* `-2.5`
* `-2.75`
* `-3`

例如：

```text
巴西 -2.5
```

表示巴西必须赢 3 球或以上才算赢。

| 比分  | 巴西 -2.5 |
| --- | ------- |
| 2:0 | 输       |
| 3:0 | 赢       |
| 4:0 | 赢       |
| 3:1 | 输       |
| 4:1 | 赢       |

---

### 亚洲大小球

支持解释：

* 大/小 1.5
* 大/小 2.25
* 大/小 2.5
* 大/小 2.75
* 大/小 3.75
* 大/小 4.5

例如：

```text
大2.25 = 一半大2.0 + 一半大2.5
```

|  总进球 | 大2.25 |
| ---: | ----- |
| 0-1球 | 全输    |
| 正好2球 | 输半    |
| 3球以上 | 全赢    |

---

### 平局退款 / Draw No Bet

```text
球队赢 → 赢
平局 → 退本金
球队输 → 输
```

---

### “球队 & 是/否”

例如：

```text
巴西 & 否
```

表示：

> 巴西赢，并且对手不进球。

能中的比分包括：

```text
1:0, 2:0, 3:0, 4:0...
```

---

### 同场复式 / Same Game Parlay

Skill 会分析同场复式的真实含义和风险。

例如：

```text
加拿大胜 + 大1.5
```

命中比分：

```text
2:0, 2:1, 3:0, 3:1...
```

不命中比分：

```text
1:0, 1:1, 0:0, 0:1...
```

Skill 会提醒用户：同场复式会提高赔率，但会缩小命中比分范围，不是保本工具。

---

## 策略设计方法

该 Skill 通常把策略拆成三层：

### 1. 主仓保护

选择更稳的方向，例如：

* 平局退款
* 亚洲盘带走水
* 小球保护
* +0.75 受让
* -1 让球盘

### 2. 价值仓

选择模型概率可能高于赔率要求的盘口，例如：

* 大2.25
* 小3.75
* 某队 -2
* 某队胜 & 否
* 某队不败
* 某队进球数

### 3. 小额冲高

选择高赔率但高波动方向，例如：

* 正确比分
* 进球球员
* 3串1
* 同场复式
* 净胜球比分
* 谁进第N球

这种结构可以避免所有资金都压在单一剧本上。

---

## 收益与风险计算

Skill 可以对用户已有投注单计算：

* 总投入
* 最坏情况
* 最大盈利
* 当前命中状态
* 仍未确定的票
* 哪些比分最有利
* 哪些比分最危险
* 保本概率估计
* 期望返还
* 期望利润

例如：

```text
总投入：5.5元
最大返还：14.23元
最大盈利：8.73元
最坏亏损：-5.5元
主要风险：巴西只赢2球、海地进球、土巴正好低比分
```

Skill 会用场景表说明不同比分下的收益变化。

---

## 临场分析能力

该 Skill 适合实时比赛分析，例如：

* 72分钟 3:0 是否还要追大球？
* 半场 4:0 是否继续买强队让球？
* 82分钟 0:1 是否买小球？
* 当前票哪些已经确定盈利？
* 球员进球/助攻是否结算？
* 正确比分是否要对冲？
* 是否该买双方进球作为保险？

临场分析会重点考虑：

* 当前比分
* 比赛分钟
* 剩余时间
* 换人
* 黄牌/红牌
* 控球和射门数据
* 领先方是否降速
* 落后方是否有进攻质量
* 当前盘口是否已经失去价值

例如：

> 半场 3:0 时，Skill 通常不会建议继续追深盘，而是判断是否应该保护已有利润，或者小额防 3:1 这种伤害最大的彩票情境。

---

## 风险控制原则

该 Skill 的所有输出都遵守以下原则：

* 不承诺盈利
* 不鼓励重仓
* 不鼓励追损
* 不把投注当投资建议
* 不使用“稳赢”“包中”等表达
* 明确区分“方向正确”和“赔率有价值”
* 明确提示重复暴露风险
* 强调赔率变化、阵容变化和临场状态会改变判断

核心风险提示：

> 本 Skill 仅用于足球比赛研究、概率建模和赔率结构分析，不构成任何投注建议或财务建议。足球比赛具有高度不确定性，任何策略都可能亏损。

---

## 示例使用场景

### 赛前分析

```text
分析一下巴西 vs 海地，从阵容、战术、出线形势、赔率价值和大小球角度判断。
```

### 盘口解释

```text
大2.25是什么意思？如果我投4元，进2球和3球分别怎么结算？
```

### 收益计算

```text
我买了巴西-2.5 1.5元、巴西&否2元、正确比分3:0 1元，现在半场3:0，哪些已经盈利？最大收益和风险是什么？
```

### 临场策略

```text
现在72分钟巴西3:0海地，还能怎么买？要不要防3:1？
```

### 组合评估

```text
我有一个3串1，加上几个单关，帮我算最低亏损、最大盈利、保本概率和最危险比分。
```

---

# English Introduction

`football-value-analysis` is a ChatGPT Skill designed for structured football/soccer match research, prediction, odds-value analysis, live-match reassessment, and betting-slip risk evaluation. It does not simply output a pick or a score prediction. Instead, it combines **football analysis, probability modeling, market valuation, Asian handicap settlement, totals settlement, scenario analysis, and risk control** into one repeatable workflow.

The core idea is:

> The most likely football outcome is not always the most valuable market price.

This Skill separates three questions:

1. **Football question:** What is most likely to happen on the pitch?
2. **Mathematical question:** Does the estimated probability beat the break-even probability implied by the odds?
3. **Strategy question:** Does this selection improve the overall risk/reward structure?

---

## Key Capabilities

### Football Research

The Skill evaluates matches from a football analyst’s perspective, including:

* Team strength
* Formations and tactical matchups
* Starting lineups and bench depth
* Player roles and impact
* Injuries and suspensions
* Recent match data
* xG, shots, big chances, corners, and game state
* Pressing, transitions, set pieces, and defensive weaknesses
* Motivation, group standings, and qualification scenarios
* Weather, venue, travel, altitude, and kickoff time

It prioritizes performance data over final score alone. A narrow win with poor underlying numbers may be treated as unstable, while a draw with strong xG and chance creation may be treated as a positive performance signal.

---

### Mathematical Odds Analysis

The Skill converts decimal odds into implied probability:

```text
implied probability = 1 / odds
```

For example:

```text
odds 1.67 → 1 / 1.67 ≈ 59.9%
```

That means a selection must win more than roughly 59.9% of the time to be profitable before market margin adjustments.

It also supports expected value analysis:

```text
EV = model probability × odds - 1
```

This allows the Skill to distinguish between:

* a likely outcome;
* a fairly priced outcome;
* an overpriced favorite;
* a true value opportunity.

---

### Poisson-Based Score Modeling

The Skill can use a Poisson-style framework:

```text
Home goals ~ Poisson(lambda_home)
Away goals ~ Poisson(lambda_away)
```

It then maps score probabilities to:

* 1X2 markets
* Asian handicaps
* total goals
* correct score
* both teams to score
* team totals
* winning margin
* same-game parlay conditions

This is useful for evaluating markets such as:

* Brazil -2.5
* Over 2.25
* Under 3.75
* Brazil & No
* Correct score 3:0 / 4:0
* Team to score next
* Player goal or assist markets

---

## Market Settlement Support

The Skill explains and calculates common football markets, including:

### Asian Handicap

Example:

```text
Brazil -2.5
```

Brazil must win by 3 or more goals.

| Final Score | Brazil -2.5 |
| ----------- | ----------- |
| 2-0         | Lose        |
| 3-0         | Win         |
| 4-0         | Win         |
| 3-1         | Lose        |
| 4-1         | Win         |

---

### Asian Total Goals

Example:

```text
Over 2.25 = 50% Over 2.0 + 50% Over 2.5
```

| Total Goals | Over 2.25 |
| ----------: | --------- |
|         0-1 | Full loss |
|   exactly 2 | Half loss |
|          3+ | Full win  |

---

### Draw No Bet

```text
Selected team wins → win
Draw → stake refunded
Selected team loses → loss
```

---

### Team & Yes/No

Example:

```text
Brazil & No
```

This means:

> Brazil wins and the opponent does not score.

Winning scores include:

```text
1-0, 2-0, 3-0, 4-0...
```

---

### Same-Game Parlays

The Skill evaluates same-game parlays by identifying which score ranges they actually cover.

Example:

```text
Canada win + Over 1.5
```

Winning scores:

```text
2-0, 2-1, 3-0, 3-1...
```

Losing scores:

```text
1-0, 1-1, 0-0, 0-1...
```

The Skill highlights that same-game parlays increase payout but narrow the winning scenario space.

---

## Strategy Framework

The Skill organizes strategies into three layers:

### 1. Core Protection

Lower-volatility selections such as:

* Draw No Bet
* Asian handicap with push protection
* +0.75 underdog handicap
* Under totals
* Favorite -1 instead of -1.5
* Team win & clean sheet protection

### 2. Value Exposure

Markets where the model probability may exceed the break-even requirement, such as:

* Over 2.25
* Under 3.75
* Favorite -2
* Favorite & No
* Team total goals
* BTTS No / Yes when supported by tactics

### 3. Upside Tickets

Small high-variance positions such as:

* Correct score
* Player goal
* Multi-leg parlay
* Same-game parlay
* Winning margin
* Next goal scorer

The Skill discourages over-concentrating on the same condition across multiple tickets.

---

## Live Match Analysis

The Skill is especially useful for in-play situations.

It can evaluate:

* current score
* minute
* substitutions
* cards
* possession
* shots
* expected match state
* whether the leader will slow down
* whether the trailing team has enough attacking quality
* whether a live market still has value

Examples:

* At halftime 3-0, should the user chase more goals?
* At 72 minutes 3-0, should the user hedge against 3-1?
* At 82 minutes 0-1, should the user buy under 2.5 or the next goal?
* Which tickets are already effectively settled?
* Which final score is the most dangerous for the current portfolio?

---

## Payoff and Risk Evaluation

The Skill can calculate:

* total stake
* maximum return
* maximum profit
* worst-case loss
* break-even scenarios
* expected return
* probability of profit
* currently winning tickets
* tickets still at risk
* most favorable final scores
* most dangerous final scores

Example output:

```text
Total stake: 5.5
Maximum return: 14.23
Maximum profit: 8.73
Worst-case loss: -5.5
Main risk: Brazil wins by only 2, Haiti scores, or the total lands below the parlay threshold.
```

---

## Important Risk Disclaimer

This Skill is for football research, probability modeling, and market-structure analysis only. It does not provide guaranteed outcomes, financial advice, or betting advice. Football is highly uncertain, and any strategy can lose. The Skill never treats betting as investment, never promises profit, and always emphasizes risk control.

---

## Example Prompts

```text
Analyze Brazil vs Haiti using lineups, tactical matchup, motivation, weather, odds, and expected value.
```

```text
What does Over 2.25 mean? If I stake 4 units, how is it settled at 2 goals or 3 goals?
```

```text
I have Brazil -2.5, Brazil & No, correct score 3-0, and Vinicius goal/assist. It is halftime 3-0. Which tickets are already safe, and what final score hurts me most?
```

```text
It is 72 minutes and Brazil leads 3-0. Should I hedge against 3-1 or avoid chasing?
```

```text
Evaluate this parlay and calculate maximum profit, minimum loss, break-even probability, and the most dangerous match scenario.
```

---

## Philosophy

A good football value analysis should never stop at “who is stronger.”

It should answer:

```text
What is likely?
What is priced correctly?
What is mispriced?
What is the downside?
What happens under alternative score scenarios?
```

`football-value-analysis` exists to make that process repeatable, transparent, and disciplined.


可以。这里要分清楚两个概念：

1. **ChatGPT Skill**：像你刚才这个 `football-value-analysis/SKILL.md`，可以作为 ChatGPT Skills 的可上传 Skill 包。
2. **Codex / Claude Code / Cursor / Copilot Coding Agent 的项目指令**：通常是放在仓库里的 `AGENTS.md`、`CLAUDE.md`、`.cursor/rules` 等文件，让代码代理在这个仓库里自动读取。

所以你的这个足球分析 Skill 可以同时做两种导入方式。

---

## 方式一：导入 ChatGPT Skills

这个用你已经打包好的：

```text
skill.zip
```

一般流程是：

1. 打开 ChatGPT 的 Skills 页面或 Skill library。
2. 选择创建/上传 Skill。
3. 上传 `skill.zip`。
4. 系统会读取里面的 `SKILL.md`。
5. 之后你问足球赔率、盘口、收益计算、临场策略时，它就会自动触发。

适合场景：

```text
平时和 ChatGPT 对话分析比赛、赔率、盘口、收益。
```

---

## 方式二：导入 Codex

Codex 更像代码代理，它通常不是直接“安装 ChatGPT Skill”，而是读取仓库里的项目说明文件。常见做法是在仓库根目录放一个：

```text
AGENTS.md
```

然后把你的 Skill 精简转换成 Codex 能读的项目指令。

推荐结构：

```text
predict_sc_strategy/
├── README.md
├── AGENTS.md
├── football-value-analysis/
│   └── SKILL.md
└── skill.zip
```

### AGENTS.md 示例

你可以在仓库根目录新建：

```markdown
# AGENTS.md

## Project Purpose

This repository contains a football value-analysis skill and methodology for analyzing soccer matches, betting markets, Asian handicaps, totals, live-match scenarios, expected value, and payoff structures.

## Main Instruction

When working on this repository, read:

- `football-value-analysis/SKILL.md`

Use it as the authoritative methodology for football match analysis, odds value analysis, ticket payoff calculations, and strategy construction.

## Core Rules

- Do not present any prediction as guaranteed.
- Do not use language such as “sure win,” “guaranteed profit,” or “risk-free.”
- Always separate:
  1. football likelihood,
  2. mathematical value,
  3. strategy risk/reward.
- Always calculate implied probability and break-even probability when odds are available.
- Always explain Asian handicap and total-goal settlement clearly.
- Always warn when the same risk is repeated across multiple tickets.
- For live matches, consider score, minute, substitutions, cards, game state, and whether the market still has value.

## Output Style

Use Chinese by default unless the user asks for English.

Prefer structured output:

1. Short conclusion
2. Football analysis
3. Mathematical/odds analysis
4. Strategy table
5. Payoff scenario table
6. Risk statement
```

然后在 Codex 里使用时，你可以让它：

```text
Read AGENTS.md and football-value-analysis/SKILL.md, then help me improve the strategy engine or write examples.
```

Codex 这类 coding agent 通常会读取仓库上下文和项目级说明文件；社区和研究里也常见 `AGENTS.md` 作为 coding agent 的仓库级配置文件，Claude Code 则更常见 `CLAUDE.md`。([arXiv][1])

---

## 方式三：导入 Claude Code

Claude Code 最常见的是在项目根目录放：

```text
CLAUDE.md
```

Claude Code 会把它当作项目工作指令。你可以把 `AGENTS.md` 的内容复制一份，改名为：

```text
CLAUDE.md
```

推荐仓库结构：

```text
predict_sc_strategy/
├── README.md
├── CLAUDE.md
├── AGENTS.md
├── football-value-analysis/
│   └── SKILL.md
└── skill.zip
```

### CLAUDE.md 示例

```markdown
# CLAUDE.md

## Repository Context

This repository stores a football value-analysis methodology and reusable AI skill.

The main methodology file is:

- `football-value-analysis/SKILL.md`

Before answering football analysis, odds strategy, Asian handicap, totals, live-match, or betting-slip evaluation tasks, read and follow that file.

## Required Reasoning Framework

For every football strategy analysis:

1. Analyze the football context:
   - lineups
   - tactics
   - motivation
   - previous match data
   - weather and venue
   - live score if relevant

2. Analyze the mathematics:
   - implied probability
   - break-even probability
   - expected value
   - Poisson-style score distribution when useful
   - Asian handicap or total-goal settlement

3. Analyze risk:
   - worst-case loss
   - maximum return
   - key dangerous scores
   - repeated exposure
   - whether the user is chasing

4. Give a strategy:
   - core protection
   - value exposure
   - small upside ticket
   - final risk warning

## Style

Respond in Chinese by default.

Never say:
- guaranteed win
- sure profit
- risk-free
- must buy
- all-in

Use:
- research direction
- simulated allocation
- theoretical value
- risk structure
- cannot guarantee profit
```

Claude Code 使用 Markdown 项目指令文件是常见模式，相关文献和资料也把 `CLAUDE.md` / `AGENTS.md` 作为 coding agent 的配置上下文来讨论。([arXiv][2])

---

## 方式四：导入 Cursor

Cursor 一般可以用 `.cursor/rules` 或项目规则。

推荐：

```text
predict_sc_strategy/
├── .cursor/
│   └── rules/
│       └── football-value-analysis.mdc
├── football-value-analysis/
│   └── SKILL.md
```

`football-value-analysis.mdc` 可以这样写：

```markdown
---
description: Football value analysis methodology for soccer match prediction, odds value, Asian handicap, totals, live match strategy, and ticket payoff evaluation.
alwaysApply: true
---

Use `football-value-analysis/SKILL.md` as the main methodology.

When analyzing football matches or betting strategies:

- separate football likelihood from odds value;
- calculate implied probability when odds are available;
- explain Asian handicap and total-goal settlement;
- calculate profit/loss scenarios for tickets;
- avoid guaranteed-profit language;
- use Chinese by default.
```

---

## 方式五：导入 Claude Project / 普通 Claude Chat

如果不是 Claude Code，而是网页 Claude 项目：

1. 建一个 Claude Project。
2. 上传：

   * `README.md`
   * `football-value-analysis/SKILL.md`
3. 在 Project Instructions 里写：

```text
Use the uploaded football-value-analysis/SKILL.md as the required methodology for all soccer match analysis, odds-value analysis, live-match decisions, Asian handicap settlement, total-goal settlement, and payoff calculations. Respond in Chinese by default. Never promise guaranteed profit.
```

这样 Claude 在该 Project 里就会按这套方法回答。

---

## 我建议你仓库里同时放这几个文件

最通用的结构是：

```text
predict_sc_strategy/
├── README.md
├── AGENTS.md
├── CLAUDE.md
├── football-value-analysis/
│   └── SKILL.md
└── skill.zip
```

含义：

| 文件                                 | 用途                         |
| ---------------------------------- | -------------------------- |
| `README.md`                        | 给人看的仓库说明                   |
| `AGENTS.md`                        | Codex / 通用 coding agent 指令 |
| `CLAUDE.md`                        | Claude Code 项目指令           |
| `football-value-analysis/SKILL.md` | ChatGPT Skill 核心文件         |
| `skill.zip`                        | 可上传到 ChatGPT Skills 的打包文件  |

---

## 最推荐的做法

你这个项目我建议这样处理：

1. `football-value-analysis/SKILL.md` 保留完整版本。
2. `README.md` 放中英文介绍。
3. `AGENTS.md` 写给 Codex / 通用 coding agent。
4. `CLAUDE.md` 写给 Claude Code。
5. `skill.zip` 用于 ChatGPT Skill 上传。

这样同一套方法可以同时用于：

```text
ChatGPT Skills
Codex
Claude Code
Claude Project
Cursor
其他 coding agents
```

一句话：

> **ChatGPT 用 skill.zip；Codex 用 AGENTS.md；Claude Code 用 CLAUDE.md；Cursor 用 .cursor/rules；Claude Project 直接上传 SKILL.md 并写入 Project Instructions。**

[1]: https://arxiv.org/abs/2601.20404?utm_source=chatgpt.com "On the Impact of AGENTS.md Files on the Efficiency of AI Coding Agents"
[2]: https://arxiv.org/abs/2509.14744?utm_source=chatgpt.com "On the Use of Agentic Coding Manifests: An Empirical Study of Claude Code"
