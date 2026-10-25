# Day 44: Build an AI-Powered LinkedIn Profile Optimizer

**Turn Your LinkedIn into a Recruiter Magnet**

**Date:** 25 October 2026
**Author:** Rashmi Chaudhary
**Goal:** Use AI to audit, rebuild and activate my LinkedIn profile for software and AI/ML internships.

---

## 1. What I Built Today

An AI-powered LinkedIn Profile Optimizer. It takes a real profile as input and produces:

- An honest **roast** with a score for every section
- A complete **rebuild** of headline, About, experience and skills
- A **before vs after scorecard**
- A **7-day activation plan** with ready-to-post drafts
- A shareable **summary card**

The output is a single interactive HTML app, plus a poster that summarizes every result.

## 2. The Idea

Most profiles fail in the first 3 seconds. Recruiters scan the headline and the first two lines of About, then decide whether to keep reading. This project plays the role of an ex-recruiter who has reviewed thousands of profiles. It quotes your own words back at you, explains why they hurt, and rewrites them with the reasoning shown, so you learn personal branding instead of just copy-pasting.

## 3. How the Workflow Runs

| Step | What happens |
|------|--------------|
| 1 | Prompt acts as a LinkedIn expert, personal branding consultant and ex-recruiter |
| 2 | It collects 5 inputs: headline, About, latest experience, top skills, target goal |
| 3 | Part 1: Roast (score out of 10 per section, plus a recruiter's 3-second reaction) |
| 4 | Part 2: Rebuild (3 headline options, new About, experience rewrite, skills) |
| 5 | Part 3: Before vs after scorecard |
| 6 | Part 4: 7-day activation plan |
| 7 | Part 5: Summary card to screenshot and post |

**Rule that makes it trustworthy:** use only the information provided. Never invent achievements, roles, companies or metrics. If something is missing, suggest what to add, and mark it as a blank to fill in.

## 4. Steps I Followed

1. Pasted the prompt into Claude.
2. Answered the interview questions (uploaded my LinkedIn profile PDF, then chose my goal: **Job / Internship**).
3. Generated the complete HTML application.
4. Saved the generated HTML file (`rashmi-linkedin-roast.html`).
5. Opened it locally in the browser.
6. Tested the workflow by clicking through all five tabs, with no errors.
7. Took screenshots and made a poster of every result.

## 5. Results

### Score: 42/100 → 80/100 (+38)

| Section | Before | After |
|---------|:------:|:-----:|
| Headline | 5/10 | 8/10 |
| About: first 2 lines | 3/10 | 8/10 |
| About: full section | 5/10 | 8/10 |
| Experience | 3/10 | 7/10 |
| Skills & keywords | 4/10 | 8/10 |

These are AI-assessed scores. The "after" numbers assume I fill in the blanks (hackathon name, GitHub link, real IBM topics) truthfully.

### Top 3 Mistakes Found

1. **Hedge words in the headline.** "Aspiring" and "Enthusiast" say what I hope to be, not what I have done. The headline also said "Intern @ IBM" although that entry ended in August 2026.
2. **My best project was buried.** The Smart Intelligence Guard hackathon result sat in the middle of About, while the opening lines were a generic list of interests.
3. **Top skills didn't match my goal.** Prompt Engineering and Generative AI were pinned, while Python, Machine Learning and SQL were only plain text inside About, so they weren't searchable skill tags.

### Other Findings

- About text ran together with no line breaks ("Problem SolvingI have").
- Two IBM bullets repeated each other, and none described a tool, task or output.
- "Generative AI for Web Developers" is a course title, not a skill.

## 6. The Rebuild (Highlights)

**Headline (keyword-optimized):**

> Computer Science Student (B.Tech '28) | Python · Machine Learning · Computer Vision · SQL | Hackathon 2nd Runner-Up | Seeking SWE & AI/ML Internships

**About hook (the part visible before "see more"):**

> I built an AI system that watches a mall in real time, spots suspicious activity, captures a screenshot, and alerts security. It placed 2nd Runner-Up at a hackathon.

**Experience:** retitled to "AI Virtual Intern (IBM SkillsBuild / FSP)" so it is accurate, and merged the repeated bullets.

**Skills:** pin Python, Machine Learning, Computer Vision. Add DSA, SQL, OpenCV, C++, Git & GitHub, Data Analysis. Demote Prompt Engineering and remove the course-title skill.

## 7. The 7-Day Activation Plan

| Day | Action |
|-----|--------|
| 1 | Apply all profile changes (10-item checklist) |
| 2 | Publish Post #1: "I let AI roast my LinkedIn profile" |
| 3 | Send 10 strategic connection requests (note under 300 characters) |
| 4 | Leave 5 value comments: Agree + Add Insight + Ask a Question |
| 5 | Publish Post #2: hot take on "Aspiring" in student headlines |
| 6 | Reply to every comment, send 5 more requests |
| 7 | Review profile views, search appearances and acceptance rate, then adjust |

## 8. Key Learnings

- **Lead with proof, not a title.** A concrete result beats a list of interests.
- **Headline and first two lines carry most of the weight.** Treat them as ads.
- **Skills tags are search filters.** Text in About does not count as a skill.
- **Be honest about what the experience was.** Calling a virtual internship what it is builds trust.
- **A profile is only half the job.** Posting, commenting and connecting are what get it seen.
- **Prompt rules matter.** "Never invent metrics" is what keeps AI output usable on a real profile.

## 9. Tech and Tools

- Claude (prompt-driven interview, analysis and rewrite)
- Single-file HTML, CSS and vanilla JavaScript (tabs, copy buttons, animated score bars, saved checklist)
- Playwright headless Chromium (to test the app and render the poster)

## 10. Files Produced

| File | Purpose |
|------|---------|
| `rashmi-linkedin-roast.html` | Interactive optimizer app |
| `rashmi-linkedin-poster.png` | Poster of all results, for sharing |
| `rashmi-linkedin-poster.pdf` | Printable version of the poster |
| `day44.md` | This log |

## 11. How to Run It

1. Download `rashmi-linkedin-roast.html`.
2. Double-click it to open in Chrome or Edge. No install or internet is needed.
3. Use the five tabs: Roast, Rebuild, Scorecard, 7-Day Plan, Summary.

## 12. Next Steps

- [ ] Fill in the blanks: hackathon name, GitHub link, real IBM topics, project metrics
- [ ] Apply the Day 1 checklist to my live profile
- [ ] Publish Post #1 and Post #2
- [ ] Re-run the optimizer after one week and compare scores
- [ ] Turn the prompt into a reusable tool that accepts any profile

## 13. Share-Ready Summary

> I let AI roast my LinkedIn profile today. Here's what changed:
>
> Before: 42/100
> After: 80/100
>
> Top 3 mistakes I was making:
> 1. Hedge words ("Aspiring", "Enthusiast") in my headline
> 2. My best project was buried instead of opening my About
> 3. My top skills didn't match the jobs I want
>
> The #1 thing that made the biggest difference: opening with proof (my hackathon-placing project) instead of a title.

`#Day44` `#LinkedIn` `#AI` `#PersonalBranding` `#Internships`
