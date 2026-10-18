# Day 37: Build Task Compass

**Learn How Work Flows Through Real Organizations**

---

## Today's Goal

Build **Task Compass**, a single-file HTML game that teaches how work moves through an organization: ownership, delegation, collaboration, escalation and workflow. It should feel like a management simulation, not a quiz.

**Workplace explored:** Tech Company

---

## What I Built

A self-contained app using only HTML, CSS and vanilla JavaScript. It has no libraries, no APIs, and works completely offline.

| Stage | Name | Tickets | What the player does |
|-------|------|---------|----------------------|
| 1 | Who Owns This? | 3 | Drags one role card into the ownership slot |
| 2 | Task Routing | 3 | Places roles in order to build a workflow (3 to 5 steps) |
| 3 | Collaboration Challenge | 3 | Assigns up to four roles to a larger situation |

**Roles in the Tech Company:** Frontend Developer, Backend Developer, QA Engineer, Product Manager, UX Designer, Customer Support, Engineering Manager, DevOps / SRE.

---

## How the Game Works

1. **Stage 1:** a ticket appears, for example "Payments fail only on iPhones". After submitting, the game reveals the primary owner, why they own it, and which roles may assist. It never just says right or wrong.
2. **Stage 2:** the player orders the roles, and the slots light up one by one as the ticket moves through the organization. The game then explains why that order is commonly used.
3. **Stage 3:** the player picks a primary owner plus supporting roles. The result shows the primary owner, supporting teams, reasoning and a possible communication flow.
4. **Dashboard:** instead of points, the player sees understanding in four categories, drawn as a radar chart and bars.

---

## Scoring Categories

- **Ownership:** did I recognise who should hold the problem first?
- **Delegation:** did I involve sensible people at each step?
- **Collaboration:** did I make room for supporting teams?
- **Workflow Thinking:** did I sequence handoffs the way work commonly travels?

The final reflection covers what I understood well, where I tended to over-assign, where I underestimated collaboration, and one insight about organizations.

---

## Key Design Choices

- Dark mode with glassmorphism and an animated gradient background
- Each role is a collectible-style card with its own department colour
- Tasks look like work tickets (`TICKET #1040`)
- Drag and drop, with tap-to-place as a fallback for touch screens
- Snap animations, hover lift, a progress bar, soft sounds and confetti at the end
- All scenarios live in JavaScript arrays (`S1`, `S2`, `S3`), so adding more is easy
- Cautious wording ("often", "commonly", "may") because real teams differ

---

## What I Learned

- Ownership gives a problem direction. It does not mean working alone.
- The right order of handoffs matters, and short chains tend to suit emergencies.
- Bigger problems, such as a satisfaction drop or a delayed feature, usually need several teams.
- Involving too many people adds coordination cost, and involving too few hides useful perspectives.
- Many real workplace problems are solved by teams rather than individuals.

---

## Challenges

- Fitting the whole game into one small file, so I limited each stage to 3 tickets instead of cutting features.
- Making drag and drop work on touch devices, which needed click-to-place as a fallback.
- Writing feedback that explains reasoning instead of just marking answers correct or wrong.

---

## How to Run

1. Paste the Task Compass prompt.
2. Choose a workplace type.
3. Generate the complete HTML application.
4. Save the file as `task-compass.html`.
5. Open it locally in your browser.
6. Complete Stage 1, Stage 2 and Stage 3.
7. Review your Organizational Thinking Dashboard.
8. Replay using another workplace type.
9. Take screenshots.

---

## Extras

- Made a poster that shows every step and every kind of result in the game.

---

## Next Steps

- [ ] Add more tickets per stage (the plan was 8 to 10)
- [ ] Try other workplaces: Startup, Hospital, Café / Restaurant, Media Agency
- [ ] Add a "shuffle tickets" option for replays
- [ ] Share screenshots of the dashboard


