# Day 32: Think Like a Marketing Strategist

**Learn how great marketers think before they create.**

## What I built

A single-file, replayable web app called **Think Like a Marketing Strategist: Grow This Brand**. It teaches beginners how marketers make decisions, not just how to write posts. Every section explains **What is this?** and **Why does it matter?** in plain language, then ends with a **How to ask Claude** card holding a reusable prompt.

- **File:** `marketing-strategist.html`
- **Tech:** HTML, CSS and JavaScript, with React and Babel loaded from a CDN (no npm, no backend, no APIs)
- **UI:** dark, responsive, with progress bar, cards and transitions

## How it works

| Step | Stage | What you do | What you learn |
|---|---|---|---|
| 1 | Welcome | Start the simulation | Strategy is a set of choices that work together |
| 2 | Mode | Business, Personal Brand, or Random Client | Marketing applies to companies and to people |
| 3 | Audience | Describe and choose your core audience | Everything starts with who you are talking to |
| 4 | Platforms | Pick the best 3 of 7 | Fit beats being everywhere |
| 5 | Content pillars | Pick exactly 3 of 6 | Pillars serve awareness, trust or sales |
| 6 | 30-day roadmap | Review a weekly plan | Strategy answers why you post, not what to post |
| 7 | Surprise event | Respond to something unexpected | How you react shapes reputation |
| 8 | Growth Report | Review scores and lessons | Measure, reflect, improve |

Personal Brand mode swaps "product" for your expertise and story, "competitors" for people you admire, and weights LinkedIn, X, YouTube and newsletters more heavily.

## How to run it

1. Save `marketing-strategist.html`.
2. Open it in a browser with internet (the CDN scripts load on first run).
3. Choose a mode and play through all 8 steps.
4. Replay with a different mode or a new random client.

## My run: Edusmart AI

An AI study platform that turns PDFs into notes, quizzes, flashcards and study plans, aimed at students aged 16 to 28.

| Area | Choice | Score |
|---|---|---|
| Audience | Described in detail | 85% |
| Platforms | Instagram, LinkedIn, YouTube | 63% |
| Pillars | Education, Social Proof, Entertainment | 80% |
| Event | Harsh public review: replied publicly and offered a fix | 95/100 |
| **Growth potential** | | **High (81%)** |

**What went well:** replying openly to criticism showed that trust is built in public.

**What I'd change:** LinkedIn is a poor fit for students. TikTok would have been a better third platform. None of my pillars drove sales, so my best posts need a clear call to action.

## Prompts I used with Claude

Good prompts give a **role**, **context**, a **task** and a **format**.

1. **Audience:** "Act as a senior marketing strategist. I run [brand]. Interview me with 5 questions, then write a one-paragraph audience profile."
2. **Platforms:** "Act as a social media strategist. Compare the main platforms for [audience]. Give a fit score from 1 to 5, one reason, and weekly effort for each. Recommend the best three."
3. **Pillars:** "Act as a content strategist. For [brand], my pillars are [A, B, C]. Say which goal each supports, list 5 angles and 2 formats. Do not write full posts."
4. **Roadmap:** "Build a 4-week strategy roadmap for [brand] with the goal, strategy and one metric per week. Do not write individual posts."
5. **Event:** "Act as a crisis and opportunity advisor. For [brand], this just happened: [event]. Give 3 responses, the likely consequence of each, and which you'd choose."

## Three lessons

1. **Know your audience first.** Every platform and content choice depends on it.
2. **Fewer platforms, done well.** Fit beats presence everywhere.
3. **Balance awareness, trust and sales.** And respond to surprises in line with your values.

## Screenshots

Add your screenshots to a `screenshots/` folder in `Day32/`:

- `welcome.png`
- `mode.png`
- `platforms.png`
- `pillars.png`
- `roadmap.png`
- `event.png`
- `report.png`

I also made a poster that combines all of these stages and results.

## Folder structure

```
Day32/
├── Day32.md
├── marketing-strategist.html
└── screenshots/
```

## Next steps

- Replay in Personal Brand and Random Client modes and compare the scores.
- Add more events and random clients.
- Make the report pick the best decision across steps more fairly.
- Inline the CDN scripts so it runs fully offline.
