# Day 13: AI-Powered Job Search with Claude and the Indeed Connector

## Objective

Use Claude with the Indeed connector to turn a resume into a targeted job search. The goal was a ranked list of matching roles, a skill-gap analysis, market demand insights, and a report I could save and share.

## Tools Used

- **Claude** for profile building, analysis and report generation
- **Indeed connector (MCP)** for live job search and job details
- **Resume (PNG)** as the source for my professional profile

## Workflow

1. Opened Claude and went to **Connectors**.
2. Connected the **Indeed** connector and signed in to my Indeed account.
3. Started a new conversation.
4. Ran three prompts in order:
   - **Prompt 1: Professional profile.** Role, experience, skills, domain, location and achievements.
   - **Prompt 2: Job search criteria.** Target titles, company types, work mode, salary, exclusions and posting recency.
   - **Prompt 3: Job discovery and analysis.** Search, rank, filter, then produce the table and the analysis.
5. Reviewed match scores, skill gaps and market demand insights.
6. Exported the results as a designed HTML report and took screenshots.

## Inputs

My Indeed account had no resume or saved preferences, so Claude asked for my details. I uploaded my resume instead. The profile Claude built from it:

| Field | Value |
|---|---|
| Status | B.Tech CSE student (2024–2028) |
| Focus | AI/ML, computer vision, NLP |
| Core skills | Python, OpenCV, YOLO, scikit-learn, DSA, OOP, Git, Firebase |
| Experience | Two virtual AI/ML internships (IBM SkillsBuild, AICTE) |
| Projects | Smart Intelligence Guard, Fake News Detection, Chest X-Ray Classification |
| Achievement | 2nd Runner-Up among 200 finalist teams at the IIMT Hackathon |

Search criteria assumed: AI/ML and Python internships, Delhi NCR or remote, posted in the last ~30 days, pay shown as stipend.

## Results

Claude ran several Indeed searches, read the full listings for the strongest candidates, and excluded stale or ineligible ones.

| Company | Role | Location | Match | Pay |
|---|---|---|---|---|
| HelixBeat | Data Scientist Intern | Remote | 92% | Not listed |
| Labour Laws India | AI/ML Intern | North Delhi | 90% | ₹5,000/month |
| WeIntern | AI/ML Intern | Remote | 88% | ₹10,000–20,000/month |
| Welldone Healthcare | AI/ML/Python Developer Intern | Remote | 70% | ₹4,057–6,799/month |
| Appnox Technologies | Full Stack + AI Trainee | Noida | 55% (stretch) | ₹10k–20k/month, then ₹3.6–5 LPA |

Excluded: SmartBridge (graduates only, 2 months unpaid) and listings posted before Mar 2026.

## Key Insights

**Most requested skills:** Python, ML fundamentals, scikit-learn, Pandas/NumPy, Git/GitHub, OpenCV and SQL.

**My skill gaps:**
- Pandas, NumPy and Matplotlib are missing from my resume
- PyTorch or TensorFlow
- A RAG or LLM project
- Django or FastAPI and REST APIs
- Statistics, Docker and cloud

**Market demand:**
- Remote AI/ML internships are plentiful, but most pay ₹5k–20k a month.
- GenAI and RAG skills now show up even in intern listings.
- Computer vision plus healthcare is a niche where my projects stand out.

## Action Plan

- [ ] Add NumPy, Pandas, Matplotlib and PyTorch to the resume (only what I've actually used)
- [ ] Add a GitHub link and demo video for Smart Intelligence Guard
- [ ] Finish the Chest X-Ray project and report AUC and Grad-CAM results
- [ ] Build a small RAG chatbot with FastAPI
- [ ] Apply to 15–20 roles a week, starting with the top three matches

## Learnings

- Connectors let Claude work with live data instead of guesses.
- Reading the full job description changed the ranking. One role looked ideal in search but accepted only graduates.
- Data from job boards can be inconsistent. One listing showed a yearly pay figure that contradicted its stated monthly stipend, so I checked the description.
- A resume is a much better input than a typed summary, and the analysis got sharper once Claude had it.

## Deliverables

- `Rashmi_Job_Search_Report.html`: the designed report with the ranked table, skills analysis and recommendations
- Screenshots of the report

---

