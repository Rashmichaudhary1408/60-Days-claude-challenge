# Day 48: Verdict Engine, Best-Value Smartphone

Data as researched on 29 October 2026. Source: `verdict-engine.html` (an interactive ranking tool; this note records what it shows when run).

## What it is

A single-page tool that ranks four base-model phones. Five sliders (0 to 10) set how much each factor matters, and the ranking and score bars update live.

**Phones:** iPhone 16 (128GB), Galaxy S25 (128GB), Pixel 9 (128GB), OnePlus 13 (256GB).
**Not included:** newer successors (iPhone 17, Galaxy S26, Pixel 10, OnePlus 15).

## The data

| Criterion | iPhone 16 | Galaxy S25 | Pixel 9 | OnePlus 13 |
|---|---|---|---|---|
| Price (US launch MSRP, lower is better) | $799 | $799 | $799 | $899 |
| Battery (EU-label endurance) | 37:00 h | 37:16 h | 49:12 h | 61:36 h |
| Charging (rated wired) | 25 W (estimate) | 25 W | 27 W | 100 W (cross-source) |
| Performance (Geekbench 6 multi-core) | 7,929 | 10,050 | 4,489 | 8,999 (cross-source) |
| Camera (PhoneArena score) | 149 | 147 | 144 | 145 |

### Flagged values
- **iPhone 16 charging:** Apple publishes no rating. 25W is the listed figure, and about 30W was measured at peak.
- **OnePlus 13 charging:** 100W is the global rating (0 to 100% in 36 min). The US model is reported at 80W, which would still lead.
- **OnePlus 13 performance:** sources give 8,999 / 9,278 / 9,467. The lowest was used.
- **Pixel 9 price:** the $799 figure comes from an aggregator citing GSMArena.
- **Camera:** all four scores sit within about 5 points, so camera rarely changes the ranking.

## How scoring works

1. Each criterion is scored 0 to 100 across the four phones. Price is inverted, so cheaper scores higher.
2. Your slider weights average the five scores.
3. Two methods are available:
   - **Relative to best (default):** score = value ÷ best value. Small gaps stay small.
   - **Spread:** best = 100, worst = 0. Small gaps get exaggerated.

## Results when run

### Default (all sliders at 5, relative method)

| Rank | Phone | Score |
|---|---|---|
| 1 | **OnePlus 13** | **95.1** |
| 2 | Galaxy S25 | 76.8 |
| 3 | iPhone 16 | 72.8 |
| 4 | Pixel 9 | 69.6 |

Verdict shown on the page: OnePlus 13 is the best match, 18.3 points ahead of the Galaxy S25. A caution is also shown because its charging and performance figures are flagged as cross-source.

### Spread method (equal weights)

| Rank | Phone | Score |
|---|---|---|
| 1 | OnePlus 13 | 60.2 |
| 2 | iPhone 16 | 52.4 |
| 3 | Galaxy S25 | 52.2 |
| 4 | Pixel 9 | 30.5 |

The iPhone 16 and Galaxy S25 are effectively tied (0.2 apart), and the gap between 1st and 2nd is much smaller than under the relative method.

### Other priority profiles (relative method)

| Priorities | Winner | Runner-up |
|---|---|---|
| Price only | Three-way tie at 100: iPhone 16, Galaxy S25, Pixel 9 (OnePlus 13 last at 88.9) | n/a |
| Battery 10 + Charging 5 | OnePlus 13 (100.0) | Pixel 9 (62.2) |
| Performance only | Galaxy S25 (100.0) | OnePlus 13 (89.5) |
| Camera only | iPhone 16 (100.0) | Galaxy S25 (98.7) |
| Balanced value (price 8, battery 6, charging 3, performance 3, camera 8) | OnePlus 13 (94.9) | Galaxy S25 (83.1) |

## Takeaways

- **OnePlus 13** wins whenever battery or charging carries any weight. It only loses when price or raw performance is the sole priority.
- **Galaxy S25** is the pick for pure performance and the best all-round alternative.
- **iPhone 16** wins only on camera, and only by about 1 to 3 points.
- **Pixel 9** ranks last or near-last in most profiles, mainly because of its low Geekbench score (4,489). It is competitive on price and camera.
- Prices are launch MSRP. Street prices vary widely, so check today's price before buying.

## Caveats

- Geekbench is a synthetic benchmark, not a measure of everyday speed.
- The EU-label battery rating was the only battery metric available for all four phones.
- Rankings reflect only the listed sources and are not a purchase guarantee.
