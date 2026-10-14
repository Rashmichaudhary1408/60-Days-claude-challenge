# Day 33: Build a Media Integrity Analyzer

**Topic:** Learn to evaluate information before believing it

A single-file, offline web app that teaches media literacy through interactive discovery. You observe, think, then reveal the answer. It is a guided lesson, not a quiz.

---

## What I Built

**Media Integrity Analyzer** is one HTML file written in pure vanilla HTML, CSS and JavaScript. It has no frameworks, no npm, no backend, no APIs and no images. It works fully offline in any browser.

### Features
- Four color themes: Emerald Green, Claude Orange, Midnight Blue, Royal Violet
- Short concept lesson before each challenge (simple explanation, why it matters, everyday life)
- Two interactive challenges with a reveal step
- Live Media Integrity metrics that update as you progress
- Final dashboard with a replay option that picks new scenarios
- Premium dark editorial design, smooth animations, progress bar, responsive layout

---

## The Learning Flow

| Step | Screen | What happens |
|------|--------|--------------|
| 1 | Theme choice | Pick a color theme |
| 2 | Concept 1 | Learn why headlines are advertisements for stories |
| 3 | Headline Detective | Read a fictional story, choose Yes / Maybe / No to "Would you click this?", tap exaggerated parts |
| 4 | Headline reveal | Accuracy score, highlighted mismatches, explanation, fair rewritten headline, key takeaway |
| 5 | Concept 2 | Learn why emotion is the fastest persuader |
| 6 | Emotion Detector | Read a fictional post, say how it felt, tap the influencing words |
| 7 | Emotion reveal | Target audience, intended emotion, manipulation technique, highlighted phrases, neutral rewrite, key takeaway |
| 8 | Dashboard | Overall score, what you learned, biggest red flag, three habits, replay |

### Live Metrics
- **Headline Accuracy**: how well the headline matches the article
- **Source Reliability**: average trust score of the sources seen
- **Emotional Manipulation**: how strongly the post pushes feelings
- **Audience Targeting**: how precisely the post aims at a group

---

## Key Media Literacy Concepts

1. **Headlines can exaggerate.** Compare the headline with the real numbers and quotes in the article.
2. **Strong verbs are a warning.** Words like "proves" and "cures" often claim more than a small study shows.
3. **Proposal is not decision.** Check whether something has happened or is only suggested.
4. **Emotion is a tool.** Fear, outrage and FOMO make people share before they think.
5. **Urgency hides weak evidence.** "Only 2 hours left" is pressure, not proof.
6. **Neutral rewrites reveal the facts.** Remove the feeling and see what is left.

## Three Habits to Keep
1. **Read past the headline.** Check whether the article backs up the big claim.
2. **Pause when you feel a surge.** Fear, anger or FOMO plus urgency is a cue to slow down.
3. **Check the source and the evidence.** Ask who made it, what they want, and where the proof is.

---

## How It Works (Technical Notes)

- Scenarios are stored as data in arrays. Each text chunk carries an optional "red flag" note, so the app can score what you tapped and highlight what you missed.
- Score = (flags found minus half of wrongly flagged parts) divided by total flags, limited to 0 to 100.
- Themes use CSS custom properties on `data-theme`, so switching is instant.
- Random scenarios avoid repeating the previous one, so replay always feels new.
- `color-mix()`, `conic-gradient` and CSS grid handle the visuals with no libraries.

## How to Run
1. Save `media-integrity-analyzer.html`.
2. Double-click it to open in your browser.
3. Choose a theme and complete both challenges.
4. Review the dashboard and replay with new scenarios.

---

## Project Structure
```
Day33/
├── Day33.md
├── media-integrity-analyzer.html
└── screenshots/
```

## What I Learned
- Teaching by discovery works better than testing. Users reveal answers after thinking.
- Good media literacy is a habit of pausing, checking, and comparing, not a list of rules.
- Data-driven UI keeps a single-file app small and easy to extend with more scenarios.

## Ideas for Next Time
- More scenarios (charts, quotes, photo captions)
- Streak tracking across replays
- Printable summary of the dashboard
