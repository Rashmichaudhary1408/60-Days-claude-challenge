# Day 45: Build an AI Decision Strategist

### Think Better. Decide Smarter.

*ABTalks 60-Day Challenge | Built with Claude AI*

---

## The Idea

Tough decisions rarely fail because of a lack of information. They fail because our thinking is clouded by fear, bias and wishful thinking.

Today I built an **AI Decision Strategist**: a short, guided interview that turns a messy decision into a clear, visual report. It asks four questions, then produces a complete, interactive decision dashboard.

The rule I gave the AI: **be impartial, challenge me, and don't tell me what I want to hear.**

---

## How It Works

### Step 1: The 4-Question Interview

The strategist asks one question at a time and collects answers without analyzing yet.

| # | Question | What it uncovers |
|---|----------|------------------|
| 1 | What's the decision, and why is it hard? | The real options and the emotional weight |
| 2 | What's your goal and timeline? | The yardstick for judging each option |
| 3 | What does your gut say, and what's stopping you? | Hidden preferences and doubts |
| 4 | What are you most scared of, and can you undo it? | Risk and reversibility |

### Step 2: The Decision Report

After the fourth answer, Claude generates a single HTML dashboard with eight sections:

1. **The Real Decision:** the actual trade-off and why it's emotionally hard
2. **The Case for Each Option:** strongest case, hidden upside, biggest weakness, who it suits
3. **Assumption Buster:** three assumptions, two named biases, one thing being ignored
4. **Decision Matrix:** each option scored out of 70 across 7 dimensions, with animated bars
5. **Premortem:** imagine it failed after 12 months, find the reasons, warning sign and prevention
6. **7-Day Test Plan:** research, experiment, conversation, decision day
7. **The Verdict:** one decisive pick, what could flip it, one hard truth
8. **Shareable Cards:** three screenshot-ready cards for social sharing

### The 7 Scoring Dimensions

Life/Career Upside, Financial Safety, Growth & Learning, Stress Level, Reversibility, Long-term Alignment, Regret Risk.

---

## Test Run: Placement Prep Strategy

I tested the full workflow with a real decision: **how to prepare for a Google SWE placement in the next 6 months.**

| Option | Score |
|--------|-------|
| A: DSA + Core CS first | **52 / 70** |
| B: Balanced prep + AI/ML projects + applications | 51 / 70 |
| C: AI/ML portfolio first | 37 / 70 |

**Verdict:** Option A wins narrowly, with projects and applications kept as a capped side track.

**Hard truth from the report:** *Six months is enough only if you measure readiness with timed mocks, not with how many hours you studied.*

**Biggest insight:** I had no measured baseline. Every option was a guess until I took a mock interview. The report turned a vague worry into a concrete first step: one timed mock in the first week.

---

## What I Built and Tested

- [x] Wrote the strategist prompt with strict interview rules
- [x] Answered all 4 questions with a real decision
- [x] Generated the complete HTML report
- [x] Saved it as `decision-report.html`
- [x] Opened it in a browser and checked the animated matrix
- [x] Created a one-page poster summarizing all 8 steps
- [x] Took screenshots of the report and shareable cards

**Files:** `decision-report.html`, `decision-poster.png`, `decision-poster.pdf`

---

## Lessons Learned

1. **Specific input beats clever prompts.** The report is only as good as the answers. Labels like "Option A" give the AI nothing to work with.
2. **One question at a time works.** It keeps the interview fast and makes answers more honest than a long form.
3. **Forced structure creates clarity.** Seeing biases, risks and scores side by side exposes weak thinking.
4. **Scores are judgment, not data.** The matrix is a thinking aid. It organizes your reasoning but doesn't replace testing.
5. **Reversibility changes the decision.** Knowing you can adjust lowers the pressure to pick perfectly.

---

## Try It Yourself

1. Paste the Decision Strategist prompt into Claude.
2. Answer the four questions with a real decision, in a sentence or two each.
3. Let Claude build the HTML report.
4. Save the file and open it in your browser.
5. Take the 7-Day Test Plan seriously. Day 7 is where the decision gets made.

---

## LinkedIn Caption

**I stopped overthinking a big decision and let AI interview me instead.**

4 questions. 8 sections. 1 clear verdict.

My AI Decision Strategist challenged my assumptions, named my biases and scored every option. Then it gave me a 7-day plan to test the answer before committing.

Think better. Decide smarter.

What decision are you stuck on?

`#ABTalks` `#60DayChallenge` `#ClaudeAI` `#DecisionMaking` `#BuildInPublic`

---

*Day 45 of 60 | Built with Claude AI | ABTalks 60-Day Challenge*
