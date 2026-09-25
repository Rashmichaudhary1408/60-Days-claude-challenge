# Day 14 – AI Job Red Flag Detector 🚩

## 🎯 What is this task?

Today's goal was to build an **AI-powered Job Red Flag Detector** using Claude — a tool that analyzes a job description and company information, then tells you how risky or safe that opportunity really is before you spend time applying.

In simple words: instead of blindly applying to any job you find online, you paste in the **Job Description** and **Company Information**, and Claude acts like an experienced career advisor — scanning for warning signs like hidden salary info, unrealistic requirements, toxic culture language, fake "remote" claims, and company stability risks.

---

## 🛠️ Tools Used
- **Claude** (AI Assistant by Anthropic)
- A custom prompt: **"Job Red Flag Detector"**
- A self-contained **HTML/CSS/JS dashboard** built by Claude to visualize the results

---

## 📋 How I Did It (Step-by-Step)

1. Opened Claude and used the Job Red Flag Detector prompt.
2. Pasted a real **Job Description** (AI Engineer role) and asked Claude to analyze it.
3. Pasted the matching **Company Information** and had Claude combine both into a full risk report.
4. Asked Claude to turn the analysis into a **visual dashboard** — with a risk score gauge, red flags, positive signals, and interview questions — instead of plain text.
5. Ran the same detector across multiple companies: **Microsoft, Google, and OpenAI**.
6. Reviewed the final interactive report and downloaded it as a standalone HTML file.

---

## 📊 What Claude Found (Summary Across Companies)

| Company | Risk Score | Verdict |
|---|---|---|
| Microsoft | 41/100 | ⚠️ Apply with Caution |
| Google | 32/100 | ⚠️ Apply with Caution |
| OpenAI | 38/100 | ⚠️ Apply with Caution |

### 🚩 Notable Red Flags
- **Microsoft** — Recurring layoff history in recent years, even alongside strong AI investment; stack-ranked performance reviews (Connects) can create internal competition.
- **Google** — Inflated requirements for supposedly standard roles (PhD or 8+ years); brutal 5–7 round hiring loops with high candidate ghosting after the onsite.
- **OpenAI** — Compressed shipping timelines around major releases; complex equity (PPUs) that's poorly explained before the offer stage; "remote-friendly" postings with a strong cultural pull back to the office.

### ✅ Positive Signals Found
- All three companies had **transparent, well-documented tech stacks** in their postings.
- Strong compute/research infrastructure and genuine long-term AI investment.
- No manipulative buzzwords like "family culture" or fake "unlimited PTO."
- Reasonable to strong compensation structures relative to market.

---

## ❓ Smart Interview Questions Claude Suggested (Sample)

1. What does the first 90-day roadmap look like — is scope already defined?
2. How has this specific team been affected by recent company-wide layoffs?
3. Is remote work genuinely supported long-term, or expected to shift to onsite?
4. How is performance actually evaluated — output, impact, or a forced ranking system?
5. What percentage of the team has been here longer than two years?

---

## 💡 What I Learned

- AI tools like Claude can be used **before** applying to a job, not just for resumes or cover letters.
- A job that sounds great on paper can still carry real risk — vague scope, hidden salary info, or unstable company history.
- Turning a text report into an **interactive dashboard** made the findings far easier to compare across companies at a glance.
- Always validate red flags directly in the interview — don't assume the best based on the posting alone.

---

## 📌 Status
✅ Task Completed — Day 14