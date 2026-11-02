# Day 52: System Design

**Challenge:** AB Talks 60-Day Claude AI Challenge · Capstone Day 2 of 10
**Project:** ShortlistIQ, an AI-assisted resume screening system for college placement cells

## What I did today
Turned the Day 1 plan (PRD, Implementation Blueprint, Pitch Deck) into a complete technical design. No application code was written; today was about making every build decision before building.

## Design decisions

| Area | Decision |
|---|---|
| Frontend | Next.js (App Router), JavaScript, Tailwind CSS |
| Backend | Three small Next.js serverless routes: health, extract-skills, score-resume |
| Database | None on the server; saved drives live in browser localStorage |
| Authentication | None (a PRD decision); input limits and rate limiting protect the public routes |
| AI | Google Gemini free tier, model name kept in an environment variable, with a keyword fallback scorer |
| Hosting | Vercel Hobby plan, deployed from GitHub |

**Key principles**
- Rules decide eligibility; AI judges fit.
- AI returns evidence for each skill; the final score is computed in code with a fixed formula.
- Resume PDFs never leave the browser.
- Every failure path (AI busy, unreadable PDF, full storage) has a defined, visible outcome.

## Deliverables created
| File | What it covers |
|---|---|
| `ARCHITECTURE.md` | Tech stack rationale, component diagram, data flow, request lifecycle, AI interaction, security, failure modes |
| `SCHEMA.md` | Data model (JSON documents), ER diagram, constraints, validation against all 10 user stories |
| `API.md` | The 3 endpoints with validation, error codes and examples, plus client-side module contracts |
| `UI-WIREFRAMES.md` | Screen inventory, user flow, screen flow, low-fidelity wireframes, navigation |
| `PROJECT-STRUCTURE.md` | Folder tree, responsibilities, dependency rules, which day creates which file |

## Issues found during design review
- Schema validation against the user stories found 3 gaps: cancelled runs could leave half-scored data, draft drives were never requested by the PRD, and saved drives had no version field for future changes.
- The Blueprint's example rate limit (60 requests per 10 minutes) could block a legitimate 50-student run, so 150 per 10 minutes is proposed.
- Today's "no production code" rule moves the Blueprint's old Day 2 code tasks to Day 3, so a re-baselined schedule was proposed.

## Proposed changes to the Blueprint (status)
| # | Change | Status |
|---|---|---|
| PC-1 | Re-baseline the schedule (setup code to Day 3, upload UI to Day 4, storage to Day 5, drop optional chart) | Pending approval |
| PC-2 | Server-only code in `src/lib/server/` with the `server-only` package | Pending approval |
| PC-3 | Error `code` field, 150 requests per 10 minutes, request guard built with the first routes | Pending approval |
| PC-4 | `schemaVersion`, save only completed drives, cancelled runs not saved | Pending approval |
| PC-5 | `docs/planning/` and `docs/design/` layout, separate `wizardReducer.js` | Pending approval |

## Day 3 readiness
About 44 hours of work remain against 40 to 48 hours available, so the plan is feasible with little slack. The first cuts if time runs short are the optional chart, the JD eligibility hints, and the search box. Day 10 is a feature freeze and acts as the buffer.

## Project repo
- Repository: `<link to shortlistiq repo>`
- Today's commit: `<link to commit>`

## Checklist
- [ ] GitHub repo `shortlistiq` created and cloned
- [ ] Next.js starter and folder skeleton created
- [ ] Five design documents committed under `docs/design/`
- [ ] Updated Blueprint committed (after approvals)
- [ ] Project log updated
- [ ] Changes pushed to both repos
- [ ] LinkedIn post and poster published
- [ ] Commit URL submitted

## What I learned
- A design review is the cheapest time to change your mind.
- Checking a design against every user story exposes gaps early.
- Deciding where secrets, data and logic live makes later days much simpler.
