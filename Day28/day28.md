# Day 28 — Build a Hospital Admission Readiness Simulator

> Experience hospital admissions through an interactive healthcare workflow.

**Live demo:** https://claude.ai/artifact/4hBeqd6s3f1YphLYPtkGYC
**Stack:** Single-file HTML · Tailwind CSS (CDN) · Vanilla JavaScript
**Role you play:** Hospital Admission Coordinator

> ⚠ All provider, physician and payer names in the simulator are **illustrative training data**. Industry figures are estimates only.

---

## 1. What We're Building

An interactive simulation where you act as an Admission Coordinator and clear every barrier between a patient and a safe, compliant admission. It is **task-first**: there is no dashboard on load. You configure a case, analyze it, then work through workflow actions until the patient is ready to be admitted.

## 2. Learning Objectives

- Understand the steps that must be complete before a patient is admitted.
- See how **Prior Authorization (PA)** outcomes (approved, pending, denied) change your workflow.
- Learn how documentation, orders, insurance, consent and bed readiness combine into a weighted readiness score.
- Recognize **Observation vs. Inpatient** differences (CMS 2-Midnight Rule, MOON notice).
- Practice risk tracking and make a final **Admit / Not Ready** decision.
- Learn how to prompt an AI to generate a complete single-file application.

## 3. Setup Inputs

| Field | Options |
|---|---|
| Provider | Free text (illustrative) |
| Attending Physician | Free text (illustrative) |
| Diagnosis | Acute MI · CHF · Pneumonia · Elective Surgery · Hip Fracture |
| Admission Type | Inpatient · Observation · Emergency · ICU · Same-Day Surgery |
| PA Status | Approved · Pending · Denied |
| Admission Date | Date picker |

**Observation status** always displays:
*CMS 2-Midnight Rule applies — different cost-sharing, SNF eligibility, and billing than inpatient. Medicare patients require written MOON notification.*

## 4. Readiness Score

The initial analysis scores between **30% and 60%** and withholds the final decision.

| Component | Weight |
|---|---|
| Prior Authorization | 25% |
| Clinical Documentation | 20% |
| Physician Orders | 20% |
| Insurance | 15% |
| Consent | 10% |
| Bed | 10% |

**Rule:** a denied PA combined with an ICU admission cannot exceed **69%** from administrative tasks alone. The appeal must succeed first.

## 5. Prior Authorization Branches

- **Approved** → continue the workflow.
- **Pending** → Follow Up · Upload Docs · Contact Physician. Completing all three secures approval.
- **Denied** → Review Reason · Contact Insurance · Submit Appeal. A successful appeal converts the PA to **Approved**.

## 6. Workflow Actions

1. Assign Bed
2. Verify Insurance
3. Upload Documentation
4. Complete Consent
5. Contact Physician
6. Notify Nursing *(requires assigned bed)*
7. Prepare Patient Arrival *(requires bed + consent)*

## 7. Clinical Context Features

- **Criteria note** (Acute MI, CHF): *InterQual/Milliman thresholds apply — ensure documentation meets medical necessity standards before UR review.*
- **Timeline:** PA Review → Insurance Verification → Bed Assignment → Documentation → Consent → Patient Arrival → Registration → Clinical Assessment → Admission Complete
- **Care Coordination Cards:** Attending · Case Manager · Nursing · Utilization Review · Discharge Planner. The UR card names concurrent review, denial risk identification, InterQual and Milliman.
- **Risk Tracking:** Documentation · Insurance · Bed · Clinical. Clinical Risk is weighted higher (×1.4) for Acute MI, CHF and ICU.
- **Governance Snapshot** (shown at readiness ≥ 75%): *Industry benchmarks (estimates only): PA turnaround 3–5 days · Inpatient denial rate ~8–10% (CMS) · PA rework cost ~$11/transaction (CAQH).*

## 8. Final Decision

| Readiness | Outcome |
|---|---|
| ≥ 90% | ✅ **Admit** — full summary |
| < 90% | ⚠ **Not Ready** — missing items, required actions, remaining risks |

## 9. Step-by-Step Walkthrough

1. Paste the Hospital Admission Readiness Simulator prompt into Claude.
2. Generate the complete HTML application.
3. Save the generated HTML file.
4. Open the simulator in your browser.
5. Enter provider and physician details.
6. Select a diagnosis and admission type.
7. Configure PA status and admission date.
8. Click **🏥 Analyze Admission Readiness** and review the initial score.
9. Complete workflow actions to improve readiness.
10. Resolve PA scenarios: approval, pending follow-up, or appeal.
11. Reduce documentation, insurance, bed and clinical risks.
12. Review the Governance Snapshot when it appears.
13. Click **Finalize Admission Decision** and analyze the result.
14. Restart and test multiple diagnosis scenarios.
15. Take screenshots of the simulator and results.

## 10. Test Scenarios to Try

| Scenario | What to observe |
|---|---|
| Acute MI + ICU + PA Denied | Score capped at 69% until the appeal succeeds; high clinical risk |
| CHF + Inpatient + PA Pending | Criteria note shown; three actions convert PA to Approved |
| Pneumonia + Observation + PA Approved | Permanent 2-Midnight / MOON banner |
| Elective Surgery + Same-Day Surgery + Approved | Fastest path to ≥ 90% |
| Hip Fracture + Emergency + Pending | Sequencing of bed, consent and arrival steps |
| Finalize early | See the **Not Ready** report with missing items |

## 11. Prompting Tips

- State the **role**, **inputs**, **scoring weights** and **rules** explicitly.
- Specify exact required text (e.g., the Observation note and benchmarks) so it appears verbatim.
- Define **gating rules** (e.g., denied PA + ICU cap) so the simulation behaves realistically.
- Iterate on design with follow-ups such as *"enhance the UI and make it more attractive."*

## 12. Key Takeaways

- Admission readiness is a **coordination problem**: no single task gets a patient admitted.
- Prior authorization is the heaviest-weighted barrier, so resolve it early.
- Observation vs. inpatient status changes billing, cost-sharing and notification duties.
- Risk visibility helps prioritize which gaps to close first.
- A well-structured prompt can produce a complete, interactive application in a single file.

---

*Day 28 complete. Next: restart the simulator, test every diagnosis, and capture your screenshots.*
