Day 29: Build Operation Lifeline: Supply Chain Crisis Lab

Topic: Lead an enterprise through a supply chain crisis Deliverable: Operation_Lifeline.html, a single-file React simulator that runs by opening it in a browser

1. What you are building

A beginner-friendly game where you play the Chief Supply Chain Officer of a randomly generated company. A random crisis hits, and you must respond, negotiate with a supplier, answer the board, invest in AI, and then see how well you led.

Every playthrough is different: the company, the crisis, the starting numbers and the outcomes are all randomized.

2. Learning objectives

By the end of today you should be able to:

Explain what a supply chain is and why it breaks.
Describe the trade-offs between cost, speed, inventory and customer satisfaction.
Name common resilience tools: backup suppliers, safety stock, multi-sourcing, early-warning data.
Build a multi-screen React app in one HTML file using useState.
Design a scoring model that turns player choices into feedback.
3. Key supply chain vocabulary
Term	Plain meaning
Supply chain	The journey of a product from raw materials to factories, warehouses and customers
Lead time	Days between ordering and receiving
Inventory days	How long current stock lasts without new deliveries
Safety stock	Extra inventory kept for emergencies
Single point of failure	One supplier, route or site whose failure stops everything
Resilience	How well the business absorbs a shock and recovers
Expediting	Paying extra to speed up production or shipping
4. Simulation flow
Welcome: title, subtitle, Start Simulation.
Company profile: random industry, revenue, factories, warehouses, suppliers, inventory days, lead time, countries.
Crisis briefing: one of eight crises (factory fire, supplier bankruptcy, port strike, cyberattack, flood, raw material shortage, political conflict, shipping delay) with urgency, a clock and estimated weekly loss.
War Room: choose 3 of 6 actions. Animated bars show Cost, Inventory, Profit, Delivery Speed and Customer Satisfaction.
Negotiation: four branching rounds that move Trust, Price and Lead Time, with a live negotiation score.
CEO Boardroom: five multiple-choice leadership questions, scored 0, 1 or 2 points each.
AI Strategy: pick 2 of 5 investments (Demand Forecasting, Inventory Optimization, Supplier Risk Monitoring, Warehouse Vision, Procurement Copilot) and see expected impact.
Final dashboard: overall score (0 to 100), six sub-scores, best decision, biggest mistake, expert recommendation, lessons learned, replay.
5. Architecture

Everything lives in one HTML file:

React 18 and Babel loaded from the cdnjs CDN.
Plain CSS in a <style> block, with a dark enterprise theme using CSS variables.
Data tables (CRISES, ACTIONS, ROUNDS, QS, AIS) separate content from logic.
Reusable components: Tip, Bar, Steps, Stat.
Screen components: Welcome, CompanyScreen, CrisisScreen, WarRoom, Negotiation, Boardroom, AIStrategy, Dashboard.
App holds the current stage, the generated game g, and accumulated results res.
State pattern
jsx
const [stage, setStage] = useState("welcome");
const [g, setG] = useState(newGame);      // company + crisis
const [res, setRes] = useState({dec: []}); // results from each stage

Each screen receives a done(...) callback. It reports its results upward, and App moves to the next stage. This keeps screens independent and easy to test.

6. Randomization

newGame() picks a random crisis and company, then applies the crisis "hit" to baseline metrics:

js
start[k] = clamp(base[k] + crisis.hit[i] + random(-3, 3));

Action effects also get small random noise, and actions that fit the crisis get a 1.4x boost on their positive effects. So the same choices can give slightly different outcomes each run.

7. Scoring model
Score	Based on
Leadership	Boardroom points plus how many War Room actions fit the crisis
Negotiation	Trust, price index and lead time after four rounds
Resilience	Average of inventory and delivery speed, plus AI bonus
Cost Control	100 minus Cost, plus AI bonus
Risk Management	Boardroom, crisis fit, trust, plus AI bonus
Customer Satisfaction	Satisfaction metric plus AI bonus

The Overall Crisis Score is the average of the six. Grades: 80+ Crisis Commander, 60+ Capable Leader, below 60 Needs Training.

Every decision records a quality value q. The highest q becomes the best decision and the lowest becomes the biggest mistake.

8. Design principles used
Context before every decision: each screen opens with a "Why does this matter?" tip.
Plain language: jargon is defined in a glossary tip.
Feedback after every choice: the player learns why a choice was strong or weak.
Traffic-light bars: green is healthy, amber is risky, red is trouble. Cost is inverted because lower is better.
Progress stepper so the player always knows where they are.
Responsive grid and keyboard focus outlines, with motion reduced when the user prefers it.
9. How to run it
Save Operation_Lifeline.html.
Open it in Chrome, Edge, Firefox or Safari (internet needed on first load for the CDN scripts).
Click Start Simulation and play through all seven steps.
Click Replay to get a new company and crisis.
10. Test checklist
 Welcome button starts the game and a company is shown.
 Crisis screen shows urgency, clock and estimated loss.
 War Room allows exactly three selections and the Run button stays disabled until then.
 Bars animate after running the simulation.
 All four negotiation rounds work and the score updates.
 All five boardroom questions give feedback.
 AI Strategy allows exactly two selections.
 Dashboard shows the overall score and six sub-scores, with best decision and biggest mistake.
 Replay produces a different scenario.
 No errors in the browser console.
 Layout works on a phone-width window.
11. Lessons the simulation teaches
Speed, cost and customer happiness always trade off.
Backup suppliers and safety stock are insurance, cheap in good times and priceless in a crisis.
Trust with suppliers is built before the emergency.
Early-warning data and AI turn surprises into manageable problems.
Match the response to the type of crisis; no single action fits every disaster.
12. Stretch goals
Add a second crisis that hits mid-game.
Add a budget limit so every action has a price.
Save high scores with localStorage when running outside a sandbox.
Add a difficulty setting that changes crisis severity.
Add a printable summary of the final dashboard.
Bundle React locally for a fully offline version.
13. Reflection questions
Which action gave the best result for your crisis, and why?
When did saving money hurt you?
How did your negotiation style change trust and price?
Which AI investment would you pick for a real company, and why?
What would you fund first once the crisis is over?

Day 29 complete: you built an interactive enterprise crisis simulator with React, randomization, scoring and beginner-friendly guidance.