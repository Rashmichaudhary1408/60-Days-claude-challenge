# Day 25: Entrepreneurship Applications with Claude

## 🦈 Build an AI Shark Tank Simulator
**Pitch your startup to AI investors**

A single-file web app, built with Claude, where you pitch a startup idea to four AI "sharks", answer their tough questions, and receive a scorecard, valuation and investment decision. It runs entirely in the browser, with no backend, no API keys and no external libraries.

---

## 🎯 Objective

Use Claude to design and generate a complete, production-style web application from a single detailed prompt, then test it end to end as a real user would.

## ✨ Features

| Area | What it does |
|---|---|
| **Startup input** | Startup Name, Problem, Solution, Revenue Model, Target Audience, Funding Ask |
| **AI judges** | 🦈 Venture Capitalist (market size, scalability) · 🦈 Founder (execution) · 🦈 Customer (usefulness) · 🦈 Angel Investor (profitability) |
| **Pitch round** | Pitch summary, 8 questions (2 per judge), user answers, dynamic judge reactions |
| **Scoring** | Market Potential, Innovation, Business Model, Execution, Investment Worthiness (each /100) |
| **Decision** | Invest, Reject, Acquire or Come Back Later, with suggested valuation, funding amount, equity and reasoning |
| **UI** | Dark Shark Tank theme, animated cards, responsive layout |
| **Bonus** | Confetti on funding success, downloadable PDF pitch report, leaderboard, share button |

## 🛠️ Tech Stack

- HTML, CSS and vanilla JavaScript in one file
- Rule-based scoring engine that checks answer length, specificity, numbers and keywords
- `localStorage` for the leaderboard
- A hand-built PDF generator, so no libraries are needed
- Canvas API for confetti

## 🚀 How to Run

1. Download `shark-tank-simulator.html`.
2. Double-click it to open it in any modern browser.
3. No installation or internet connection is required.

## 🧪 Step-by-Step Walkthrough

1. Paste the project prompt into Claude and generate the HTML.
2. Save the output as `shark-tank-simulator.html`.
3. Open it in your browser.
4. Fill in all six startup fields (or use **Fill demo idea**).
5. Click **Start the Simulation**.
6. Read each judge's question.
7. Answer the questions and watch how the judges react.
8. Review the **scorecard**.
9. Review the **investment decision**.
10. Check the **valuation and funding** recommendation.
11. Open the **Leaderboard** and run a second pitch to test ranking.
12. Click **Download Pitch Report** to get the PDF.
13. Take screenshots of the key screens.


## 📊 How the Decision Is Made

- **Invest**: overall score of 72 or higher. Funding is the ask (or 80% of it), and equity is set by score.
- **Acquire**: strong innovation but weak execution, so the sharks offer a buyout.
- **Come Back Later**: promising but not ready, with an overall score of 55 or higher.
- **Reject**: overall score below 55.

Better answers (specific, numeric, relevant) raise each judge's confidence and therefore the final score.

## 💡 Key Learnings

- Detailed, structured prompts produce complete apps in one pass.
- Splitting requirements into inputs, logic, scoring, UI and bonus features keeps the output organized.
- A self-contained HTML file is the easiest way to prototype and share an idea.
- Testing the generated app as a user is as important as generating it.

## ⚠️ Limitations and Next Steps

- Judges use templated, rule-based logic, not a live LLM. Connecting the Claude API would make questions and reactions fully dynamic.
- The PDF report is plain text. A styled layout could be added.
- Possible extensions: voice pitching, multiple pitch rounds, investor negotiation, and a shareable result image.

## 📁 Project Structure

```
Day25/
├── Day25.md
├── shark-tank-simulator.html
└── screenshots/
    ├── 01-input.png
    ├── 02-questions.png
    ├── 03-results.png
    └── 04-leaderboard.png
```

---
*Part of my daily Claude learning series. Day 25 of the challenge.*