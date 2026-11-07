# Day 7 — Product Refinement & User Experience

**Project:** ShortlistIQ  
**Sprint focus:** Product refinement, usability, feedback, accessibility, and resilient UI states  
**Date:** 7 November 2026

## Overview

Day 7 focuses on making the existing ShortlistIQ workflow easier to understand and safer to use without changing the product's core purpose: helping recruiters or placement teams shortlist students using explicit eligibility rules and explainable resume-fit evidence.

This document is based on the supplied `day7-changes.zip` and the supplied one-page PDF snapshot of the ShortlistIQ home page. The PDF is a rendered application page, not the 10-Day Sprint Workbook. Therefore, this file documents the visible/code-backed Day 7 changes but does not claim to verify the workbook's exact task list.

## Product and UX improvements represented in the supplied changes

### 1. Home page and drive management
- Retains the existing ShortlistIQ positioning and four-step workflow.
- Shows a clearly labelled example result using fictional candidate data.
- Adds a loading skeleton while saved drives are being retrieved.
- Provides an empty state with a clear action to start the first drive.
- Displays storage/read errors as visible alerts.
- Adds a confirmation dialog before deleting a saved drive.
- Uses toast feedback after successful or failed delete actions.

### 2. Screening run experience
- Adds a step-progress indicator with the current step identified accessibly.
- Shows screening progress through a semantic progress bar and live status text.
- Provides a cancel action during a run.
- Presents distinct completion, partial/fallback, save-error, and run-error states.
- Keeps an Excel export action available after a completed run.

### 3. Results and candidate review
- Adds summary and result-loading UI.
- Supports filtering by all candidates, shortlisted, eligible but not shortlisted, resume issues, and ineligible.
- Supports searching by candidate name or student ID.
- Allows the shortlist size (Top N) to be adjusted.
- Allows manual include/exclude overrides from the results table.
- Adds a candidate details drawer with resume evidence indicators.
- Provides an Excel export action with an in-progress state and success/error feedback.
- Explains when keyword-based fallback scoring was used instead of AI scoring.

### 4. Reusable UI and accessibility
- Adds reusable confirmation dialog, score bar, skeleton, toast, drive card, and stepper components.
- Uses accessible labels, live regions, dialog semantics, progress semantics, and button states in the supplied components.
- Adds subtle drawer/toast motion and a reduced-motion fallback in the supplied stylesheet.
- Includes dedicated error and not-found pages.

## Files included in `day7-changes.zip`

The ZIP contains these 16 project files. Extract them into the root of the existing Next.js project and allow the files to merge into the matching folders.

```text
src/
  app/
    drive/[id]/page.js
    error.js
    globals.css
    layout.js
    not-found.js
    page.js
  components/
    layout/
      Header.js
    results/
      CandidateDrawer.js
      ResultsTable.js
    ui/
      ConfirmDialog.js
      DriveCard.js
      ScoreBar.js
      Skeleton.js
      Toast.js
    wizard/
      RunStep.js
      Stepper.js
```

**Important:** The supplied ZIP contains only the files listed above, not a complete application repository. It imports other project modules/components (for example, storage, shortlist, export, summary-card, and wizard components) that must already exist in the project. Do not delete or replace other files based only on this ZIP.

## Apply the changes

1. Make a backup or commit the current working version of the project.
2. Download and extract `day7-changes.zip`.
3. Copy the extracted `src` folder into the root of the existing project.
4. When Windows asks whether to replace files, choose **Replace the files in the destination** for the matching paths.
5. Open the project folder in VS Code.
6. In the VS Code terminal, run:

```bash
npm install
npm run lint
npm run build
npm run dev
```

If the project does not define a `lint` script, skip `npm run lint` and run the build. Do not add or change dependencies until checking the existing `package.json`.

7. Open `http://localhost:3000` and test the checklist below.
8. Only deploy after the local build and manual checks pass.

## Day 7 verification checklist

- [ ] Home page loads without a runtime error.
- [ ] Saved drives load, and the loading skeleton is visible while loading.
- [ ] Empty state appears when there are no saved drives.
- [ ] Delete action asks for confirmation before deleting.
- [ ] Success and error toast messages are readable and dismissible.
- [ ] New-drive wizard progress is clear at desktop and mobile widths.
- [ ] Screening progress, cancel, completion, fallback, and error states behave correctly.
- [ ] Results summary and candidate rows load correctly.
- [ ] Search works by candidate name and student ID.
- [ ] Each result filter returns the expected candidates.
- [ ] Top N can be edited without input snapping unexpectedly.
- [ ] Manual shortlist include/exclude overrides persist after refresh.
- [ ] Candidate details drawer opens, displays evidence, and closes correctly.
- [ ] Excel export downloads a valid workbook.
- [ ] Missing-drive and not-found pages provide a working route back.
- [ ] Keyboard focus, dialog labels, live announcements, and reduced-motion behavior are usable.
- [ ] Layout is checked at narrow mobile, tablet, and desktop widths.

## Known verification limits

The supplied ZIP and PDF were inspected as source artifacts. They do not prove that the changes have been installed into the full repository, that all imported modules are present, that the application builds, or that the deployed Vercel site has been updated. Those checks require the complete repository and a local build/test run.

The supplied PDF shows the home page, example results, workflow explanation, and past drives. It does not contain the 10-Day Sprint Workbook. Upload the workbook if the Day 7 task list must be checked item by item against the original sprint plan.

## Suggested Git workflow

After local checks pass:

```bash
git status
git add src
git commit -m "Improve ShortlistIQ Day 7 product UX"
git push origin main
```

If the project uses a different default branch, replace `main` with that branch name. Deploy through the existing Vercel project after the push, then verify the production URL.

## Day 7 outcome

The supplied changes represent a usability and resilience pass across the home page, screening flow, and candidate results experience. The goal is to make progress visible, actions safer, candidate decisions easier to inspect, and errors easier to recover from—while preserving ShortlistIQ's explainable, rules-first shortlisting approach.

## Next milestone

**Day 8 objective:** Follow the Day 8 section of the 10-Day Sprint Workbook. Do not begin Day 8 work until the Day 7 implementation is installed, built, manually tested, and deployed (if the project is ready for deployment).
