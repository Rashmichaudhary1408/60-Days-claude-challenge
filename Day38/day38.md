# Day 38: Build Typing Speed Studio
### Create a Premium Commercial Typing Platform

**Date:** 19 October 2026
**Tool:** Claude (chat interface)
**Output:** `typing-speed-studio.html`, a single self-contained HTML, CSS and JavaScript app, plus a result poster

---

## 1. Goal

Build a polished, commercial-feeling typing platform, not just a basic typing test. It had to run from a single HTML file, with no libraries, frameworks or account system. It should compare with platforms like Monkeytype in its analytics and UX.

## 2. Workflow

| Step | What I did |
|------|-----------|
| 1 | Pasted the Typing Speed Studio prompt into Claude |
| 2 | Answered the interview questions, one at a time |
| 3 | Claude generated the complete HTML application |
| 4 | Saved it as `typing-speed-studio.html` |
| 5 | Opened it locally in the browser |
| 6 | Tried multiple typing modes |
| 7 | Completed several typing sessions |
| 8 | Reviewed the analytics dashboard |
| 9 | Took screenshots and turned them into a poster |

### Interview answers

1. **Typing experience:** Academic (sciences, humanities and social sciences passages)
2. **Features:** Automatic, so Claude chose the full feature set

## 3. What was built

### Typing modes
- **Time:** 15, 30, 60 and 120 seconds
- **Words:** 25, 50, 100 and 250 words
- **Quote:** short academic quotes
- **Custom:** paste your own text
- **Adaptive:** difficulty level 1 to 5, adjusted by accuracy and speed
- **Focus:** only the current line is visible
- **Zen:** untimed, distraction-free practice

### Dynamic academic passages
Passages are generated from sentence templates (subject + verb + object + qualifier) for each discipline, so no two sessions are identical. Adaptive levels add longer clauses and denser vocabulary.

### Live statistics
WPM, Raw WPM, CPM, Accuracy, Time, Mistakes, Streak, Done % and Remaining, plus a progress bar. Characters show correct, incorrect and cursor states with smooth transitions.

### Analytics dashboard (after every session)
- WPM, Accuracy, Raw WPM, Consistency, Completion and Duration
- WPM progress graph (net vs raw) with error markers
- Accuracy-over-time graph
- Character counts: correct, incorrect, extra, missed
- Typing rhythm graph and average key interval
- Keyboard error heatmap
- Percentile estimate, achievement badges, personal bests
- Summary of strengths, weaknesses and personalised suggestions

### Product features
- Local history, personal bests and daily streaks (via `localStorage`, no account)
- Pause (Esc), restart (Tab), next test (Enter)
- Four themes, font size slider, optional sound effects
- Reduced-motion support, focus outlines, ARIA labels, responsive layout

## 4. Key concepts I learned

**Net WPM**

```
WPM = (correct characters / 5) / minutes
```

One "word" is 5 characters, and only correct characters count.

**Raw WPM** uses all keystrokes, including mistakes.

**Accuracy** is correct keystrokes divided by total keystrokes.

**Consistency** is based on how much per-second typing speed varies. A lower coefficient of variation gives a higher score:

```
consistency = 100 * (1 - tanh(cv + cv^3/3 + cv^5/5))
```

**Realistic values:** WPM is computed over at least a 1-second window and capped at 400, so unrealistic numbers such as 20,000 WPM can't appear.

**Percentile estimate:** a normal curve around about 40 WPM with a standard deviation of 16. It is an estimate, not real user data.

## 5. My test session

Mode: **Time 120s, Mixed discipline**

| Metric | Result |
|--------|--------|
| WPM | 28 |
| Raw WPM | 33 |
| Accuracy | 85.2% |
| Consistency | 45% |
| Completion | 100% |
| Characters | 277 correct, 48 incorrect, 8 extra, 0 missed |
| Best streak | 60 |
| Total keystrokes | 325 |
| Avg key interval | 369 ms |
| Percentile | about 22.1% |
| Badges | Endurance, First session, New personal best |

**Most mistyped keys:** space (8), s (6), e (6), c (4), i (3)

**Takeaways**
- The WPM graph dipped sharply early on, a sign of starting too fast and making early errors. Speed then recovered and stabilised.
- Accuracy and consistency are the main weaknesses.
- The suggestions were to slow down, keep a steady rhythm and drill the weak keys.

## 6. Prompting lessons

- A staged interview (one question at a time) makes the output fit the user's intent.
- Being specific about the output, such as the exact stats, graphs and badges, produces a much richer dashboard.
- The constraint "single file, no external libraries" keeps the project portable.
- Calling out edge cases up front, like unrealistic WPM values, makes the calculations trustworthy.
- Screenshots of results can be fed back to Claude to generate a shareable poster.

## 7. Limitations and next steps

**Known limitations**
- No Programming mode, because I chose Academic.
- "Extra" counts only letters typed where a space was expected.
- The percentile is a rough estimate.

**Ideas to extend**
- Word-by-word (Monkeytype-style) typing engine
- Larger quote and passage libraries
- Export or import of history
- More categories, with a switcher inside the app (Adaptive category version)
- Weak-key drill mode that generates text around mistyped letters

## 8. Files

- `typing-speed-studio.html`: the application
- Result poster: https://claude.ai/artifact/UFqH1Qge6TwW4Gxrehh989
- Screenshots of the analytics dashboard (taken locally)

---

**Summary:** In one session I went from a single prompt to a complete typing platform with seven modes, live stats, a full analytics dashboard, local history and a shareable result poster.
