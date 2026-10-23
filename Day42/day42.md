# Day 42: AI Productivity Applications

## Build Personal Financial Command Center
### Create Your AI-Powered Financial Dashboard

---

## 1. Goal for today

Use an AI assistant to design and build a complete, working financial dashboard as a single HTML file, without writing the code by hand. By the end of the day I should have:

- A personalised dashboard that runs offline in any browser
- A financial health score and rule-based recommendations
- What-if simulations to test money decisions
- A poster summarising the results of every step

**Skills practised:** structured prompting, interview-style prompting, specifying a product (not just code), testing AI output, turning results into a shareable summary.

---

## 2. Key idea: let the AI interview you first

The prompt did not ask for a dashboard straight away. It told Claude to **ask questions one at a time, as multiple choice, before building anything**. This works because:

- A generic dashboard fits nobody. Personal details (income, goals, living situation) drive every design choice.
- Multiple choice is fast to answer and keeps answers consistent.
- Typed input only as the last option still leaves room for anything unusual.
- Claude decides when it has enough information, so the interview adapts to the answers.

**Pattern to reuse:** *Role + interview rules + build instructions + constraints.*

---

## 3. The prompt structure

| Part | What it did |
|---|---|
| **Role** | Financial planner, budgeting specialist, designer, data-visualisation expert and senior front-end developer, all in one |
| **Interview rules** | One question at a time, MCQ only, typed answer as last option |
| **Build spec** | Overview dashboard, then modules chosen for the user's profile |
| **Features** | Charts, health score, AI recommendations, what-if simulations, progress tracking |
| **Closing content** | Tips, checklists, resources, extra AI prompts for learning |
| **Constraints** | One self-contained HTML file, no libraries, dark mode, local storage, printable, responsive |

The constraints matter most for portability: one file with no dependencies means it opens by double-click and never breaks when a library changes.

---

## 4. My interview answers

| Question | Answer |
|---|---|
| Who is the dashboard for? | Student |
| Main source of money | Parents / family support |
| Level of study | Undergraduate (college) |
| Where do you live? | Hostel / PG |
| Monthly money | ₹5,000 to ₹10,000 |
| Biggest struggle | Not saving anything |
| Main saving goal | Trips and experiences |
| Design approach | Let Claude design it automatically |

Seven short answers were enough to shape the whole product: a small monthly budget in rupees, a trip-focused goal, and a strong push on saving habits.

---

## 5. What was built

**File:** `personal-financial-command-center.html` (one file, about 20 KB, zero libraries)

### Modules

1. **Overview**: trip progress track, health score, monthly summary, spending donut chart, weekly spending bars, top recommendations
2. **Money**: set the monthly allowance, add and delete expenses
3. **Budget**: a limit and progress bar per category (red when over)
4. **Goals**: multiple goals with progress and an estimated completion date
5. **What-if**: sliders that recompute the goal date instantly
6. **Insights**: recommendations generated from the user's own numbers
7. **Learn**: hostel-budget tips, a planning checklist, resource links, copyable AI prompts

### Built-in extras

- Dark mode that follows the system setting and can be toggled
- Data saved in the browser's local storage
- A print-friendly layout for a full report
- Responsive layout for phone and desktop

### How the health score works (out of 100)

| Part | Points | Full marks when |
|---|---|---|
| Saving rate | 40 | You save 20% or more of your allowance |
| Budget discipline | 30 | No category is over its limit |
| Goal progress | 15 | Goals are at least half funded on average |
| Tracking habit | 15 | You log 12 or more expenses a month |

---

## 6. Results with the demo data

The app opens with sample data (₹7,500 allowance, October 2026) designed to show room for improvement. I ran the app's own calculation code on it, so these are the real numbers it produces.

| Measure | Result |
|---|---|
| Total spent | ₹7,099 |
| Left to save | ₹401 (about 5% of allowance) |
| Health score | **41 / 100** (Needs attention) |
| Score breakdown | Saving 11/40, Budget 13/30, Goals 2/15, Tracking 15/15 |
| Categories over limit | Food and mess, Snacks and delivery, Fun and social, Other |
| Goa trip (₹12,000, ₹1,500 saved) | About 27 months away at the current pace |

### Top recommendations produced

- Save about ₹1,125 a month (15%) and move it on the day the allowance arrives
- Snacks and delivery are ₹850 over limit; halving them frees about ₹925 a month
- Start a small emergency fund, even ₹500

### What-if results (Goa trip)

| Scenario | Months to reach ₹12,000 |
|---|---|
| Today's pace | 27 |
| Halve delivery spending and use a 6.5% recurring deposit | 8 |
| The above, plus ₹1,000 a month from tutoring | 5 |

**Lesson:** one small habit change (ordering less delivery) moves the trip from more than two years away to under a year.

---

## 7. Step-by-step workflow I followed

1. Pasted the Personal Financial Command Center prompt into Claude
2. Answered the interview questions one at a time
3. Let Claude generate the complete HTML application
4. Saved the file as `personal-financial-command-center.html`
5. Opened it locally by double-clicking
6. Explored every module (Overview, Money, Budget, Goals, What-if, Insights, Learn)
7. Reviewed the health score and recommendations
8. Tried the what-if sliders
9. Captured results as a poster (`financial-command-center-poster.png`)

**Note:** the poster was drawn from the numbers the app's code computed, because a real browser was not available to take screenshots. To capture true screenshots, open the HTML file in a browser and screenshot each tab.

---

## 8. Prompting lessons

1. **Interview before building.** Questions first gives a personalised result instead of a template.
2. **Constrain the output.** "Single file, no libraries" produced something easy to share and run.
3. **Describe the outcome, not the code.** The prompt named modules, behaviours and quality (premium, responsive, dark mode) and left the code to the AI.
4. **Ask for judgement features.** A score, recommendations and what-if tools turn a tracker into a decision-making tool.
5. **Verify results.** Running the logic and checking the numbers showed what the app really does, rather than trusting the description.
6. **Know the limits.** The recommendations are rules based on the user's data, not a live AI, and the tool is educational, not financial advice.

---

## 9. Practice tasks

- [ ] Replace the demo expenses with your real spending for two weeks
- [ ] Set your own category limits in the Budget tab
- [ ] Rename the Goa goal to your real trip and set its true cost
- [ ] Use What-if to find the cheapest habit change that gets you there in under 6 months
- [ ] Switch to dark mode and print a report as a PDF
- [ ] Re-run the prompt choosing a different profile (Freelancer or Family) and compare the modules
- [ ] Try the "customise modules" route and choose only three modules

### Stretch challenges

- Add a "no-spend days" counter to the Money tab
- Add a monthly history chart comparing this month with last month
- Ask the AI to add CSV export, then review the code it writes

---

## 10. Prompts to keep

```
Explain how a recurring deposit works, with a ₹1,000 a month example, in simple words.
```
```
I get ₹7,500 a month in a hostel. Build me a weekly spending plan that saves ₹1,500.
```
```
Compare an RD, a liquid fund and a savings account for a 6-month trip fund.
```
```
Review the code of my dashboard and list three bugs or improvements, ordered by impact.
```

---

## 11. Reflection

- What surprised me most about the interview approach?
- Which single spending habit costs me the most?
- If I saved the suggested 15% for a year, what would I afford?
- What would I change in the prompt to get an even better dashboard?

---

## 12. Files from today

| File | Purpose |
|---|---|
| `personal-financial-command-center.html` | The dashboard application |
| `financial-command-center-poster.png` / `.svg` | Poster of every step's result |
| `day42.md` | These notes |

*Disclaimer: the dashboard is an educational tool, not professional financial advice. Interest rates shown are illustrative, so check current rates with your bank.*
