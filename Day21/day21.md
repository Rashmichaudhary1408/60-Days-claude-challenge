# Day 21: Privacy Intelligence with Claude

**Build a Digital Privacy Intelligence Dashboard**
*Visualize your digital footprint and privacy exposure*

---

## Overview

Today I used Claude to build an interactive **Digital Privacy Intelligence Dashboard**: a single self-contained HTML file that turns a list of apps into scores, heatmaps, rankings and a personalised privacy plan.

The goal was to see how much a simple list of everyday services can reveal about digital exposure, and to do it responsibly by clearly separating **Facts** from **Estimates**.

> **Important:** The dashboard never accesses private databases or real account data. It works only from the list of services provided, and every behavioural or demographic conclusion is labelled as an estimate.

## Live Artifact

[Open the dashboard](https://claude.ai/artifact/McM5Dnq84ijQMiYRv8sqwh)

The generated file is saved in this repo as `digital-privacy-dashboard.html`. Open it in any modern browser.

## Sample Dataset (Facts)

| Category | Services |
|---|---|
| Social | Instagram, Snapchat, TikTok, YouTube, Discord |
| Messaging | WhatsApp, iMessage |
| Entertainment and gaming | Spotify, Roblox, PUBG Mobile |
| Shopping and payments | Amazon, Meesho, Google Pay |
| Search and storage | Google Search, Google Photos |

**15 services** across **11 inferred parent companies**: Meta, Snap Inc., ByteDance, Alphabet, Discord Inc., Apple, Spotify AB, Roblox Corp., Krafton, Amazon and Meesho.

## Dashboard Sections

| # | Section | What it shows |
|---|---|---|
| 1 | Digital Footprint Score | 0-100 score with levels: 🟢 Minimal, 🟡 Moderate, 🟠 Significant, 🔴 Extensive |
| 2 | Privacy Score | 0-100 score with levels: 🔴 Weak, 🟠 Fair, 🟡 Good, 🟢 Strong |
| 3 | Summary stats | Total services, parent companies, ecosystem concentration, estimated tracking surface |
| 4 | Exposure Heatmap | Service x data-type grid showing how likely each service is to handle each data type |
| 5 | Company Exposure Ranking | Which parent companies hold the largest share of your exposure |
| 6 | Data Collection Matrix | Likelihood of each data type being collected, by company |
| 7 | Risk Radar | Radar chart across 10 data categories |
| 8 | Digital Twin Profile | A cautious, estimated reading of how an analyst might profile the footprint |
| 9 | WOW Insights | Surprising patterns, such as Alphabet owning 4 of 15 services |
| 10 | Most Valuable Data Assets | The data types most useful to advertisers or attackers |
| 11 | Privacy Improvement Plan and Simulator | Tick steps and watch both scores update live |
| 12 | Final Verdict | A plain-language summary that updates with the simulator |

## Facts vs Estimates

| Type | Examples |
|---|---|
| **Fact** | The list of services, the parent company of each service |
| **Estimate** | All scores, heatmap levels, the Digital Twin, data value rankings, concentration score |

Anything that cannot reasonably be inferred (income, occupation, health) shows: *"Not enough information provided."*

## How the Scores Work

The scoring is a simple, transparent heuristic, not a real measurement.

1. Each service gets a 0-3 likelihood for 10 data types: Identity, Contacts, Location, Messages, Media, Payments, Search, Behavior, Device and Biometric.
2. **Footprint score** is the total likelihood across all services, scaled to 0-100.
3. **Ecosystem concentration** uses a Herfindahl-style index of how services are split across parent companies.
4. **Privacy score** is 100 minus a weighted blend of the footprint score and concentration.
5. **Tracking surface** is the count of non-zero data-type touchpoints across all services.
6. The simulator subtracts footprint and adds privacy points for each recommended action you tick.

## Steps I Followed

1. Pasted the Digital Privacy Dashboard prompt into Claude.
2. Reviewed the sample dataset included in the prompt.
3. Generated the complete HTML dashboard.
4. Reviewed the Digital Footprint Score.
5. Analysed the Privacy Score.
6. Explored the Exposure Heatmap.
7. Reviewed the Company Exposure Ranking.
8. Analysed the Digital Twin Profile section.
9. Reviewed the Risk Radar.
10. Studied the Most Valuable Data Assets section.
11. Tried the Privacy Improvement Simulator.
12. Read the Final Verdict.
13. Took screenshots and saved the HTML file.

## Key Learnings

- **Concentration matters.** Several services sharing one parent company means one account or policy can connect a lot of data.
- **Payments and social graphs are high value.** Purchase history and contact networks are among the most valuable data types.
- **Small settings add up.** Location sharing, contact syncing and ad personalisation are quick wins that reduce exposure.
- **Honest labelling builds trust.** Separating facts from estimates keeps a privacy tool from overclaiming.
- **Prompt design works.** Clear rules (never claim certainty, never claim database access) shaped the whole output.

## Tech Notes

- Single HTML file with inline CSS and JavaScript, no external dependencies
- Light and dark theme support with a toggle
- Responsive layout that works on mobile and desktop
- Pure SVG gauges and radar chart

## Disclaimer

This dashboard is an educational project. All scores and profiles are **estimates** derived only from a list of app names. They are not audits of any real account, and they do not reflect actual data held by any company.

---

*Part of my daily AI learning series. Day 21 complete.*