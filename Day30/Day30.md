Day 30: Build a Supply Chain Optimizer

Goal: Optimize an existing supply chain like a real operations leader.

What I Built

Supply Chain Builder is a single-file HTML app (React via CDN, plain CSS) that teaches supply chains to complete beginners. It generates a random company, then guides the player through five decisions. Before each decision it explains what the concept is, why it matters and how it affects the business. After each choice it shows the trade-offs in plain English and updates five live metrics.

Files:

supply-chain-builder.html: the simulator (open in any browser)
Poster artboards: one overview of all steps, one with sample outputs
The Operations Leader Mindset

A supply chain has no perfect setup. Cost, speed, risk, customer satisfaction and sustainability pull against each other. An operations leader asks three questions:

Which metric matters most for this business?
Where is the biggest single point of failure?
What is the cheapest change that improves the weakest metric?
App Flow
Welcome: what a supply chain is and why it matters.
Company profile: random industry, products, countries served and demand level.
Suppliers: single vs multiple.
Factory location: overseas, nearshore, domestic or multi-regional.
Warehouse strategy: central, regional, outsourced (3PL) or cross-dock.
Transportation: road, rail, sea or air.
Inventory strategy: low, balanced or high.
Final dashboard: overall score, strengths, weaknesses, biggest risk and three improvements.
Metrics
Metric	Meaning	Better when
Cost Efficiency	How cheap the chain is to run	Higher
Delivery Speed	How fast goods reach customers	Higher
Risk	Exposure to disruption	Lower
Customer Satisfaction	Availability and service	Higher
Sustainability	Environmental impact	Higher

All metrics start at 50. Each option adds or subtracts points, and company traits (perishable, heavy, seasonal, high demand and so on) add bonuses or penalties for good or poor fit.

Overall score = average of Cost, Speed, (100 − Risk), Satisfaction and Sustainability.

Sample Run

Company: Nova Devices, Consumer Electronics, medium demand, serving USA, Germany, Japan and India. Traits: high-value products, fast-moving trends.

Step	Choice	Cost	Speed	Risk	Satisfaction	Sustainability
Suppliers	Multiple	42	50	35	55	48
Factory	Nearshore	48	56	27	63	52
Warehouse	Regional	40	71	19	73	50
Transport	Air freight	21	93	18	91	32
Inventory	Balanced	23	97	14	97	32

Overall score: 67/100 (Strong).

Strengths: Delivery Speed, Customer Satisfaction
Weaknesses: Cost Efficiency, Sustainability
Biggest risk: air freight cost shock
Improvements: cut costs, go greener, lower risk
Optimization Experiment

The weakest metrics were cost and sustainability, and air freight was the cause of both. I changed one decision and recalculated with the app's own formula.

Scenario	Cost	Speed	Risk	Satisfaction	Sustainability	Score
Air freight	23	97	14	97	32	67
Rail instead of air	50	71	11	79	62	70

Cost and sustainability roughly doubled, and risk dropped slightly. Speed and satisfaction fell, but both remain strong. The net result is a better balanced chain. A real leader would also weigh this against how much customers value speed in the electronics market.

Key Lessons
Single points of failure (one supplier, one warehouse) are the most dangerous hidden risks.
Speed is expensive. Air freight lifts satisfaction but damages cost and sustainability.
Buffers cost money but buy resilience. Inventory is insurance.
Context decides the answer. A strategy that suits electronics can fail for fresh food.
Optimize the weakest link first. One targeted change often beats rebuilding everything.
How to Run
Save supply-chain-builder.html.
Open it in a browser (internet needed on first load for the React and Babel CDN scripts).
Play several rounds, since each replay generates a new company.
Compare your scores and try the same company with different choices.
Next Steps
Add disruption events (port strike, supplier failure) to test resilience.
Add a budget limit and track real cost numbers.
Save and compare multiple runs side by side.
Bundle React and Babel locally for fully offline use.