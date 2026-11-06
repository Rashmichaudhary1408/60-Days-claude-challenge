# Day 56: Complete the MVP and Deliver a Working Demo

**Live app:** https://shortlistiq-sigma.vercel.app/
**Repo:** https://github.com/Rashmichaudhary1408/shortlistiq

## What I built today

- Scoring engine: PDF text reading in the browser, a fixed scoring formula, and a free keyword fallback ("Basic match")
- `/api/score-resume` route using Google's free Gemini API
- Run step with a progress bar, a cancel button, retries and fallback
- Results page with Top N, manual Add and Remove, a detail panel and an Excel export
- Drives saved in the browser, with a home page listing past drives
- Footer: "Built with Claude as part of the AB Talks 60-Day Claude AI Challenge."
- Deployed to Vercel (free Hobby plan) with the Gemini key stored as an environment variable

## Screenshots

- screenshots/01-upload.png
- screenshots/02-skills.png
- screenshots/03-rules.png
- screenshots/04-live-results.png
- screenshots/05-live-health.png
- screenshots/06-detail-panel.png
- screenshots/07-home-with-drive.png
- screenshots/08-excel.png

## Key learnings

- [Write one thing you learned about rules versus AI, for example why the score is computed in code and not by the AI]
- [Write one thing you learned about debugging, for example how a small file-name typo broke the build]
- Free API tiers have rate limits, so a fallback path keeps the app working when the AI is busy.
- Secrets like API keys belong in environment variables, never in the code or GitHub.