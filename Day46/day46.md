# Day 46: Build Autonomous Agent Studio

**Topic:** Design Multi-Agent AI Systems with Claude
**Project:** Autonomous Agent Studio, a single-file HTML app where seven agents write, score and rewrite marketing copy until it is good enough to ship.

---

## 1. What I built

A browser app that takes a creative brief (product, audience, tone, goal) and runs an automatic improvement loop:

1. A **Planner** turns the brief into a strategy and a 100-point rubric.
2. An **Executor** writes the first full draft.
3. A **Safety Monitor** checks the draft for fabricated claims and risky wording.
4. An **Evaluator** scores the draft.
5. A **stop check** decides whether to continue.
6. If not stopping: a **Critic** diagnoses, an **Improver** rewrites, a **Memory Manager** records lessons, and the loop repeats.
7. When the loop stops, the best draft goes through a Safety check and a **Final Reviewer**.

The number of rounds is decided at runtime, not hard-coded.

---

## 2. Core concepts

### Multi-agent system
Instead of one giant prompt, split the work into agents with one job each. Every agent is just **a system prompt plus a Messages API call**. The "intelligence" of the system comes from how they are connected, not from any single agent.

### Orchestrator
One function (`run()`) owns all state and decides who runs next. The agents never talk to each other directly. The orchestrator passes the right context to each one.

State it keeps:
- `hist`: score, delta, critique and draft for every round
- `mem`: a rolling memory string (what to keep, what to avoid, open issues)
- counters for API calls, retries and timing

### Agent roles in this project

| Agent | Job | Output format |
|---|---|---|
| Planner | Strategy, structure, rubric | Markdown |
| Executor | First full draft | Copy only |
| Safety Monitor | Flag fabricated stats, risky claims | JSON |
| Evaluator | Score clarity, persuasion, originality | JSON |
| Critic | Top 3 weaknesses with quoted evidence | Numbered list |
| Improver | Rewrite using the critique | Copy only |
| Memory Manager | Compact notes, max 120 words | Bullets |
| Final Reviewer | Fix typos and consistency, sign off | Copy plus sign-off |

### Evaluator-optimizer loop
The central pattern. One agent produces, another judges, a third explains what to fix, and the producer tries again. It works because **judging is easier than generating**, and a separate judge catches what the writer cannot see.

---

## 3. The stop check (autonomy)

What makes this "autonomous" is that the system decides when to stop. Checked in this order after every evaluation:

1. **Manual stop**: the user pressed "Stop after this round".
2. **Plateau**: score improved by less than 1.5 points for 2 rounds in a row.
3. **Threshold**: score reached 90/100.
4. **Iteration cap**: 12 rounds, a safety limit against runaway cost.

```js
const CFG = { thr: 90, delta: 1.5, cap: 12, model: "claude-sonnet-4-6" };
```

**Lesson:** every autonomous loop needs at least two exits, one for success and one for "stop burning money". The cap is not optional.

---

## 4. Design decisions worth remembering

- **The Evaluator never sees its own past scores.** This avoids anchoring: it judges each draft fresh against the rubric.
- **The Evaluator prompt is calibrated.** "First drafts usually deserve 55-75" stops score inflation, which would trigger the threshold stop too early.
- **Memory is capped at 120 words.** Unbounded memory bloats every later prompt. Compact memory (Keep / Avoid / Open issues) stays useful.
- **The Critic must quote the weak passage.** Vague critique produces vague rewrites. Evidence makes fixes concrete.
- **The Improver keeps the structure and stays within 15% of the original length.** This prevents the rewrite from drifting or ballooning.
- **The best draft wins, not the last one.** The final step picks the highest-scoring round, because later rounds can regress.
- **Safety runs twice**: once early (its findings seed memory) and once on the best draft before sign-off.

---

## 5. Reliability engineering

Agents fail. The app handles it:

- **Retries with exponential backoff** in `call()`: up to 4 attempts, waiting `1200 * 2^i` ms between them.
- **JSON repair loop** in `askJSON()`: if the reply is not valid JSON, ask again with "Return valid JSON only", up to 3 times. It slices from the first `{` to the last `}` to ignore stray text.
- **Validation**: the Evaluator's `score` must be a finite number or the reply is rejected.
- **Observability**: an activity log, per-agent call counts, average latency and retry counts, shown at the end in a performance table.

**Lesson:** the model is only one part of the system. Parsing, retries and logging decide whether it works on a bad day.

---

## 6. Calling Claude from the browser

```js
const r = await fetch("https://api.anthropic.com/v1/messages", {
  method: "POST",
  headers,
  body: JSON.stringify({
    model: CFG.model,
    max_tokens: max,
    system: agent.prompt,
    messages: [{ role: "user", content: userText }]
  })
});
```

- Inside claude.ai artifacts the key is handled for you.
- Opened as a local file, you need your own key plus the `anthropic-dangerous-direct-browser-access` header. That is fine for a personal demo but **never ship a real key in client-side code**. Use a backend proxy for anything public.

---

## 7. Sample run (simulated)

I could not call the live API from the sandbox, so I played each agent by hand with the app's prompts. The default brief was Tidy Ledger, a bookkeeping app for freelance designers.

| Round | Score | Change |
|---|---|---|
| 1 | 67 | n/a |
| 2 | 78 | +11 |
| 3 | 86 | +8 |
| 4 | 91 | +5, threshold hit |

Stop reason: threshold. Final headline: "Tax season, minus the panic."

Note the shrinking gains each round. That pattern is typical and is why the plateau rule exists.

---

## 8. Common pitfalls

- **Score inflation**: a lenient Evaluator ends the loop too early.
- **Context bloat**: passing the whole history to every agent grows cost fast. Pass only what each agent needs.
- **Silent regression**: a rewrite can lose strengths. Keep the best draft, not the latest.
- **Invented facts**: copy agents love fake statistics. Say "never invent statistics, testimonials or awards" and check with a Safety agent.
- **No exit condition**: without a cap, a bug or a stubborn Evaluator loops forever.

---

## 9. Extension ideas

- Add a second, independent judge to reduce scoring bias.
- Run two Executors in parallel and let the Evaluator pick the stronger start.
- Add a brand-voice corpus for the Evaluator to compare against.
- Add a human-approval gate between rounds and save runs to IndexedDB.
- Add a Router agent that picks which agents to use based on the brief.
- Feed real A/B test results back into memory.
- Experiment: compare plateau deltas of 0.5, 1.5 and 3 across 10 briefs, and chart cost against score.

---

## 10. Key takeaways

1. A multi-agent system is a **set of focused prompts plus an orchestrator** that owns state.
2. **Separate generating from judging.** It is the most useful pattern in the project.
3. **Autonomy needs exit conditions**: success, plateau and a hard cap.
4. **Compact memory** beats full history.
5. **Reliability work** (retries, JSON repair, logging) matters as much as the prompts.
6. Always **keep the best result**, not just the latest.

---

## 11. Practice tasks for tomorrow

- [ ] Run the app with your own API key and a different brief.
- [ ] Change `delta` to 0.5 and then 3, and note how the round count changes.
- [ ] Rewrite the Evaluator prompt to be more lenient, and watch the loop stop early.
- [ ] Add a seventh scoring dimension to the rubric and update the Evaluator JSON.
- [ ] Sketch the loop on paper without looking at the code.
