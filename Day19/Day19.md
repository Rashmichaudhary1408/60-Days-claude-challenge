# Day 19: Build a Football Intelligence Hub

**Turn football data into predictions, assessments, and insights**

A three-stage football experience powered by a single Excel workbook: a World Cup 2026 prediction report, a Football IQ quiz, and a Messi vs Ronaldo personality match, all combined into one poster-style profile.

---

## What I Built

An AI-guided **Football Intelligence Hub** that acts as an analyst, educator, and personality assessor. It adapts its explanations to the user's football knowledge level and ends with a shareable Football Intelligence Profile.

| Stage | Name | What it does |
|---|---|---|
| 0 | Knowledge Level Check | Asks how familiar the user is with football and adjusts depth and jargon to match |
| 1 | World Cup 2026 Prediction Report | Predicts winner, runner-up, dark horse and players to watch, with confidence scores |
| 2 | Football IQ Quiz | 5 questions (beginner to advanced) that produce a Football Awareness Score and fan classification |
| 3 | Messi vs Ronaldo Personality Match | 12 questions (multiple-choice and rating scale) that produce compatibility scores, an archetype and recommendations |
| Final | Football Intelligence Profile | One poster page combining everything, with key insights |

---

## Data Source

`ABTalks_WorldCup_Intelligence_Master.xlsx`, one sheet with seven tables:

1. **Team historical performance:** 50 matches per team (wins, draws, losses, goals for and against, win %)
2. **Last 5 World Cups (2006-2022):** hosts, winners, runners-up, Golden Ball, Golden Boot
3. **Current contenders:** FIFA rank, recent record, goals, Form Score
4. **Star players:** goals, assists, rating
5. **User football awareness input** (template for quiz scoring)
6. **Messi vs Ronaldo personality input** (template for trait scoring)
7. **Live World Cup 2026 data:** 21 group matches and standings up to June 17, 2026

---

## Stage 1: Prediction Approach

I combined four signals from the workbook:

- **Long-run record:** win % and goal difference per match
- **Current form:** Form Score and goals scored and conceded in the last 10 games
- **Tournament pedigree:** finals and titles across the last five World Cups
- **Live results and star power:** 2026 opening matches and player ratings

### Results

| Prediction | Pick | Confidence |
|---|---|---|
| Winner | Argentina | 24% |
| Runner-up | France | 18% |
| Dark horse | Morocco | 9% (semi-final or better) |
| Players to watch | Mbappé, Messi, Bellingham, Haaland | 55-80% |

**Why Argentina:** FIFA #1, Form Score 92, 22 goals scored and only 6 conceded in the last 10, and a 3-0 opener.
**Why France:** reached 3 of the last 5 World Cup finals.
**Why Morocco:** joint-best defense among contenders (6 conceded) despite ranking 12th.

Confidence scores are kept modest on purpose. With 48 teams, even the favorite is far from a sure thing.

---

## Stage 2: Football IQ Quiz

- Questions drew on workbook facts (points system, 2022 final, 2018 Golden Boot, repeat runners-up, best historical defense).
- Weighted scoring: beginner 15 points, intermediate 25, advanced 20.
- **Sample result:** 80/100, **Football Enthusiast**.
- Biggest learning gap: reading team stats. Brazil conceded the fewest goals (30 in 50 matches), not France (38).

---

## Stage 3: Messi vs Ronaldo Personality Match

- 12 questions, none asking directly about Messi or Ronaldo.
- Traits measured: ambition, discipline, leadership, teamwork, creativity, competitiveness, confidence, work ethic, learning style and decision-making style.
- Each answer adds points toward Messi, Ronaldo and one of eight archetypes.
- Output: compatibility percentages, which legend you resemble more, an archetype, and one recommended player, club, national team and rivalry.

**Archetypes:** Creative Playmaker, Relentless Competitor, Tactical Visionary, Quiet Leader, Fearless Attacker, Strategic Commander, Consistent Performer, Big-Match Specialist.

---

## Output

A single self-contained HTML poster (`football_intelligence_poster.html`) with:

- World Cup 2026 report with confidence bars
- Football Awareness Score ring and classification
- Interactive personality quiz that calculates results in the browser
- Archetype card, recommendations and key insights summary
- Light and dark mode, mobile-friendly layout

**To run it:** download the file and open it in any browser. No install needed.

---

## Key Learnings

- **Data limits matter.** The workbook is a snapshot from June 17, 2026, with pending scores and a few inconsistencies (for example the Austria and Algeria standings), so the forecast is treated as an estimate rather than a fact.
- **Honest confidence beats bold claims.** Modest percentages reflect how unpredictable tournaments are.
- **Adapting to the audience works.** Explaining terms like "dark horse" and goal difference made the report accessible to a beginner.
- **Structured prompts help.** Staged prompts with clear outputs at each step made the experience easy to follow and easy to combine into one final profile.



