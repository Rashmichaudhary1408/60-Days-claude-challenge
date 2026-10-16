# Day 34: Marketing Detective (Full Task File)

## 1. Task Overview
Build **Marketing Detective**, a single-file HTML detective game that teaches marketing analysis, then create a poster showing all steps of the workflow.

**Roles Claude plays:** frontend developer, UX designer, instructional designer, marketing strategist.

## 2. The Original Prompt
> Ask the user to choose a color theme from a few presets (including Claude Orange).
> Create a beautiful single-file HTML application called "Marketing Detective". Use React via CDN + Babel. If React/Babel would prevent the app from running reliably as a standalone local HTML file, switch to pure HTML, CSS and vanilla JavaScript. Do not use Tailwind, npm, backend, APIs, databases, images or external assets.
> It should feel like a polished detective game, not a business dashboard. Every interaction should create curiosity before revealing the next clue.
> Generate 10 detailed fictional marketing cases (expand to 15-20 if quota allows), stored in a JavaScript array, with a random case on each replay.
> Design a premium dark detective look: corkboards, folders, sticky notes, push pins, paper textures, glowing accents, smooth transitions, hover effects, progress indicators, animated charts, responsive layout.
> Verify there are no syntax or runtime errors. Return ONLY the complete HTML file.

## 3. Requirements Checklist

### Case data (every case must contain)
- [x] Company Name
- [x] Industry
- [x] Campaign Objective
- [x] Target Audience
- [x] Marketing Channels
- [x] Budget Allocation
- [x] Campaign Metrics (Reach, CTR, Engagement, Conversions, Sales)
- [x] Customer Comments
- [x] Social Media Performance
- [x] One Primary Marketing Mistake
- [x] Three Supporting Clues
- [x] Correct Explanation
- [x] Suggested Improvements

### User flow
- [x] 1. Case Assignment
- [x] 2. Investigation Board
- [x] 3. Interactive Investigation with draggable evidence
- [x] 4. Solve the Case
- [x] 5. Case Closed animation
- [x] 6. Learning Report

### Design
- [x] Dark detective aesthetic
- [x] Corkboard, folders, sticky notes, push pins, paper texture
- [x] Glowing accents, transitions, hover effects
- [x] Progress indicator and animated bars
- [x] Responsive layout
- [x] Theme presets (Claude Orange, Noir Blue, Case Green, Crimson)

### Technical
- [x] Single HTML file, no npm, Tailwind, backend, APIs, databases, images or external assets
- [x] Vanilla JS used instead of React/Babel so it runs offline
- [x] Cases stored in a JavaScript array with random, non-repeating replay
- [ ] 15-20 cases (only 10 built so far)
- [ ] Tested in a real browser (not yet done)

## 4. The 12 Steps (Workflow)
| # | Step | What to do |
|---|------|-----------|
| 1 | Paste the prompt | Give the Marketing Detective brief to Claude |
| 2 | Generate the app | Claude writes the complete HTML application |
| 3 | Save the file | Save as `marketing-detective.html` |
| 4 | Open in browser | Double-click the file |
| 5 | Choose a theme | Pick Claude Orange, Noir Blue, Case Green or Crimson |
| 6 | Accept a case | Read the confidential case folder |
| 7 | Analyze evidence | Open budget, metrics, comments and social files |
| 8 | Drag evidence | Pin three key items to the cork board |
| 9 | Identify the mistake | Choose the primary marketing mistake |
| 10 | Review the verdict | See Case Closed or Case Cold and the explanation |
| 11 | Study the report | Read clues, fixes, score and detective rank |
| 12 | Replay | Play more random cases, then screenshot your results |

## 5. Task List (To-Do)
### Done
- [x] Ask user for a color theme
- [x] Build the game (10 cases, 6-stage flow)
- [x] Publish the game
- [x] Design a 12-step poster with illustrations and a case-flow strip
- [x] Write this task file

### Remaining
- [ ] Play through all 12 steps in a browser and note any bugs
- [ ] Add 5-10 more cases (target 15-20)
- [ ] Improve drag and drop on touch devices
- [ ] Take screenshots of each game screen
- [ ] Add the screenshots to the poster

## 6. Deliverables
| Deliverable | Location |
|-------------|----------|
| Game | https://claude.ai/artifact/CCbNSzq97eBELbhtMDk5Q2 |
| Poster | https://claude.ai/artifact/Rj6kpMUnJq13Wphhxo1Nfh |
| Game source file | `marketing-detective.html` |
| This task file | `day34.md` |

## 7. Marketing Mistake Types Used in the Cases
1. Wrong Audience Targeting
2. Mismatched Messaging
3. Wrong Channel Mix
4. Broken Conversion Funnel
5. Offer and Pricing Mismatch
6. Chasing Vanity Metrics

## 8. Scoring
- Correct verdict: 60 points
- Each correct clue pinned: 10 points (up to 30)
- Examining all evidence: 10 points
- Ranks: Rookie, Junior Sleuth, Senior Investigator, Master Detective

## 9. Lessons Learned
- Vanilla JS runs offline more reliably than React via CDN.
- A detailed user flow in the prompt gives a more complete app.
- Inline SVG can replace image files.
- Always test in a real browser before calling a project finished.
