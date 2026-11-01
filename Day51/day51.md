# Day 51: Product Discovery & Sprint Planning

**Challenge:** AB Talks 60-Day Claude AI Challenge · Capstone Day 1 of 10
**Project:** ShortlistIQ, an AI-assisted resume screening system for college placement cells

## What I did today
- Was interviewed one question at a time by Claude (as co-founder, product mentor and technical lead) until the idea, user, scope and success criteria were clear.
- Narrowed a broad idea ("AI resume screening for recruiters") into a focused product for **one user: the college placement officer**.
- Approved a one-paragraph project summary, then generated three deliverables.

## The project in one paragraph
ShortlistIQ turns a campus drive's pile of resumes into a ranked, explainable shortlist. The officer uploads a student spreadsheet and resume PDFs named by student ID, pastes the job description, and reviews the AI-extracted skills. Four configurable eligibility rules (minimum CGPA, allowed branches, maximum backlogs, graduation year) are applied first, and every rejected student sees the exact rule they failed. Only eligible students' resumes are scored against the skills, with a fallback scorer if AI is unavailable. The officer gets a ranked table, a detail view, manual override, Top N, spreadsheet export and saved past drives.

## Key insight
**Rules for eligibility (deterministic and explainable) + AI for skill fit (judgment) + the officer in control.**

## v1.0 includes
Spreadsheet and PDF upload · JD skill extraction with officer editing · four eligibility rules with defaults · failed-rule reasons · AI scoring with fallback · ranked table and candidate detail · manual override and Top N · .xlsx export · saved past drives · warnings for missing or unreadable resumes · public deployment with README.

## Intentionally left out of v1.0
Login and accounts · student portal · automatic emailing · side-by-side comparison · OCR for scanned PDFs · Word resumes · drives above about 50 students · extra eligibility rules. (Score distribution chart is an optional Day 9 extra only.)

## Day 10 success looks like
1. Deployed at a public link
2. Upload, JD and skill editing work
3. Eligibility rules apply with exact failed-rule reasons
4. Ranked results with a detail view
5. Override, Top N and export work
6. Past drives can be reopened
7. Missing and unreadable resumes show warnings, no crash
8. Code and README on GitHub, and a 3-minute live demo is ready

## Deliverables created
| Deliverable | File |
|---|---|
| Product Requirements Document | `ShortlistIQ_PRD.docx` |
| Implementation Blueprint (Days 2-10) | `ShortlistIQ_Implementation_Blueprint.docx` (+ `.md` copy) |
| Project Pitch Deck | `ShortlistIQ_Pitch_Deck.pptx` |

## Screenshots
- [ ] Interview conversation
- [ ] Approved project summary
- [ ] PRD
- [ ] Implementation Blueprint
- [ ] Pitch Deck

## What I learned
- A narrow user and a clear differentiator make a 10-day project realistic.
- Deciding what to leave out is as important as deciding what to build.
- Writing success criteria on Day 1 gives every later day a finish line.
