# Day 17 —  Build an AI Vehicle Cost & Fuel Analysis Dashboard
### Transform raw CSV data into an interactive dashboard

## 🎯 Objective
Used Claude to go end-to-end from a raw CSV to a live interactive dashboard:
load a 53-record vehicle fuel dataset (CNG, Diesel, E85 Flex-Fuel, Petrol E20, EV),
compute cost/emissions/maintenance metrics per fuel type, and visualize them in a
single self-contained HTML dashboard — no manual charting, no spreadsheet formulas,
just a CSV in and a working dashboard out.

Along the way, this also answered a real question: the "E85 paradox" — does a
cheaper pump price for E85 actually mean cheaper driving?

**Vehicle context:** Toyota Fortuner · Petrol (E20) · Mixed usage · assumed 1200 km/month, 4-yr age (not provided in the brief, so used as working assumptions).

## 🗂 Files in this folder
- `day17_dashboard.html` — self-contained interactive dashboard (pure SVG charts, no CDN dependencies)
- `screenshots/` — dashboard screenshots (add your own captures here)
- `day17.md` — this write-up

## 🤖 Workflow — How Claude Built This
1. **Ingest:** Uploaded the raw CSV directly; Claude read and parsed it (no manual cleaning).
2. **Compute:** Claude derived cost/km, CO₂/km, and maintenance/km per record, grouped
   and averaged by fuel type, bucketed by vehicle age, and fit linear trend lines for
   cost-vs-age projections (0–12 years) per fuel.
3. **Score:** Claude built a weighted E85 score (cost=4, CO₂=3, refuel=2, maintenance=1)
   directly from the computed averages.
4. **Visualize:** Claude generated a single self-contained HTML file — pure inline SVG
   bar/donut/line charts, an animated CSS gauge, and fuel comparison cards — with no
   external chart library or CDN dependency.
5. **Output:** One dashboard file, ready to open in any browser or host as a static page.

## 📊 Method
For every record: `cost/km`, `CO₂/km`, and `maintenance/km` were derived by
dividing the absolute figures by `Distance_km`, then averaged per fuel type.
Age buckets (New 0–2y, Mid-life 3–5y, Aged 6–9y, Old 10+y) were used to check
how cost and maintenance drift with vehicle age. Cost-vs-age trend lines were
fit with linear regression per fuel and projected across 0–12 years.

## 🔑 Key Metrics (per-fuel averages)

| Fuel | Cost/km | CO₂/km | Maint/km | Refuel/Charge | Price/unit | Mileage |
|---|---|---|---|---|---|---|
| CNG | ₹3.32 | 0.125 kg | ₹0.66 | 8 min | ₹80 | 24.1 km/kg |
| Diesel | ₹4.67 | 0.179 kg | ₹1.00 | 5 min | ₹91 | 19.6 km/L |
| E85 (Flex-Fuel) | ₹6.37 | **0.070 kg (lowest)** | ₹0.46 | 5 min | ₹82 | 12.9 km/L |
| Petrol (E20) — *your fuel* | ₹6.15 | 0.171 kg | ₹0.47 | 5 min | ₹100 | 16.3 km/L |
| Electric (EV) | **₹1.75 (lowest)** | 0.091 kg | **₹0.23 (lowest)** | 45 min | ₹12 | 6.9 km/kWh |

## ⛽ The E85 Paradox

- **Pump saving:** E85 (₹82/L) is **18% cheaper per litre** than Petrol (₹100/L).
- **Running penalty:** Despite that, E85's actual cost/km (₹6.37) is **~3.6% higher**
  than Petrol's (₹6.15) — because E85's mileage (12.9 km/L) is much lower than
  Petrol's (16.3 km/L), the fuel-efficiency loss outweighs the pump discount.
- **Break-even price:** For E85 to match Petrol's running cost, it would need
  to be priced at **₹79.11/L or lower** — about ₹3 cheaper than its current ₹82/L.
- **E85 Score: 6.6 / 10** (Cost 1.1/4, CO₂ 3.0/3 — best of all fuels, Refuel 2.0/2 — tied best, Maintenance 0.5/1)

**Takeaway:** E85's low pump price is misleading on its own — it looks cheaper
at the station but costs more to actually drive, because of the mileage drop.
Where E85 genuinely wins is emissions: it has the lowest CO₂/km of every fuel
in the dataset, including EV (which still carries grid-related emissions in
this data). It's the right choice for someone prioritizing lower tailpipe
carbon output, not someone chasing the lowest running cost.

## 📈 Age Effect
Cost/km rises with vehicle age for every fuel (more wear, less efficient
combustion, aging seals/injectors), but the slope differs sharply:
- **EV** has the flattest cost curve (~₹0.04/km per year) — least sensitive to age.
- **E85** and **Petrol** rise fastest (~₹0.13–0.15/km per year) — likely because
  higher-ethanol blends are harsher on fuel systems over time.
- At the assumed 4-year mark, Petrol sits around ₹5.9/km and E85 around ₹6.7/km
  on the fitted trend line.

## 🧠 Learnings
1. **Pump price ≠ running cost.** Mileage (km per litre/kg/kWh) is the variable
   that actually determines cost/km — a lower price per unit fuel can still lose
   if efficiency drops enough (classic E85 trap).
2. **CO₂/km and cost/km don't move together.** E85 is the cleanest fuel here but
   not the cheapest — trade-offs between cost and emissions are real and dataset-driven,
   not assumed.
3. **EV dominates on running cost and maintenance** but is heavily penalized on
   refuel/charge time (45 min vs 5–8 min for liquid/gas fuels) — a usability
   cost that raw ₹/km numbers don't capture.
4. **Weighted scoring (cost=4, CO₂=3, refuel=2, maintenance=1) is a design choice** —
   it reflects that most buyers weigh running cost most heavily, but changing
   those weights would change the "winner" materially (e.g., weighting CO₂ higher
   would push E85's score well above 8/10).
5. Building all charts in pure inline SVG (no chart library, no CDN) keeps the
   dashboard fully self-contained and portable — useful for offline sharing or
   embedding without dependency/version issues.
6. **Claude as an analyst, not just a chatbot:** the same conversation handled
   data cleaning, statistical computation, scoring logic, and front-end visualization —
   showing how a single prompt-driven workflow can replace a multi-tool pipeline
   (Excel → Python → chart tool → export) for small-to-mid-size datasets.

## ✅ Next Steps
- Get the real KM/month and car age for the Fortuner to replace the assumed values.
- Add sample-size weighting (E85/EV/Petrol/CNG have 10–11 records, Diesel has 9) —
  small-n groups are more sensitive to outliers.
- Extend the age-trend model with a non-linear (e.g. quadratic) fit if more
  data points per fuel become available past the current 1–12 year range.