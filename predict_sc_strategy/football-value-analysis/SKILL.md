---
name: football-value-analysis
description: use this skill for structured football/soccer match research, prediction, odds-value analysis, asian handicap and total-goals settlement, same-game parlay review, live-match reassessment, betting-slip payoff math, and low-cost risk-controlled strategy design. trigger when the user asks to analyze football matches, teams, lineups, tactics, injuries, motivation, goal-difference incentives, odds, expected value, break-even probabilities, profit/loss scenarios, stake/sporttery markets, or “保本” strategy. combine football reasoning, mathematical probability, market value, and risk control. never promise profit or certain outcomes.
---

# Football Value Analysis

## Core Principle

Answer three questions separately before recommending or evaluating any selection:

1. **足球上什么最可能发生？** Analyze tactics, squad, injuries, motivation, venue, weather, match state, and previous performance.
2. **数学上赔率是否有价值？** Compare model probability with break-even probability and expected value.
3. **策略上是否改善风险收益？** Check stake sizing, correlation, repeated exposure, payoff scenarios, and downside.

Default to Chinese. Keep the tone analytical, cautious, and research-oriented. Never present betting as guaranteed profit or investment advice.

## Non-Negotiable Safety Rules

- Never use claims such as “必中”, “稳赚”, “包赢”, “稳保本”, or “无风险”.
- Explain that true保本 only exists if all outcomes are mathematically covered at guaranteed positive return. Most user plans are only “在部分比分/部分剧本下接近保本”.
- Do not encourage chasing losses, increasing stake after live swings, or heavy staking.
- Prefer “研究配置”, “模拟方案”, “理论价值”, “风险结构”, “赔率价值” rather than “买稳了”.
- If the user is emotional during live betting, prioritize “不追/等收/降低波动” when value has disappeared.

## Information Handling

When the query depends on current scores, odds, injuries, lineups, weather, or rules, use current tools/sources if available. If using screenshots or user-provided odds, state “按截图/你给的赔率计算”. If a number is uncertain, mark it as uncertain and avoid over-precision.

## Standard Workflow

### 1. Parse the Request

Identify:

- match(es), competition, kickoff time, and live minute if applicable;
- market type: 1x2, asian handicap, sporttery handicap 1x2, totals, correct score, half/full time, both teams to score, player goals, same-game parlay, or multi-leg parlay;
- odds, stake, and whether the user already placed the ticket;
- user goal: explanation, prediction, payoff calculation, value ranking, hedge/protection, live reassessment, or strategy construction.

### 2. Football Research Layer

Analyze each match through these lenses:

#### Tournament motivation

- Points, goal difference, goals scored, remaining fixtures.
- Whether a draw is useful, both sides can accept a draw, or one side must win.
- Whether goal difference matters. It matters most when a strong team needs recovery after failing to win, when third-place ranking may be relevant, or when multiple teams can finish level. It matters less when both teams already have good points and a draw helps both.

#### Team and player layer

- Formation, likely XI, bench depth, rotation risk.
- Key creators, finishers, ball-winners, center backs, fullbacks, goalkeeper.
- Injuries and suspensions mapped to probability effects:
  - missing creator: lower chance creation;
  - missing striker: lower conversion;
  - missing ball-winner: higher transition risk;
  - missing center back: opponent scoring probability up;
  - star on bench: lower early attacking intensity.

#### Tactical matchup

- Pressing vs build-up.
- Wide overloads and fullback zones.
- Low block vs favorite chance quality.
- Transition defense.
- Set-piece and aerial mismatch.
- Whether the underdog has counterattack outlets.

Typical patterns:

- Favorite vs deep block: win likely, margin uncertain.
- Two teams with 3 points: draw/small-score risk rises.
- Two teams with 0 points: game can open after the first goal.
- Strong favorite needing goal difference: deep handicap becomes more plausible, but must still pass EV math.
- Big live lead: leader may slow tempo, rotate, and protect players.

#### Previous match data

Prefer process over final score:

- xG/xGA, shots, shots on target, big chances, corners, field tilt, possession quality, red cards, game-state effects.
- A 1-0 win while being outshot may be weaker than the result.
- A 1-1 draw with higher xG and big chances can be strong evidence.
- Late goals after collapse can inflate final score.

#### Venue and climate

Consider temperature, humidity, wind, rain, altitude, turf, travel, time zone, local crowd, and kickoff time.

- Heat/humidity: lower tempo, more fatigue and late errors.
- Altitude: reduced repeated sprint capacity.
- Rain/wind: more randomness, set pieces, mistakes.
- Comfortable weather: fewer limits on tempo.

### 3. Probability and Market Math

#### Implied probability

```text
raw implied probability = 1 / odds
```

Example: odds 1.67 requires about 59.9% probability before accounting for market margin.

#### De-vigging a market

For outcomes with odds `o_i`:

```text
q_i = 1 / o_i
R = sum(q_i)
fair_probability_i = q_i / R
margin = R - 1
```

#### Expected value

```text
EV = model_probability * odds - 1
```

Interpretation:

- EV > 0: theoretical value.
- EV near 0: no clear edge.
- EV < 0: direction may be likely but price is poor.

Always separate:

```text
Likely ≠ Valuable
```

#### Break-even reference

| Odds | Break-even probability |
|---:|---:|
| 1.20 | 83.3% |
| 1.40 | 71.4% |
| 1.60 | 62.5% |
| 1.67 | 59.9% |
| 1.80 | 55.6% |
| 2.00 | 50.0% |
| 2.50 | 40.0% |
| 3.00 | 33.3% |
| 4.00 | 25.0% |

### 4. Score Model

Use a Poisson-style score model when useful:

```text
home_goals ~ Poisson(lambda_home)
away_goals ~ Poisson(lambda_away)
P(score x:y) = P_home(x) * P_away(y)
```

Build or adjust lambdas from:

- team strength/Elo/FIFA ranking;
- recent xG/xGA and shot quality;
- lineup and injury effects;
- tactical matchup;
- venue/weather;
- motivation and goal-difference incentives;
- market information;
- live score and remaining time.

Keep adjustments bounded. Example bounds:

- minor injury: 2%-5%;
- major creator/striker missing: 5%-12%;
- major defensive absence: opponent lambda +5%-15%;
- extreme climate: total lambda -3%-10%;
- goal-difference incentive: favorite attacking lambda +5%-12%, but also consider rotation and game-management risk.

### 5. Market Settlement Rules

Consult `references/market-rules.md` for detailed asian handicap, quarter-goal totals, draw-no-bet, and same-game parlay settlement. Always calculate half-win/half-loss/push correctly.

### 6. Strategy Construction

Separate tickets into three layers:

1. **Protection / lower variance:** single bets, DNB, +0.75, -1 push lines, lower totals with half-loss protection.
2. **Value exposure:** selections where model probability appears above break-even.
3. **Upside:** small parlay, same-game parlay, correct score, deep handicap.

Avoid over-concentration. Warn when the same condition appears in multiple tickets, such as Brazil -2.5 single plus Brazil -2.5 in a parlay.

### 7. Payoff and Risk Calculation

For an existing ticket set, always compute:

- total stake;
- minimum return and maximum loss;
- maximum return and maximum profit;
- key scenario returns;
- approximate probability of return >= stake;
- expected return if model probabilities are available.

Formula:

```text
profit = total_return - total_stake
```

For parlays:

```text
parlay_return = stake * product(odds_i)
```

For quarter lines, split the stake and settle each half.

### 8. Live-Match Reassessment

When live:

1. Use current minute, score, and existing user tickets.
2. Reassess tempo, substitutions, cards, pressure, xG/chances, fatigue, and team objectives.
3. Avoid emotional chasing. Often the best recommendation is “不追，等收”.
4. Explain whether a new entry is hedging or chasing.

Common live patterns:

- 4-0 at halftime: leader may slow tempo; further overs/deep handicaps may lose value.
- 0-0 after 70': full-time over becomes dangerous unless pressure is extreme.
- Favorite up by 2+ late: deeper handicap often worse than live under.
- Underdog red card early: favorite margin and over probabilities rise.

### 9. Output Format

For match analysis:

```markdown
## 结论
主线：...
最大风险：...
价值方向：...

## 足球层面
- 出线/积分/净胜球：
- 阵容与伤停：
- 战术对位：
- 上一场数据：
- 天气与场地：

## 数学层面
| 选项 | 赔率 | 盈亏平衡 | 模型概率 | EV判断 |
|---|---:|---:|---:|---|

## 策略
低风险：...
中风险：...
高回报：...

## 风险提示
这不是保本结构；若首发或赔率变化，需要重新计算。
```

For ticket evaluation:

```markdown
## 当前票据
总投入：X元

| 票 | 金额 | 条件 | 返还 |
|---|---:|---|---:|

## 收益范围
最低返还：X
最大亏损：X
最高返还：X
最大盈利：X

## 关键场景
| 场景 | 返还 | 盈亏 |
|---|---:|---:|

## 结论
主要风险集中在____。保本概率约____，不是稳赚结构。
```

### 10. Final Audit Checklist

Before finalizing, check:

- Did you separate football likelihood from odds value?
- Did you compute break-even probability for key odds?
- Did you account for market margin when appropriate?
- Did you correctly settle quarter lines?
- Did you identify correlated/repeated exposure?
- Did you explain “保本” honestly?
- Did you avoid overclaiming certainty?
- Did you mark unverified lineups/odds as uncertain?
