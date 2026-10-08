# Day 27: Build a Prior Authorization Story Simulator

**Learn healthcare workflows through interactive conversations.**

An interactive, chat-style story that follows a patient through the US Prior Authorization (PA) process. Instead of reading a textbook explanation, you watch a conversation between **Rahul**, a patient, and **Priya**, a healthcare operations specialist, and make choices that shape the dialogue along the way.

---

## The Story

Rahul visits City Medical Center, where Dr. Patel diagnoses him with Rheumatoid Arthritis and prescribes Humira. The story follows his medication through the insurance process across eight scenes:

| # | Scene | What You Learn |
|---|-------|----------------|
| 1 | Doctor Visit | Diagnosis and a specialty drug prescription |
| 2 | Insurance Roadblock | The provider submits the PA request to the payer (no pharmacy involved). Approved PAs are saved on file. |
| 3 | What is PA? | Plain-language PA and step therapy, and why delays matter |
| 4 | Insurance Review | Eligibility, clinical documentation, ICD-10 match, step therapy history |
| 5 | Denial | A denial is not permanent, and it has a real cost to staff time |
| 6 | Appeal | Gathering documents, a Letter of Medical Necessity, filing the appeal |
| 7 | Approval | Reference number issued, no repeat PA needed for Humira |
| 8 | Takeaways | Patient perspective and health-system perspective |

> **StarCare Health** is a fictional, illustrative payer. The reference number, timelines and scenarios are simplified for learning. Real plans and rules vary.

---

## Features

- **Chat-style storytelling** with an append-only message feed
- **Two characters:** 👦 Rahul (left) and 👧 Priya (right)
- **Narrator and doctor lines** shown as centered italic text, never as chat bubbles
- **Two choices after every scene** that change the dialogue and the story's tone
- **Progress bar and step dots** that update through all eight scenes
- **Typing indicator** before each message
- **Confetti celebration** on approval
- **Flow diagram:** Provider → PA Request → Payer
- **Two-perspective takeaways:** Patient and System
- **Restart button** to explore different dialogue paths
- Responsive layout in shades of blue with black text

---

## Tech Stack

| Item | Choice |
|------|--------|
| Language | HTML, vanilla JavaScript |
| Styling | Tailwind CSS via CDN, plus a small custom CSS block |
| Build step | None |
| Storage | None. State lives in JavaScript memory |
| File | `pa_story_simulator.html` (single file) |

### Implementation Rule

Every chat bubble, narration line and card is created with `document.createElement` and added with `appendChild`. The chat container is **never** set with `innerHTML =`. Restart clears it by removing child nodes one by one.

> Tailwind loads from a CDN, so you need an internet connection for the page to be styled.

---

## How to Run

1. Download `pa_story_simulator.html`.
2. Open it in any modern browser.
3. Press **Start the story**.

---

## How to Play

1. Read each scene as the conversation appears.
2. Follow Priya's plain-language explanations.
3. Pick one of the two choices after every scene.
4. Watch the progress bar and step dots advance through all eight scenes.
5. Reach the approval scene and enjoy the celebration.
6. Choose which takeaway to read first: **Patient** or **System**.
7. Press **Restart the story** and try different choices.

### How Your Choices Matter

- Early choices (curious vs. worried) change how Priya and Rahul speak in later scenes.
- Your denial and appeal choices change the explanation Priya gives next.
- The final choice sets the order of the takeaway cards.

---

## Learning Objectives

- Explain Prior Authorization in plain language
- Understand who submits a PA request and who reviews it
- Know the four common payer checks: eligibility, clinical documentation, ICD-10 match and step therapy history
- Recognize that a denial is not permanent and what an appeal involves
- See how health systems measure PA performance: **denial rate**, **appeal rate** and **resolution time**

---

## Sources and Notes

- *AMA 2023 PA Survey: PA causes treatment delays in the majority of cases.* (as cited in the story; verify against the original survey before publishing)
- *PA denials cost physician offices 2+ staff hours to resolve.* (figure used in the story; verify before publishing)
- This is an educational simulation, not medical, legal or insurance advice.

---

## Customizing

Edit the `SCENES` array near the top of the script. Each scene has lines and two choices:

```js
{ title: 'Scene Title',
  lines: [
    ['n', 'Narrator text'],              // centered italic text
    ['p', 'Priya says something'],       // right bubble
    ['r', flags => flags.worried ? 'Rahul (worried)' : 'Rahul (curious)']  // changes with earlier choices
  ],
  choices: [
    { label: 'Choice A', flag: 'curious', rahul: '...', priya: '...' },
    { label: 'Choice B', flag: 'worried', rahul: '...', priya: '...' }
  ] }
```

Line types: `n` narrator, `d` doctor, `r` Rahul, `p` Priya, `flow` diagram, `list` checklist card.

---

## Screenshots

Add your screenshots to a `screenshots/` folder and reference them here:

```md
![Start screen](screenshots/start.png)
![Insurance review](screenshots/review.png)
![Denial scene](screenshots/denial.png)
![Approval celebration](screenshots/approval.png)
![Takeaways](screenshots/takeaways.png)
```

---

## Repository Structure

```
Day27/
├── day27.md
├── pa_story_simulator.html
└── screenshots/
```

---

## Key Takeaway

Prior Authorization is not just paperwork. It is a process that affects how quickly patients get treatment and how much time health systems spend on administration. Clear communication and complete documentation help both.
