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
- market type: 1x2, asian handicap, sporttery handicap 1x2, totals, correct score, half/full time, both teams to score, player goals, player assists, player shots, player cards, corners, same-game parlay, or multi-leg parlay;
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
- Underdog red card early: favorite margin and over probabilities may rise, but only if chance quality also improves.
- Trailing favorite with high possession but no shots on target: do not overrate the comeback.
- Late live betting after repeated failed attacks: avoid chasing unless the odds compensate for the risk.
- Late strong-team pressure with fresh attackers, rising shots on target, many corners, and tired defenders can justify a small high-variance over/next-goal entry if price is high enough.

#### Red Card Live-Adjustment Rule

When a red card occurs, do not automatically treat it as a strong reason to chase goals, overs, or the team with the numerical advantage. A red card changes the match state, but its betting value depends on whether the numerical advantage creates real chance quality.

##### Core principle

```text
Red card is an adjustment factor, not a guarantee of goals.
```

A team being one man up may dominate possession without creating enough shots, shots on target, box entries, or high-quality chances. Do not convert “11 vs 10” directly into “the stronger team will score.”

##### Red card evaluation checklist

After a red card, check these factors before recommending any live strategy:

1. **Time of the red card**
   - Early red card: bigger impact.
   - Red card near halftime: defending team can reorganize at halftime.
   - Late red card: less time for the numerical advantage to matter.

2. **Scoreline**
   - If the team with 10 men is already leading, they may drop into a compact low block.
   - If the team with 10 men is trailing, the match may become chaotic, but not always high-scoring.
   - If the match is level, the team with 10 men may accept a draw.

3. **Chance quality after the red card**
   Look for:
   - shots on target increasing;
   - box touches increasing;
   - repeated corners;
   - dangerous free kicks;
   - defensive clearances under pressure;
   - goalkeeper saves;
   - blocked shots inside the box;
   - visible defensive disorganization.

   If the team with 11 men only has sterile possession, do not overrate its goal probability.

4. **Defending team profile**
   Some teams are built to survive with 10 men:
   - strong center-backs;
   - compact low block;
   - good aerial defense;
   - physical midfield;
   - disciplined defensive shape;
   - good goalkeeper;
   - counterattacking outlet.

5. **Attacking team profile**
   A team with numerical advantage still needs:
   - creative midfielders;
   - wide overloads;
   - box presence;
   - good crossing quality;
   - second-ball pressure;
   - set-piece quality;
   - finishing ability.

6. **Market price after the red card**
   Red-card markets often move fast. If the price collapses too much, the value may disappear even if the direction is logically correct.

##### Red card live strategy ranking

If the trailing team is one man up, prefer safer structures first:

```text
1. Team to score / BTTS Yes
2. Next goal by the team with 11 men
3. Team +0.5 / Team not to lose
4. Moderate over line
5. Full comeback win
```

Do not jump directly to the comeback win unless the attacking quality is clearly high and the odds still justify the risk.

##### Red card over/under guidance

A red card can increase or decrease goal probability depending on game state.

Red card can support overs when:

```text
- the trailing team has the extra man;
- shots and box entries increase quickly;
- the defending team cannot clear pressure;
- corners/free kicks are piling up;
- the match still has enough time;
- both teams still have transition threat.
```

Red card does not support overs when:

```text
- the team with 10 men leads and sits in a deep block;
- the team with 11 men has sterile possession;
- there are few shots on target;
- the attacking team lacks a box striker;
- the referee stops the rhythm frequently;
- the market has already over-adjusted.
```

##### Live probability adjustment

Do not blindly add a large fixed boost after a red card.

Suggested adjustment logic:

```text
If red card + real pressure:
    increase attacking goal expectation significantly.

If red card + only possession:
    increase attacking goal expectation slightly.

If red card + defending team is compact and comfortable:
    avoid aggressive overreaction.

If 10-15 minutes after red card there is no shot-quality improvement:
    downgrade the red-card effect.
```

##### Wrong vs correct red-card reasoning

Wrong:

```text
Team A is down 0:1 but has one extra player, so Team A will probably score.
```

Correct:

```text
Team A is down 0:1 and has one extra player, which increases its attacking opportunity. However, if Team A still has few shots on target and Team B is defending compactly, the value of chasing Team A goal or Over may be limited.
```

##### Practical live rule

After a red card, wait for a short confirmation window when possible:

```text
5-10 minutes after red card:
- Are shots increasing?
- Are corners increasing?
- Is the defending team pinned inside its box?
- Is the goalkeeper being tested?
- Are dangerous central zones being reached?
```

If the answer is no, do not chase simply because of the red card.


#### Late Pressure + Substitution Momentum Rule

In late-match situations, do not automatically downgrade overs or next-goal markets only because the match is near the end. Time remaining is important, but late pressure can create high-value goal entries when the market overprices the clock and underprices momentum.

##### Core principle

```text
Late overs are not bad by default. They become valuable only when pressure quality, substitution impact, and defensive fatigue all point in the same direction.
```

A late over or next-goal selection can be justified when the attacking team is not merely holding possession, but has created repeated high-pressure actions and has improved its box presence through substitutions.

##### Late pressure confirmation checklist

Before recommending a late over, next goal, or comeback entry after 70', check:

1. **Shot quality trend**
   - Are shots on target increasing compared with earlier phases?
   - Is the goalkeeper being tested?
   - Are blocked shots happening inside the box rather than from harmless distance?

2. **Set-piece and second-ball pressure**
   - Are corners piling up?
   - Are dangerous free kicks and long throws increasing?
   - Is the attacking team winning second balls after crosses and clearances?

3. **Substitution momentum**
   - Did the attacking team bring on a true striker, box runner, or fresh wide creator?
   - Has a substitute already scored, assisted, or created a big chance?
   - Did the substitution change the attack from sterile possession to direct box threat?

4. **Defensive fatigue and defensive rotation**
   - Has the defending team kept the same center-backs or fullbacks under pressure for a long time?
   - Did the defending team mostly substitute forwards or midfielders instead of refreshing the back line?
   - Are defenders losing aerial duels, second balls, or markers?
   - Are clearances becoming shorter or more panicked?

5. **Game-state incentives**
   - Does one team still strongly prefer a win rather than a draw?
   - Would the defending team accept a draw but still leave counterattacking outlets?
   - Is the match script creating two-way danger rather than one-way sterile pressure?

6. **Price check**
   - Late overs and next-goal prices can become attractive only if the odds compensate for the clock.
   - If the price is too low, do not chase even when pressure exists.

##### Upgrade late goal probability when these signals align

Upgrade the chance of another goal when several of these are true:

```text
- strong team has recently equalized or scored;
- substitute striker/attacker has already made impact;
- corners are high and still increasing;
- shots on target are rising late;
- defending back line is tired and not refreshed;
- attacking team is repeatedly entering the box;
- match still has stoppage time and emotional momentum;
- the price on Over/next goal is 2.80-3.20+ and only one goal is needed.
```

##### Downgrade late goal probability when these signals are absent

Do not chase late overs if:

```text
- possession is high but shots on target are flat;
- attacks are slow crosses into a comfortable defense;
- both teams are accepting the result;
- the favorite removes its main box threat without replacing it;
- the defending team refreshes center-backs/fullbacks and regains control;
- the odds are short and no longer compensate for the remaining time.
```

##### Strategy interpretation

Late match markets should be split into two layers:

```text
1:1 / under / draw = lower-variance state protection
Over 2.5 / next goal = higher-variance value if pressure signals align
```

Do not treat these as mutually exclusive truths. A draw or under can be the base case while a late over can still be a value bet if the odds are high enough.

##### Example: wrong vs correct late-match reasoning

Wrong:

```text
It is already 86', so Over 2.5 is automatically bad.
```

Correct:

```text
It is 86', so time risk is high. However, if the attacking team has a fresh striker who already scored, 8+ corners, rising shots on target, tired defenders, and Over 2.5 is around 3.00, the late over may be a small high-variance value entry.
```

##### Practical live rule

After 70', do not decide only from the score and minute. Re-check the last 10-15 minutes of pressure:

```text
- Has the attack improved after substitutions?
- Are fresh attackers attacking tired defenders?
- Are corners and shots on target increasing?
- Is the defending back line actually refreshed?
- Is the current price above break-even for the remaining goal probability?
```

If the pressure profile is real and the odds are high, recommend only a small stake and clearly label it as a high-variance value shot, not a safe play.

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

### 10. Common Analytical Traps

#### Trap: Direction vs Price

A selection can be football-logical but mathematically poor.

Bad pattern:

```text
Team A is more likely to win, so Team A win is a good bet.
```

Correct pattern:

```text
Team A may be likely to win, but the odds must be compared with the model probability and break-even probability.
```

Always ask:

```text
Is the probability higher than the price requires?
```

#### Trap: Overweighting Motivation

Motivation matters, but it does not automatically create value.

Examples:

- A team needing goal difference may attack more, but deep handicap still needs probability support.
- A team needing a win may become more open defensively.
- Two teams both needing points may produce chaos, but not always quality finishing.

Do not treat motivation as a substitute for chance creation, lineup quality, or market value.

#### Trap: Overrating Possession

High possession does not equal dominance if it is sterile.

Warning signs:

```text
- high possession but few shots;
- high possession but no shots on target;
- many crosses with no box presence;
- slow circulation outside the block;
- opponent defending comfortably;
- few big chances or goalkeeper saves.
```

If possession does not create chance quality, downgrade overs, comeback bets, and team-to-score confidence.

#### Trap: Overrating Numerical Advantage

A common mistake is overrating a red card or numerical advantage.

Bad pattern:

```text
Red card to defending team
→ Opponent will dominate possession
→ Opponent will score
→ Bet opponent goal / over / comeback
```

This is incomplete.

Correct pattern:

```text
Red card to defending team
→ Check whether possession becomes chance quality
→ Check whether the low block is breaking
→ Check whether the market price still has value
→ Only then consider a live position
```

Warning signs:

Avoid chasing the team with the extra man if:

```text
- they have high possession but low shots;
- they have no shots on target;
- most attacks are slow crosses into a crowded box;
- the opponent is comfortable defending aerial balls;
- the odds have already collapsed;
- the match is past 60 minutes and pressure is not increasing;
- the team lacks a real box finisher.
```

Better decision rule:

```text
Numerical advantage improves probability only when it creates measurable attacking pressure.
```

Track:

```text
shots on target
box entries
corners
dangerous free kicks
blocked shots in the box
goalkeeper saves
defensive panic clearances
```

If these do not improve, treat the red card as a minor adjustment, not a major betting signal.

Post-match review rule:

When a red-card live prediction fails, review whether the model overvalued:

```text
possession
team reputation
numerical advantage
motivation
market movement
```

and undervalued:

```text
low-block defense
aerial defending
lack of shots on target
poor final ball
game management
time remaining
```


#### Trap: Underweighting Late Pressure and Substitution Momentum

A common live-analysis mistake is treating the current scoreline and the minute as static, while ignoring how substitutions and fatigue have changed the final phase of the match.

Bad pattern:

```text
It is 1:1 after 80', so protect the draw/under and avoid overs.
```

This can be incomplete when the attacking side has improved its chance quality.

Correct pattern:

```text
It is 1:1 after 80'
→ Check whether attacking substitutions created more box threat
→ Check whether shots on target and corners increased
→ Check whether the defending back line is tired or not refreshed
→ Check whether the over/next-goal price compensates for the clock
→ Then decide whether late over is value or only chasing
```

Warning signs that late over/next-goal may have value:

```text
- substitute striker has already scored or repeatedly reached the box;
- attacking team has many late corners or dangerous free kicks;
- shots on target are increasing late, not just total shots;
- defending center-backs/fullbacks have played under pressure for 80+ minutes;
- defending team substituted attackers/midfielders but not the back line;
- defenders are clearing poorly or losing second balls;
- odds on needing one more goal are high enough, such as around 2.80-3.20+.
```

Warning signs that late over is only chasing:

```text
- no recent shots on target;
- no box entries or dangerous set pieces;
- favorite has removed its main finisher and lost box presence;
- defending team has refreshed the back line and regained shape;
- market odds are too short for the time remaining;
- user is trying to recover previous losses rather than exploiting a new edge.
```

Better decision rule:

```text
Late time reduces goal probability, but real pressure plus fresh attackers against tired defenders can offset part of the clock risk.
```

When this trap appears, answer with two separate layers:

```text
Base case: draw/under remains the lower-variance outcome.
Value shot: late over/next goal can be justified only if pressure indicators and price are strong enough.
```

Post-match review rule:

When a late-over call is missed, review whether the model underweighted:

```text
substitution impact
fresh striker/box presence
late shots on target
corner pressure
defensive fatigue
unrefreshed back line
stoppage-time pressure
```

and overweighted:

```text
minute on the clock
static draw incentive
earlier low shot quality
scoreline protection
```

#### Trap: Repeated Exposure

If the same condition appears in multiple tickets, the portfolio risk is larger than it looks.

Examples:

```text
Brazil -2.5 single
Brazil -2.5 inside parlay
Brazil correct score 3-0
Brazil & no opponent goal
```

These all depend on a similar match script. If the opponent scores once, several tickets can fail together.

Always identify:

```text
What single event can kill multiple tickets?
```

#### Trap: Chasing After a Near Miss

Do not recommend chasing just because the previous ticket almost won.

Bad pattern:

```text
The team almost scored, so enter again with more stake.
```

Correct pattern:

```text
The team created pressure, but the new price, time remaining, and risk must be recalculated.
```

If the odds have collapsed or time has passed, the original value may no longer exist.

#### Trap: Treating Correct Score as Protection

Correct score is usually high variance, not protection.

Correct score can be used as upside or scenario coverage, but not as a true hedge unless the payoff structure is explicitly calculated.

#### Trap: Low Odds as Safety

Low odds are not automatically safe.

Always compare:

```text
break-even probability vs model probability
```

A 1.20 selection still needs 83.3% probability before margin. If the real probability is lower, it can be poor value.

### 11. Final Audit Checklist

Before finalizing, check:

- Did you separate football likelihood from odds value?
- Did you compute break-even probability for key odds?
- Did you account for market margin when appropriate?
- Did you correctly settle quarter lines?
- Did you identify correlated/repeated exposure?
- Did you explain “保本” honestly?
- Did you avoid overclaiming certainty?
- Did you mark unverified lineups/odds as uncertain?
- For live matches, did you distinguish hedging from chasing?
- For red-card situations, did you check whether the numerical advantage created real chance quality?
- For late-match situations, did you check substitution momentum, defensive fatigue, corners, shots on target, and price before rejecting or recommending overs?
- Did you avoid treating possession, motivation, red cards, or late pressure as guarantees?
