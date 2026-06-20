# Football Market Rules Reference

Use this reference whenever the user asks what a football market means or how a ticket settles.

## Total Goals

### Over 1.5
Needs at least 2 total goals.

| Score | Total | Over 1.5 |
|---|---:|---|
| 0-0 | 0 | lose |
| 1-0 | 1 | lose |
| 1-1 | 2 | win |
| 2-0 | 2 | win |
| 2-1 | 3 | win |

### Over 2.5
Needs at least 3 total goals.

| Score | Total | Over 2.5 |
|---|---:|---|
| 1-1 | 2 | lose |
| 2-0 | 2 | lose |
| 2-1 | 3 | win |
| 3-0 | 3 | win |

### Over 2.25
Split the stake:

```text
50% over 2.0
50% over 2.5
```

| Total goals | Result |
|---:|---|
| 0-1 | full loss |
| exactly 2 | half loss |
| 3+ | full win |

### Under 2.25
Split the stake:

```text
50% under 2.0
50% under 2.5
```

| Total goals | Result |
|---:|---|
| 0-1 | full win |
| exactly 2 | half win |
| 3+ | full loss |

### Over 2.75
Split the stake:

```text
50% over 2.5
50% over 3.0
```

| Total goals | Result |
|---:|---|
| 0-2 | full loss |
| exactly 3 | half win |
| 4+ | full win |

### Under 3.75
Split the stake:

```text
50% under 3.5
50% under 4.0
```

| Total goals | Result |
|---:|---|
| 0-3 | full win |
| exactly 4 | half loss |
| 5+ | full loss |

## Asian Handicap

### +0.75
Split the stake:

```text
50% +0.5
50% +1.0
```

| Selected team result | +0.75 |
|---|---|
| win | full win |
| draw | full win |
| lose by 1 | half loss |
| lose by 2+ | full loss |

### -0.75
Split the stake:

```text
50% -0.5
50% -1.0
```

| Selected team result | -0.75 |
|---|---|
| win by 2+ | full win |
| win by 1 | half win |
| draw or lose | full loss |

### -1.0

| Selected team result | -1.0 |
|---|---|
| win by 2+ | win |
| win by 1 | push/refund |
| draw or lose | lose |

### -1.5

| Selected team result | -1.5 |
|---|---|
| win by 2+ | win |
| win by 1 or less | lose |

### -2.5

| Selected team result | -2.5 |
|---|---|
| win by 3+ | win |
| win by 2 or less | lose |

## Draw No Bet / 平局退款

| Result | Settlement |
|---|---|
| selected team wins | win |
| draw | stake refunded |
| selected team loses | lose |

## Team & Yes/No

- `team & yes`: selected team wins and both teams score.
- `team & no`: selected team wins and opponent does not score.

Example: `Brazil & No` wins on 1-0, 2-0, 3-0, 4-0, etc.

## Same-Game Parlay

A same-game parlay requires every condition to be true. It increases payout but narrows the winning score band.

Example:

```text
Canada win + over 1.5
```

Wins on 2-0, 2-1, 3-0, 3-1. Loses on 1-0, 1-1, 0-0, 0-1.
