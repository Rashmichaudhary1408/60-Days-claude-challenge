# Day 26: Build a Prior Authorization Workflow Simulator

**Learn healthcare workflows through interactive gameplay.**

A single-file, browser-based game that simulates the US healthcare **Prior Authorization (PA)** process. Players drag a patient case through the Patient, Provider and Payer lanes, build the PA request, and handle the payer's decision, while learning why each step matters.

---

## What Is Prior Authorization?

Prior authorization is a requirement from health insurers (payers) that a provider get approval *before* delivering certain services, such as surgeries, advanced imaging, specialty drugs and some hospital admissions. It exists to control costs and confirm medical necessity, but it can delay care and add administrative work. This simulator makes that process visible.

---

## Features

- **Three workflow lanes:** Patient, Provider and Payer
- **Drag-and-drop case movement** between stages, with a button fallback
- **Four patient scenarios:**
  - Elective knee replacement
  - Lumbar spine MRI
  - Specialty medication (biologic)
  - Inpatient admission
- **Medical necessity evaluation:** choose the clinical findings that support the request
- **Document collection:** drag or click to assemble the PA packet (required vs. irrelevant files)
- **Submission to payer**
- **Review outcomes:** Approval, Pend, Denial, Appeal and Peer-to-Peer Review
- **Educational explanation** after every step
- **Progress tracker** across the top
- **Days elapsed counter** and **efficiency score**
- **Celebration animation** on approval
- **Workflow summary** with a timeline and grade on completion
- **Restart / New Patient** buttons
- Responsive layout in shades of blue with black text

---

## Tech Stack

| Item | Choice |
|------|--------|
| Language | HTML, CSS, vanilla JavaScript |
| Dependencies | None (no frameworks, no CDNs, no build step) |
| Storage | None. All state lives in JavaScript memory |
| File | `pa_workflow_simulator.html` (single file) |

Scenario data is stored in an editable `SCENARIOS` array near the top of the script, so you can add or change patients without touching the game logic.

---

## How to Run

1. Download `pa_workflow_simulator.html`.
2. Open it in any modern browser (Chrome, Edge, Firefox, Safari).
3. Pick a patient scenario and start playing.

---

## How to Play

1. **Choose a patient** from the scenario picker.
2. **Drag the case** from *Visit & Order* to *Medical Necessity*.
3. **Select the findings** that support medical necessity, then confirm.
4. **Collect documents:** add every required document to the packet and skip the irrelevant ones, then finalize.
5. **Submit** by dragging the case to *Payer Review*.
6. **Handle the decision:**
   - **Approved:** celebrate and view the summary.
   - **Pended:** send the requested additional information.
   - **Denied:** choose Peer-to-Peer or a formal Appeal.
7. **Review the summary** for total days, efficiency score, grade and timeline.
8. Press **New Patient** to try another scenario.

### Scoring

- You start at **100** efficiency points.
- Each elapsed day, incorrect selections, unneeded documents and out-of-order moves reduce the score.
- Faster, cleaner submissions earn a better grade.

---

## Scenario Outcomes

| Scenario | Payer Path | Lesson |
|----------|-----------|--------|
| Knee replacement | Denial, then Peer-to-Peer overturns it | Conservative therapy must be documented |
| Lumbar MRI | Pend, then Approval | Missing details cause delays |
| Specialty drug | Denial, Peer-to-Peer upheld, then Appeal approved | Step therapy and escalation paths |
| Inpatient admission | Approval | Emergency care and notification rules |

---

## Learning Objectives

- Understand the roles of the patient, provider and payer in PA
- Recognize what makes a strong medical necessity case
- See why complete documentation reduces pends and denials
- Compare Peer-to-Peer review with formal appeals
- Appreciate how PA delays affect patients and staff

---

## Customizing

Add a new patient by adding an object to `SCENARIOS`:

```js
{
  id: 'example',
  icon: '🩺',
  name: 'Example Procedure',
  patient: 'Name, Age',
  service: 'Service description (CPT code)',
  path: ['pend', 'approve'],   // payer outcomes in order
  p2pWins: true,               // does peer-to-peer overturn a denial?
  crit: [{ t: 'Supports necessity', ok: true }, { t: 'Irrelevant', ok: false }],
  docs: [{ n: 'Clinical notes', req: true }, { n: 'Unneeded file', req: false }],
  why: 'Explanation shown for the denial.'
}
```

---

## Screenshots

Add your screenshots to this folder and reference them here:

```md
![Scenario picker](screenshots/picker.png)
![Workflow in progress](screenshots/workflow.png)
![Approval celebration](screenshots/approval.png)
![Workflow summary](screenshots/summary.png)
```

---

## Repository Structure

```
Day26/
├── day26.md
├── pa_workflow_simulator.html
└── screenshots/
```

---

## Disclaimer

This is an educational simulation. Payer rules, timelines and criteria vary widely by insurer, plan and state, and the scenarios are simplified. It is not medical, legal or billing advice.

---

## Key Takeaway

Prior authorization is a coordinated workflow across three parties. Complete, accurate clinical documentation at the start is the most effective way to shorten the path to care.
