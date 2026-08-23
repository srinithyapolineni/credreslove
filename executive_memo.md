# Credresolve Collections Analytics — Executive Memo

## Executive Summary

The reported statement that “Recovery has improved by 11% month-on-month” is **partially true**.

Cleaned successful recovery increased **11.03% from February to March 2026**. However, this was not accompanied by an equivalent improvement in collection efficiency. Targeted accounts increased **9.81%**, paying accounts increased **11.32%**, target-to-payment conversion improved by only **0.58 percentage points**, and recovery per paying account declined **0.26%**.

Therefore, the evidence supports an increase in absolute recovery, but **does not support describing the change as an 11% improvement in underlying collection efficiency**.

## 1. What Happened?

February recovery was approximately **₹17.01 Cr**, increasing to **₹18.89 Cr in March**, an **11.03% increase**.

The number of paying accounts increased from **2,173 to 2,419 (+11.32%)**, while recovery per paying account decreased from approximately **₹78,298 to ₹78,095 (-0.26%)**.

Targeted accounts also increased from **5,160 to 5,666 (+9.81%)**.

Across the full completed-month series, March is not evidence of a sustained 11% month-on-month improvement. Recovery subsequently declined in April and June, while conversion also moved back down. August is incomplete and should not be treated as a full-month performance period.

## 2. Why Did It Happen?

The February-to-March increase appears primarily **volume-driven**.

DPD mix changed, with the 1–30 DPD segment increasing its share of recovery from approximately **34.63% to 38.29%**. However, loan-type and risk-segment mixes were comparatively stable.

Channel targeting mix was also broadly stable, although March showed higher recovery associated with SMS, Voice and WhatsApp in the observational channel analysis.

Recovery per paying account did not improve overall, and several DPD segments actually experienced lower recovery per payer. This suggests that the observed increase was not a broad-based operational improvement across all borrower segments.

## 3. Data Quality and Confidence

The raw data contains significant quality issues that required independent cleaning and validation:

* **500 duplicate payment IDs** were identified without field-level conflicts. Removing one copy per payment ID reduced SUCCESS recovery by approximately **₹2.59 Cr (1.93%)**.
* **66.63% of calls** change hour after normalization across UTC, Asia/Kolkata and Asia/Dubai timestamps; **9.77%** change calendar date.
* **2,913 accounts (9.71%)** have missing or invalid borrower relationships.
* **50.32% of account-status history records** have event timestamps later than their recording timestamps, indicating substantial late-arriving/timestamp-ordering behavior.
* Multiple disposition versions coexist, so disposition semantics should remain version-aware unless formally validated.

Confidence in the conclusion that the 11% February-to-March increase is largely volume-driven is **Medium–High**. Confidence in any causal claim about a specific channel or operational intervention is **Medium/Low**, because the supplied data is observational and does not provide a controlled experiment.

## 4. Recommended Action — ₹10 Cr

### Recommendation: SMS / Digital Engagement Scale-Up Through Controlled Experimentation

SMS produced the highest observed recovery and the highest observed recovery per agent-hour in the available channel analysis:

**₹1,009 recovery per agent-hour for SMS**, versus **₹846 for Field**, a **19.33% observational efficiency gap** between the strongest and weakest channels.

This should **not** be interpreted as a proven 19.33% causal uplift.

The recommended use of the ₹10 Cr is therefore a controlled scale-up of SMS/digital engagement, with treatment and control groups defined by borrower/account characteristics and measured on recovery rate, target-to-payment conversion, PTP kept rate, recovery per account and cost per ₹ recovered.

### Scenario Economics

| Scenario | Assumed uplift | Incremental recovery / year |     ROI | Approx. payback |
| -------- | -------------: | --------------------------: | ------: | --------------: |
| Downside |             2% |                    ₹2.54 Cr |  25.37% |      3.94 years |
| Base     |             5% |                    ₹6.34 Cr |  63.42% |      1.58 years |
| Upside   |         19.33% |                   ₹24.52 Cr | 245.20% |      0.41 years |

The **5% base case** should be treated as a scenario assumption, not a measured causal effect. Payback assumes the uplift persists at the assumed rate.

## 5. Final Decision

**Verdict on the 11% claim: PARTIALLY TRUE.**

The February-to-March recovery amount increased by approximately 11%, but the data does not support an 11% improvement in collection efficiency. The increase is primarily associated with a larger targeted and paying population rather than higher recovery generated per paying account.

**Decision:** Scale SMS/digital engagement through a controlled experiment, with strict measurement of incremental recovery and cost efficiency before committing the full investment.
