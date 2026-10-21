# Day 40 — AI Assistant Builder: Screenwise

**Date:** October 21, 2026
**Task:** Use the "AI Assistant Builder" prompt to interview-design, then build, a domain-specific AI assistant as a single-file HTML app with live Claude API calls.
**Result:** **Screenwise: Resume Screening Check**, a tool that shows how a resume reads to an applicant tracking system (ATS) and a recruiter for one specific role, then tells you what to fix first.

---

## 1. Goal

Build a purpose-built assistant (not a generic chatbot box) by letting Claude interview me, then generate:

1. A production-quality **system prompt** (the assistant's "brain")
2. A **self-contained HTML interface** with a premium, domain-matched UI
3. A collapsible **"How this was built"** documentation panel

---

## 2. Process

| Step | What I did | Status |
|------|-----------|--------|
| 7 | Pasted the AI Assistant Builder prompt and answered Claude's MCQ interview, one question at a time | Done |
| 8 | Claude generated the complete HTML application | Done |
| 9 | Published the artifact from the dropdown so it runs inside Claude.ai (no API key needed) | Done |
| 10 | Noted: downloading or self-hosting the HTML requires a real Anthropic API key | Noted |
| 11 | Tested the assistant with a sample resume and job description | Done |
| 12 | Reviewed the generated system prompt | Done |
| 13 | Explored the "How this was built" documentation panel | Done |
| 14 | Took screenshots | Done |

---

## 3. Interview Answers

The answers below are inferred from the finished app. Edit any that don't match what you picked in the quiz.

| # | Question | Answer |
|---|----------|--------|
| 1 | Domain → niche | Careers → resume / ATS screening for a specific target role |
| 2 | Audience and key outcome | Job seekers; one session gives a clear score and a prioritised list of what to fix to match a specific job posting |
| 3 | Inputs | Form fields (target role, seniority) plus pasted job description and pasted resume |
| 4 | Output | Score/verdict plus a structured report with recommendations and reasoning |
| 5 | Tone | _[your choice, e.g. professional / blunt-expert]_ |

---

## 4. What Was Built

### 4.1 Inputs (left panel)
- **Target role** text field (tested with *Product Marketing Manager*)
- **Seniority** segmented toggle: Entry / Mid / Senior / Lead (tested with *Mid*)
- **Job description** and **Your resume** text areas, each with a live word counter (92 and 120 words in the test)
- **Switch theme** control for dark and light modes

### 4.2 Output (right panel and below)
- **Overall score dial:** 58 out of 100, with the verdict **"Needs work"** and a short summary of the candidate's fit
- **Five sub-score bars**, each with a one-line explanation:

| Dimension | Score |
|-----------|-------|
| Keyword and skill match | 52 |
| Relevance and seniority fit | 58 |
| Impact | 55 |
| ATS readability | 80 |
| Clarity and concision | 62 |

- **Keywords from the posting** as tags: green for matched (HubSpot, product launch, sales team, product managers, customer feedback, Google Analytics, copywriting, dashboard) and red for missing or underplayed (positioning and messaging, go-to-market strategy, competitive analysis, win/loss and customer research, sales enablement, SQL or dashboards, adoption and pipeline metrics, cross-functional leadership). Selecting a red tag explains why the term matters.
- **Resume, marked up:** the resume text highlighted in three colors: *works well* (green), *vague or weak* (amber), *relevant but underplayed* (red). Selecting a highlight shows a note and a suggested rewrite.
- **What to fix first:** a ranked action list, each item with the problem and the concrete fix:
  1. Reframe experience around product marketing responsibilities
  2. Expand the launch bullet (38% trial signup growth) into a full case study
  3. Surface research, competitive and data skills, without claiming experience you lack

### 4.3 System prompt (the brain)
Reviewed for these parts:
- **Role:** expert resume reviewer thinking like both an ATS and a recruiter
- **Scope:** one resume against one specific role and posting
- **Constraints:** never invent experience; recommend only facts the user can verify
- **Output format:** structured data the UI can render into the dial, sub-scores, tags, highlights and action list
- **Edge cases:** irrelevant input, missing information, abuse

### 4.4 Documentation panel
A collapsible "How this was built" section covering system prompt design, why the UI fits the use case, and how to extend it with tools, memory and multi-step flows.

---

## 5. Screenshots

**1. Inputs, overall score dial and first sub-scores**
![Score and breakdown](screenshots/01-score-and-breakdown.png)

**2. ATS readability, clarity, keyword tags and resume markup**
![Keywords and markup](screenshots/02-keywords-and-markup.png)

**3. Remaining markup and the "What to fix first" list**
![Fix first](screenshots/03-fix-first.png)

---

## 6. Testing

| Test | Observed |
|------|----------|
| Valid role, JD and resume | Score of 58 with "Needs work" verdict, sub-scores, keywords, highlights and fix list all rendered |
| Honest grounding | Fixes tell the user not to claim experience they lack |
| Interactive elements | Red tags and highlights are selectable for explanations and rewrites |
| Missing info, empty submit, off-topic or abusive input | _[add result if you tested these]_ |

---

## 7. Key Learnings

- Interviewing first (MCQ, one question at a time) produced a design far more specific than a one-shot prompt.
- A structured output format in the system prompt is what lets the UI show a score dial, tags and highlighted text instead of plain chat.
- The domain shaped the UI: resume checking needs the original text marked up in place, with colors that mean something.
- Honesty constraints in the prompt (no invented experience) make the advice trustworthy.
- Inside Claude.ai the API call is handled automatically. Outside it, a real API key is required, and in production it belongs on a backend proxy, not in client-side code.

---

## 8. Next Steps

- Add **tools** (parse uploaded PDF/DOCX resumes, fetch a job posting from a URL)
- Add **memory** (save past scans and show score progress over time)
- Add **multi-step flows** (check, rewrite bullets, re-score)
- Add export of the report and a rewritten resume
- Move API calls behind a backend before deploying publicly
