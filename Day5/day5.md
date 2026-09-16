# Day 5 — Context vs No Context in Prompting

## 🎯 Task

The goal of Day 5 was to understand how providing **context** changes the quality and personalization of an AI-generated response.

I created two prompts for generating a **30-day learning roadmap**:

* **Prompt A:** Without personal context
* **Prompt B:** With personal context

I then compared both outputs to understand the impact of context on AI responses.

---

# 📝 Prompt A — Without Context

### Prompt

> Create a 30-day learning roadmap.
>
> Include:
>
> * Weekly milestones
> * Daily tasks
> * Resources
> * Projects
> * Final outcome
>
> Make it practical and beginner-friendly.

### Purpose

This prompt provides the AI with the basic requirements but does not provide information about the learner.

The AI therefore has to create a **general-purpose roadmap** that could work for a wide range of beginners.

### Output 1 — Screenshot

![Prompt A Output](output1.png)

---

# 📝 Prompt B — With Context

### Prompt

> Create a 30-day learning roadmap.
>
> Context:
>
> * Current Situation: Student
> * Current Skills: Python, C++, basic Machine Learning, Git/GitHub
> * Goal: Become a Software Engineer with AI/ML skills
> * Available Time: 2–3 hours per day
> * Experience Level: Beginner
> * Preferred Learning Style: Projects + Videos
>
> Include:
>
> * Weekly milestones
> * Daily tasks
> * Resources
> * Projects
> * Final outcome
>
> Make it practical and beginner-friendly.

### Purpose

This prompt gives the AI information about my current situation, skills, goal, available time, experience level, and preferred learning style.

Because of this additional information, the AI can create a roadmap that is more relevant to my individual needs.

### Output 2 — Screenshot

![Prompt B Output](output2.png)

---

# 🔍 Comparison of Both Outputs

## 1. Which roadmap feels more personalized?

**Prompt B's roadmap feels more personalized.**

Prompt A only knows that the learner is a beginner, so the resulting roadmap is relatively general.

Prompt B provides additional information such as:

* Current skills
* Career goal
* Available study time
* Experience level
* Learning preferences

This allows the AI to adjust the roadmap according to the learner's actual situation.

---

## 2. Which roadmap would I actually follow?

I would follow **Prompt B's roadmap** because it is more closely aligned with my current skills and career goal.

The roadmap can be structured around my existing knowledge instead of starting completely from scratch.

It also considers the amount of time I can dedicate each day and my preferred learning style.

This makes the roadmap more realistic and easier to follow consistently.

---

## 3. What role did context play in improving the result?

Context played an important role in improving the output.

### Without Context

The AI had limited information about the learner.

Therefore, it had to make assumptions and create a general roadmap.

### With Context

The AI had more information about:

**Who I am →** Student

**What I know →** Python, C++, basic ML, Git/GitHub

**Where I want to go →** Software Engineering + AI/ML

**How much time I have →** 2–3 hours/day

**How I prefer to learn →** Projects + Videos

This allowed the AI to generate a roadmap that was more specific and relevant.

---

# 📊 Side-by-Side Comparison

| Feature                  | Prompt A — Without Context | Prompt B — With Context                  |
| ------------------------ | -------------------------- | ---------------------------------------- |
| Personalization          | Low                        | High                                     |
| Understanding of learner | Limited                    | Detailed                                 |
| Career alignment         | General                    | Goal-oriented                            |
| Daily schedule           | Generic                    | Can match available time                 |
| Learning style           | Generic                    | Customized                               |
| Difficulty               | Beginner-friendly          | Beginner-friendly + personalized         |
| Projects                 | General                    | More relevant to goals                   |
| Resources                | General                    | Can be selected according to preferences |
| Practicality             | Good                       | More realistic for the learner           |
| Overall usefulness       | General                    | More personalized                        |

---

# 🧠 Key Learnings

### 1. Context improves personalization

Providing information about the user helps AI generate responses that are more relevant to their situation.

### 2. Specific prompts reduce assumptions

When the AI knows my skills, goals, time availability, and experience level, it has less need to make assumptions.

### 3. The same task can produce different results

Both prompts asked for a 30-day learning roadmap, but the outputs were different because the second prompt contained more context.

### 4. Context makes AI more useful

A general answer can provide a starting point, but a contextualized answer can better match an individual's needs.

### 5. Prompt engineering is iterative

A good first prompt does not always produce the best result. Adding useful context and refining the instructions can improve the output.

---

# 💡 Main Takeaway

The biggest lesson from Day 5 is:

> **Context transforms a generic AI response into a more personalized and actionable response.**

Prompt A tells the AI **what to create**.

Prompt B tells the AI **what to create and who it is creating it for**.

The more relevant context we provide, the better the AI can tailor the response to our specific requirements.

---

# 📸 Outputs

### Output 1 — Without Context

![Output 1](output1.png)

### Output 2 — With Context

![Output 2](output2.png)

---

# 🚀 Final Reflection

This activity helped me understand why **context is an important part of prompt engineering**.

Instead of simply asking AI to complete a task, providing information about the user's background, current skills, goals, constraints, and preferences can make the response significantly more relevant.

**Day 5 completed ✅**

**60 Days Claude Challenge — Day 5/60**
