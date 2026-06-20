# predict_sc_strategy

This repository contains the `football-value-analysis` ChatGPT Skill for structured football/soccer match research, prediction, odds-value analysis, Asian handicap/total-goals settlement, same-game parlay review, live-match reassessment, betting-slip payoff math, and risk-controlled strategy design.

## Contents

- `football-value-analysis/SKILL.md` — main skill instructions
- `football-value-analysis/references/market-rules.md` — Asian handicap, totals, DNB, same-game parlay settlement rules
- `football-value-analysis/references/output-templates.md` — reusable output templates
- `football-value-analysis/agents/openai.yaml` — ChatGPT UI metadata
- `skill.zip` — packaged upload-ready skill bundle

## Upload the skill

Upload `skill.zip` in ChatGPT Skills.

## Push to GitHub

If the repo is empty and you have SSH access configured:

```bash
git clone git@github.com:TuVon010/predict_sc_strategy.git
cp -R football-value-analysis skill.zip predict_sc_strategy/
cd predict_sc_strategy
git add .
git commit -m "add football value analysis skill"
git push origin main
```

Or from this directory:

```bash
git init
git add .
git commit -m "add football value analysis skill"
git branch -M main
git remote add origin git@github.com:TuVon010/predict_sc_strategy.git
git push -u origin main
```
