# Day 59 (Project Day 9): Launch and Production Readiness

**Project:** ShortlistIQ, a placement shortlisting tool where rules decide eligibility and AI only judges resume fit.
**Live app:** https://shortlistiq-sigma.vercel.app/
**Repo:** https://github.com/Rashmichaudhary1408/shortlistiq
**Launch commit:** [`ce13d52`](https://github.com/Rashmichaudhary1408/shortlistiq/commit/ce13d52), merged into `main`

## Goal

Treat the project as if it launches publicly today: close the gaps between "it works" and "a stranger can trust it".

## Status

| Step | Status |
|---|---|
| Day 8 hardening fixes applied to the repo | [x] |
| `npm test`: 20 files, 115 tests | [x] passed |
| `npm run build`: 14 routes including `/privacy`, `/robots.txt`, `/sitemap.xml` | [x] passed |
| Launch commit pushed and merged into `main` (`b86e42f..ce13d52`) | [x] |
| Live site shows the new metadata, privacy page and footer link | [x] checked on the deployed pages |
| LinkedIn Post Inspector shows the preview card, title and description | [x] |
| Wrong `og:url` on every page: one-line fix in `layout.js` | [ ] found on the live site, not applied yet |
| Security headers visible in the browser (F12, Network) | [ ] |
| Lighthouse (mobile): Performance ___  Accessibility ___  Best practices ___  SEO ___ | [ ] |
| QA sheet in `docs/test-log.md`, rows 1 to 16 | [ ] |
| One full run on the live site: Method shown [ ] AI  [ ] Basic match | [ ] |
| GitHub About, topics and social preview image | [ ] |
| `v1.0.0` release tag | [ ] |

## What I did for launch readiness

| Area | What changed |
|---|---|
| Hardening (Day 8 fixes) | Security headers, a health check that cannot burn the free AI quota, retries planned inside the 30 second limit, a Basic match scorer that works on older Safari, resume paths and title rows handled, a circuit breaker so a run finishes when the AI quota is gone |
| Branding | New favicon, browser tab icon and iPhone home-screen icon from the ShortlistIQ mark |
| Sharing | A 1200 by 630 preview card with alt text, plus Open Graph and Twitter card tags |
| Search | Site title and description, `robots.txt`, a sitemap, and `noindex` on private drive pages |
| Trust | A plain-language `/privacy` page, linked from the footer, saying where resume data goes |
| Openness | MIT license, a rewritten README, `docs/SETUP.md` and `docs/ENVIRONMENT.md` |
| Tidiness | Removed five unused starter images, added package description, license and repository fields |

**Size of the change:** 41 files changed, 1,047 lines added, 90 removed. 115 tests cover the logic, up from 92.

## A bug that only the live site showed

After deploying, I read the live page source. Every page, including `/privacy`, told social sites that its address was the home page, so a shared privacy link would have shown the home card. Local tests could not catch it. The fix is one line in `layout.js`, and it still needs applying.

## Screenshots to add

Add these to `Day59/screenshots/`:

- `tests-115-passing.png` and `build-14-routes.png`
- `live-home-with-icon.png` (the browser tab shows the new icon)
- `linkedin-post-inspector.png`
- `live-privacy-page.png`
- `security-headers.png` and `lighthouse-scores.png`
- `github-about-and-topics.png`
- `linkedin-poster.png`

## Key learnings (draft, edit in your own words)

- **Trust comes from the details around the product:** a privacy page, a license, a clear preview card and a setup guide matter as much as the features.
- **Check the deployed site, not just your machine.** Reading the live page source found a bug that tests and local builds could not.
- **Say where user data goes.** A tool that sends resume text to an AI service owes people a plain explanation of it.
- **Small automation prevents drift:** copying the pdf.js worker after every install means its version can never fall out of step.
- **Honest status beats a confident guess.** Marking a step as not yet done kept the record true.

## Free tools used

Next.js, React, Tailwind CSS, Google Gemini API (free tier), SheetJS, pdf.js, Vitest, GitHub and Vercel Hobby. No paid service and no Anthropic API key.

## Next: Day 10

Apply the share-address fix, finish the live checks above, add screenshots to the README, tag `v1.0.0`, and write the final summary.
