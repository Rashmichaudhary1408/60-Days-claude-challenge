# Day 16 — Custom Claude Skill: `stock-fundamental-research`

## Objective
Build a reusable Custom Skill in Claude that analyzes Indian and global listed
companies using fundamentals only (financial statements, valuation, growth,
ownership, risks) — and test it end-to-end without re-entering the prompt
each time.

---

## 1. Skill Details

**Skill Name:** `stock-fundamental-research`

**Description:**
> Analyze Indian and global listed companies using fundamentals, financial
> statements, business quality, competitive advantages, valuation, risks, and
> growth prospects. Generate evidence-based research reports and
> investor-friendly summaries. Never provide direct buy, sell, or hold
> recommendations.

**Core rules encoded in the skill:**
- Source priority: Screener > Tickertape > Moneycontrol > NSE > BSE > Annual
  Reports > Earnings Calls; cross-check key figures with 2+ sources.
- Never fabricate data — flag unavailable figures with 🚩 instead of guessing.
- Cite a source next to every key figure.
- Never give buy/sell/hold calls, target prices, or personalized advice.
- No predictions — only illustrative, historical-trend discussion.
- Plain-English explanations for financial jargon on first use.

**Supported modes:** Quick Take · Deep Dive · Compare · Pros & Cons ·
Portfolio Fit (auto-selected based on how the request is phrased).

---

## 2. Setup Steps (performed in Claude)

1. Opened Claude (web/app).
2. Set model effort level to Low/Medium for faster iteration.
3. Navigated to **Settings → Capabilities → Skills**.
4. Selected **Create Skill**.
5. Set Skill Name: `stock-fundamental-research`.
6. Pasted the description above into the Description field.
7. Pasted the full instructions block (rules, checklist, interpretation
   thresholds, output formats) into the Instructions field.
8. Saved the Custom Skill.

*(See `screenshots/skill-setup.png` and `screenshots/skill-saved.png`.)*

---

## 3. Testing the Skill

The skill was tested across all three practical output modes, in fresh
chats, without re-pasting any instructions — confirming the skill loads
and applies itself automatically once saved.

### Test 1 — Deep Dive: Tata Consultancy Services (TCS)
- Mode: **Deep Dive**
- Output: Tabbed dashboard — Snapshot, Valuation, Growth, Health, Returns,
  Peers, Ownership, View
- Key figures reviewed: CMP ₹2,304 · Market Cap ≈₹8.3L Cr · P/E ≈18.1x ·
  ROE (5Y avg) 58% · Revenue FY26 ₹2,20,938 Cr · D/E ~0.11 (Safe)
- Unavailable metrics (ROCE, current ratio, interest coverage, FCF) were
  correctly flagged with 🚩 rather than fabricated.
- Artifact: `tcs-deep-dive.html`

### Test 2 — Compare: Tata Motors vs Mahindra & Mahindra
- Mode: **Compare**
- Output: Side-by-side VS dashboard with metric cards, a dedicated
  "Business Note" tab on the JLR cyberattack (Sept 2025) and its impact on
  Tata Motors' FY26 numbers, and a neutral summary with no declared winner.
- Key comparison: M&M's steadier ~25% YoY revenue growth and 24.1x P/E vs
  Tata Motors CV's post-demerger, less comparable ~52x P/E.
- Artifact: `tatamotors-vs-mm-compare.html`

### Test 3 — Deep Dive: Infosys
- Mode: **Deep Dive**
- Key figures: CMP ₹1,030 · Market Cap ≈₹4.18L Cr · P/E ≈13.8x (cheaper than
  TCS/HCL Tech peers) · ROE ~32% · ROCE ~36.8% · Debt/Equity 0.00
- Peer table included TCS, HCL Tech, Wipro, Persistent Systems.
- Artifact: `infosys-deep-dive.html`

*(See `screenshots/tcs-report.png`, `screenshots/compare-report.png`,
`screenshots/infosys-report.png`.)*

---

## 4. Observations

- **Reusability:** Once saved, the skill activates automatically in any new
  chat just by naming a stock or asking for a comparison — no need to
  re-paste the description or instructions. This was confirmed by opening a
  brand-new chat and asking for a report directly.
- **Data integrity in practice:** Live web data for Indian stocks is often
  inconsistent across sources and snapshot dates. The skill's "never
  fabricate, flag instead" rule proved genuinely useful here — several
  ratios (ROCE, current ratio, interest coverage, FCF) were marked 🚩 rather
  than filled in with guessed numbers.
- **Mode detection:** Simply phrasing a request as "X vs Y" correctly
  triggered Compare mode, while naming a single stock triggered a Deep Dive,
  matching the skill's mode-selection rules.
- **Compliance:** Every report ended with the required disclaimer and never
  issued a buy/sell/hold call, even when asked to compare two stocks
  head-to-head.

---






