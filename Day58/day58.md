# Day 58 (Project Day 8): Testing, Debugging and Production Hardening

**Project:** ShortlistIQ, a placement shortlisting tool where rules decide eligibility and AI only judges resume fit.
**Live app:** https://shortlistiq-sigma.vercel.app/
**Repo:** https://github.com/Rashmichaudhary1408/shortlistiq

## Goal

Review the whole app as if it launches publicly tomorrow, find what could break, and fix it without adding new features.

## Status

| Step | Status |
|---|---|
| Release-readiness review (QA, software engineering, security, performance) | Done |
| Fix package built: 10 files replaced, 7 new | Done |
| New logic checked outside the project: 24 checks on parsing, matching, the fallback scorer, the AI circuit breaker and the Gemini wrapper | Passed |
| Fixes applied to the repo | [ ] |
| `npm test` (expected: 20 files, 115 tests) | [ ] |
| `npm run build` | [ ] |
| Deployed to Vercel | [ ] |
| Manual QA sheet run on the live site (`docs/test-log.md`) | [ ] |

Applying, verifying and deploying the fixes continues on the next day.

## What the review found

| # | Area | Problem | Severity |
|---|---|---|---|
| 1 | API | A slow AI call could outrun Vercel's 30-second limit and return a bare platform error | Medium |
| 2 | Security | The public health check called the AI on every refresh, so anyone could burn the free quota | Medium |
| 3 | Security | No security headers (framing, content sniffing, referrer, permissions) | Medium |
| 4 | Compatibility | The Basic match scorer used a regex feature that older Safari cannot parse | Medium |
| 5 | Data import | Resume column values like `resumes\A1.pdf` or `A1` (no extension) never matched their file | Medium |
| 6 | Data import | A spreadsheet with a title line above the headers failed with "Missing required column(s)" | Medium |
| 7 | Accessibility | The two file pickers had no labels for screen readers | Medium |
| 8 | UX | If nobody could be scored, Start screening was disabled with no explanation | Low |
| 9 | UX | Reloading or closing the tab silently lost all uploaded data | Low |
| 10 | Performance | When the AI quota ran out, every resume tried three times, so a big run could take minutes | Medium |
| 11 | Maintenance | The pdf.js worker file was copied by hand and could drift from the installed version | Low |

## Checked and found fine

- **Excel export:** text that starts with `=` is stored as plain text, so the file cannot run formulas.
- **API key:** it stays on the server (no `NEXT_PUBLIC_` prefix) and `.env.local` was never committed.
- **Logs:** the server logs only error codes and durations, never resume or job description text.
- **Rendering:** React escapes everything it displays, including AI output.
- **Prompt injection:** the AI returns facts, a fixed formula computes the score, and a skill only counts with evidence.

## Risks I accepted

- The per-IP rate limit is per server instance and trusts a forwarded header, so it is advisory. With a free key and a Basic match fallback, the worst case is that scoring degrades.
- Drives are saved in one browser only. The home page, the export and the README all say so.

## The fix package

- **Replaced (10):** `next.config.mjs`, `health/route.js`, `drive/new/page.js`, `RunStep.js`, `UploadStep.js`, `fallbackScore.js`, `matchResumes.js`, `parseStudents.js`, `runner.js`, `server/gemini.js`
- **New (7):** `scripts/copy-pdf-worker.mjs`, `docs/test-log.md`, and five test files (`gemini`, `matchResumesPaths`, `fallbackScoreEdge`, `parseMatrix`, `runnerBreaker`)
- **Also:** one `package.json` setting so the pdf.js worker is copied after every install

## Screenshots to add

Add these to `Day58/screenshots/` after the fixes are applied:

- `tests-passing.png` (`npm test` with 20 files and 115 tests)
- `build-passing.png` (`npm run build`)
- `security-headers.png` (browser Network tab showing `x-frame-options`)
- `nothing-to-score.png` (Run step message)
- `live-qa-results.png` (the filled-in QA sheet or the live app after the fixes)
- `linkedin-poster.png`

## Key learnings (draft, edit in your own words)

- **Passing tests do not mean the product is safe.** The suite passed at every step, and a review from a QA, security and performance point of view still found 11 issues.
- **Public endpoints on a free key need protecting.** Anyone can open a public link, so the quota needs a cache, a rate limit and a fallback.
- **Real spreadsheets are messy.** Title rows above the headers and folder paths in a column are normal, not rare.
- **Compatibility is a feature.** One modern regex feature would have crashed the fallback on older phones.
- **Fail cleanly inside the time you have.** A planned time budget gives people a clear message instead of a platform error.

## Free tools used

Next.js, React, Tailwind CSS, Google Gemini API (free tier), SheetJS, pdf.js, Vitest, GitHub and Vercel Hobby. No paid service and no Anthropic API key.

## Next

Apply and verify the fixes, deploy, run the live QA sheet, then write `DAY8-SUMMARY.md`, `SETUP.md` and `ENVIRONMENT.md`.
