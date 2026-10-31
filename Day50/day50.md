# Day 50: Build Defend Your Experience

**Create an AI-Powered Adaptive Interview Defense Simulator**

## The idea

Most interview prep tools help you *improve* a resume. This one asks a different question: **can you defend every claim you made?**

You give the app your resume (or any write-up of your work). It pulls out each meaningful claim, then questions you the way a real interviewer would. Every answer changes the next question, so the conversation gets more specific as it goes. At the end you get a Defense Report showing which claims hold up and which need work.

## What I built

A single self-contained HTML file with no backend, no build step and no API key.

| Feature | How it works |
|---|---|
| Claim extraction | Claude reads the document and returns 6–10 claims, each with a reason an interviewer might doubt it and a personalised opening question |
| Adaptive interview | After each answer, Claude scores the defense (0–100), lists strengths and gaps, gives one coaching tip, and writes a sharper follow-up |
| Interviewer styles | Friendly recruiter, skeptical hiring manager, technical deep-dive, executive |
| Progress tracking | Per-claim confidence bars and a "claims tested" counter |
| Defense Report | Overall score ring, claims grouped by strength, optional game plan |
| Persistence | Sessions saved in `localStorage`, with a history list to reopen or delete |
| Export | Markdown and JSON (falls back to clipboard if downloads are unavailable) |
| Input | Drag-and-drop or paste; text, Markdown, CSV, JSON and HTML files |
| Resilience | Retry banner for rate limits and other errors, automatic backoff on rate limiting |
| Design | Warm, rounded style, light and dark themes, responsive layout, reduced-motion support |

## Design choices

- **Warm and friendly, not intimidating.** Interview practice is stressful. Soft colors, rounded shapes and encouraging feedback make it easier to keep going.
- **Color carries meaning.** Green means well defended (70+), amber means getting there (40–69), red means shaky (under 40). Each state also has a text label, so color is never the only signal.
- **One memorable thing.** The headline question and the score ring do the work. The rest stays quiet.

## Architecture

```
Home (upload / paste / pick interviewer)
   │
   ▼
Extract claims ──► Claude returns JSON: claims[]
   │
   ▼
Interview loop (per claim, max 3 rounds)
   question ─► answer ─► Claude scores + feedback ─► next question
   │
   ▼
Defense Report ──► optional game plan ──► export
```

State is one object per session:

```js
{
  id, created, title, mode, role, doc,
  claims: [{ id, text, why, firstQ, pending, score, rounds: [{ q, a, fb }] }],
  activeId, plan
}
```

Everything is rendered from that object, then saved to `localStorage` after each change.

## The prompts that matter

**1. Claim extraction.** The model plays the chosen interviewer and must quote or restate each claim in under 25 words. For each claim it gives `why` (what would be doubted) and `first_question` (which must reference the person's own details, not a generic template). Output is JSON only.

**2. Evaluation.** The model receives the claim, the doubt, the resume context, the previous exchange and the new answer. It scores on four things: personal ownership, concrete evidence, honesty about limits and story clarity. It must be fair but not inflate scores. It returns `score`, `verdict`, `strengths`, `gaps`, `coaching` and `next_question` (null once the score reaches 80).

**3. Game plan.** The model gets a summary of all claims and scores and returns 4–5 ordered rehearsal actions that name the specific claim and the evidence to prepare.

Each prompt demands JSON only, and a small parser strips code fences and reads from the first `{` to the last `}`.

## Problems and decisions

- **API access.** A published page can't call the Messages API directly, so the app uses the artifact runtime's "ask Claude" capability instead. It needs no key and no backend, and the first call asks the user for permission.
- **File types.** The browser can read text files natively. PDF and Word files can't be parsed without extra libraries, so the app tells the user to paste the text instead of failing silently.
- **Rate limits.** The helper retries twice with a growing delay, then shows a banner with a Retry button instead of losing the user's answer. The answer stays in the box.
- **Score honesty.** Untested claims count as zero in the overall score, because a real interviewer can ask about any of them.
- **Limiting rounds.** Three rounds per claim keeps a session finishable. A claim also ends early once it scores 80 or more.

## What I learned

1. A follow-up question is only useful if it points at something the person just said. Telling the model to build on a specific detail made questions feel far less generic.
2. Asking for structured JSON makes the UI simple, but you still need defensive parsing.
3. Friendly feedback and honest scoring can coexist if you tell the model to be kind in tone and strict on evidence.
4. Empty states matter. A new user should see the purpose, the three steps and a "Try an example" button before anything else.

## Not yet tested

I haven't run the app end to end, so check these first:

- [ ] Claim extraction on a real resume
- [ ] A full three-round interview and the score changes
- [ ] Rate-limit retry behavior
- [ ] Markdown and JSON export (and the clipboard fallback)
- [ ] Layout on a phone-sized screen
- [ ] Dark mode contrast

## Next steps

- PDF and DOCX parsing so users can upload them directly
- Voice answers with speech-to-text
- A timer mode for answering under pressure
- Compare two sessions to show improvement over time
- A "stronger version" rewrite of each answer in the user's own voice

## Links

- App: https://claude.ai/artifact/SXS89YhszptN8kXrTXTbGN
- Poster: https://claude.ai/artifact/KGBBXYoSM3h39yDf5WzNv4
