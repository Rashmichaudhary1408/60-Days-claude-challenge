Day 31: Build an AI Supply Chain Control Tower
Manage live disruptions like the Head of Operations
Overview
Today I used Claude to build AI Supply Chain Control Tower, an interactive operations-simulation game that runs entirely in a single HTML file (HTML, CSS and vanilla JavaScript only). No frameworks, no libraries, no backend, and it works fully offline.

You play the Head of Operations at a global logistics company. Alerts such as port congestion, supplier delays and truck breakdowns stream in. You have 3 minutes to prioritize them, choose the right corrective action and keep the business healthy.

Objective
Simulate real-world operational decision making under time pressure.
Practice prioritization when multiple incidents compete for attention.
See how each decision changes business KPIs.
Learn prompt-driven development by generating a complete app from one detailed prompt.
Features
Area	What it does
Live KPIs	Service Level, Customer Satisfaction, Inventory Health, Transport Efficiency, Operating Cost, Revenue Protected, Score, Remaining Time
Alert types	Port Congestion, Supplier Delay, Truck Breakdown, Warehouse Stock-out, Customs Inspection, Demand Spike, Factory Machine Failure, Weather Disruption, Wrong Inventory Count, Damaged Shipment
Player actions	Expedite Shipment, Use Backup Supplier, Reroute Trucks, Increase Production, Transfer Inventory, Approve Air Freight, Ignore, Delay Decision
Priority system	Critical (red, pulsing), High (orange), Medium (blue) with different rewards and penalties
Delayed consequences	Good decisions pay a bonus seconds later; weak or wrong ones cause rework or escalation
Rising difficulty	Alerts spawn faster and more stay active at once as time runs out
UI extras	Animated KPI cards, live event log, countdown timer, pause, help modal, sound toggle (visual only), responsive layout
End screen	Final score, grade (A+ to D), final KPIs, alerts resolved, correct and wrong decisions, summary, Play Again
Tech stack
HTML5
CSS3 (custom properties, grid, animations)
Vanilla JavaScript (modular functions)
One self-contained file: ai-supply-chain-control-tower.html
How the game logic works
Every alert type has one best action, one acceptable action and one wrong action.
Best decision: improves KPIs, adds score and revenue protected, lowers future risk, and later gives a "resilience dividend".
Acceptable decision: small gains, higher cost, and rework later.
Wrong decision (or Ignore): KPIs drop, cost rises, satisfaction falls, and an aftershock follows.
Delay Decision buys 8 extra seconds once, at a small penalty.
An alert that expires hurts Service Level and Customer Satisfaction.
A hidden risk value rises with bad decisions, which speeds up future alerts and shortens their timers.
Steps I followed
Pasted the full AI Supply Chain Control Tower prompt into Claude.
Generated the complete HTML application.
Saved the output as an .html file.
Opened it in the browser.
Read the instructions in the Help modal.
Monitored the incoming operational alerts.
Prioritized incidents based on urgency.
Chose the best corrective action for each one.
Observed the KPI changes after every decision.
Managed multiple alerts at the same time.
Completed the 3-minute simulation.
Reviewed the final performance dashboard.
Replayed to improve my score.
Took screenshots of the results.
Created the Day31 folder in my GitHub repository.
Wrote this day31.md file.
Screenshots
Step	Screenshot
Mission briefing	![Briefing](images/01-briefing.png)
Live alerts	![Live alerts](images/02-live-alerts.png)
Multiple alerts at once	![Multiple alerts](images/03-multiple-alerts.png)
Final results	![Results](images/04-results.png)
Place the four screenshots in Day31/images/ using the file names above so the links render.

My result
Metric	Value
Grade	A+
Final score	7,196
Service Level	100.0%
Customer Satisfaction	100.0%
Inventory Health	100.0%
Transport Efficiency	100.0%
Operating Cost	$1,893k
Revenue Protected	$5.68M
Alerts resolved	60
Correct decisions	46
Acceptable decisions	8
Wrong decisions	8
Alerts expired	1
Key learnings
Prioritize by urgency and impact. Critical alerts with short timers come first, because they carry the biggest swings.
Match the action to the root cause. Air freight is not a fix for every problem, and it is the most expensive lever.
Good decisions compound. Early correct calls lowered risk and kept later alerts manageable.
Ignoring is never free. Even low-priority alerts cost service level when they expire.
A detailed prompt gets a complete product. Specifying theme, gameplay, KPIs, difficulty and code quality produced a working app in one shot.
Ideas for improvement
Add real audio effects behind the sound toggle.
Add difficulty levels (Easy, Normal, Hard).
Add a map view showing shipments and disruptions by region.
Save a local high-score table.
Add random "boss events" such as a major port closure.
Folder structure
Day31/
├── day31.md
├── ai-supply-chain-control-tower.html
└── images/
    ├── 01-briefing.png
    ├── 02-live-alerts.png
    ├── 03-multiple-alerts.png
    └── 04-results.png
How to run
Download ai-supply-chain-control-tower.html.
Double-click it to open in any modern browser.
Read the instructions, click Start Shift, and survive 3 minutes.