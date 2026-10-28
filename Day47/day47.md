# Day 47: Build Content Intelligence Studio

**Topic:** Create an AI-powered content analysis platform

## What it is

Content Intelligence Studio is a single-file web app (`content-intelligence-studio.html`) that reviews an Instagram post before it goes live. You upload an image and paste a caption. A panel of AI reviewers looks at the picture itself, reads the caption, and returns a score, a rewrite and a publishing checklist.

## How it works

The app sends your image and caption to Claude (model `claude-sonnet-4-6`) in two stages.

**Stage 1: four specialist reviewers, run in parallel**

| Reviewer | What it judges |
|---|---|
| Visual Stopping-Power Analyst | Focal point, composition, contrast, text legibility at thumbnail size, safe zones for 4:5, 1:1 and 9:16 crops |
| Caption and Hook Copywriter | First-line hook, clarity, voice, call to action, hashtags, how words and image work together |
| Reach and Algorithm Strategist | Likelihood of sends, saves, shares and comments from non-followers; format fit for the goal |
| Audience Psychology Reviewer | Curiosity, emotional triggers, social currency, trust cues, accessibility |

Each reviewer returns a score from 0 to 100, a verdict, reasoning, strengths, weaknesses, missed opportunities and recommendations.

**Stage 2: two senior leads, run in parallel**

- **Lead Strategist** reads the four reviews and produces the overall score, an executive summary, a health report, the top four improvements, a reach rating (Low, Moderate, High or Very High) and a performance estimate.
- **Creative Director** produces a rewritten caption, 5 alternative hooks, 4 on-image titles, 4 visual fixes, an 8-point checklist, a before/after summary and 4 follow-up prompts.

## Features

- Drag-and-drop or click-to-upload image input, resized to 1568px and sent as JPEG
- Choice of platform (feed post, Reel cover, carousel cover, Story) and goal (reach, followers, sales, authority)
- Four review styles: Gentle, Balanced, Strict and Brutal
- Live pipeline view showing each reviewer as waiting, reviewing, complete or failed
- Activity log, automatic retries on network errors and rate limits, and a retry button for failed stages
- Animated score ring and category bars; click a bar to open that reviewer's findings
- Before vs after caption comparison with a copy button
- Interactive publishing checklist with a progress bar
- Download or copy the full report as a `.txt` file
- Light and dark theme, responsive layout, reduced-motion support

## Running it

1. Open the HTML file in a browser.
2. Inside Claude, it works as is. Outside Claude, open "API key (optional)" at the top right and paste an Anthropic API key. The key stays in the tab's memory only.
3. Upload an image, add a caption, choose platform, goal and review style, then click **Analyze content**.

## Design notes

- Plain HTML, CSS and JavaScript in one file, with no build step or dependencies.
- The model replies in labeled plain text (`SCORE:`, `VERDICT:` and so on) rather than JSON. A small parser reads the labels, which tolerates formatting drift better than strict JSON.
- Rendering uses `textContent` and DOM nodes rather than `innerHTML`, so model output cannot inject markup.
- Performance predictions are labeled as AI estimates, not measurements.

## Deliverables for the day

- `content-intelligence-studio.html`: the app
- `content-intelligence-poster.html`: a poster page for the project
- `content-intelligence-poster.png`: the poster as an image (scores on it are sample values)
- `day47.md`: this file

## Takeaways

- Splitting one big review into specialist roles gives more focused feedback than a single prompt.
- Running independent reviewers in parallel, then combining them, keeps the wait short.
- A fixed output format with a forgiving parser makes AI output easy to turn into a dashboard.
- Retries and per-stage retry buttons keep one failed call from ruining the whole run.
