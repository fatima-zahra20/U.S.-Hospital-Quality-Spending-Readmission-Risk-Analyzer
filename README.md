# U.S. Hospital Quality & Readmission Risk Analyzer
A data‑driven investigation into hospital performance using public CMS datasets. This project combines Medicare data on readmissions, mortality, patient safety, healthcare‑associated infections, patient experience, and Medicare spending per episode.

I took 7 raw CMS datasets, built a complete cleaning pipeline, and designed a multi‑dimensional quality scoring system.  
Here's the code. Here's the output. Here's what it means.


## Individual Hospital Quality.ipynb

### Q1 — What does a hospital's overall quality profile look like across all dimensions?

A hospital's overall star rating (1–5) summarizes all weighted dimensions. The best hospitals have the lowest mortality rates, fewest patient safety incidents, strong patient experience scores, and efficient use of resources.

### Q2 — How aligned is the CMS star rating with actual clinical outcomes?

Five‑star hospitals are flagged "Better than the National Rate" more often, have fewer patient incidents, and lower readmissions.  
A simple star rating hides important nuance. That's why I built a detailed chart (`hosp_quality_star_rating.png`) showing both scores and flags side‑by‑side.


## Identifying Risk.ipynb

### Q3 — Which hospitals have an Excess Readmission Ratio above 1.0 across multiple conditions simultaneously?

I identified hospitals where patients are readmitted more than expected for AMI, heart failure, pneumonia, COPD, hip/knee replacement, and CABG.  
A heatmap shows the top offenders.  
**Surprising insight:** 470 hospitals across the U.S. are getting penalties — all above 1.0 on four to six conditions, indicating a systemic problem.

### Q4 — Which hospitals have both high readmission rates AND high patient safety incidents (PSI scores)?

498 hospitals (out of 2,828 with complete data) show simultaneous safety failures and excess readmissions — roughly 1 in 6 hospitals with evaluable data has a systemic quality problem.  
**Worst case:** St. Bernards Medical Center (AR) shows a PSI‑90 score of 3.16 (3× expected safety incidents) with a readmission ratio of 1.077 across all six conditions.  
Results are shown in a scatter plot.

### Q5 — Which hospitals spend significantly above the national average but have worse‑than‑average outcomes?

**35 hospitals out of 5,426 (0.6%)** are simultaneously:
- Flagged worse than national rate on mortality
- Below average on patient experience
- Above expected on patient safety incidents (PSI‑90)
- Penalized for excess readmissions
- Spending above the national average per episode

These hospitals are not just underperforming — they are actively harming patients *and* costing the healthcare system more. High spending here does not buy better outcomes. It is the worst possible combination.


## Understanding What Drives Quality

### Q6 — Does hospital ownership type predict quality outcomes?

Physician‑owned hospitals consistently outperform all other ownership types across every dimension:
- Lowest mortality (fewer "worse" flags)
- Highest patient experience (90.2)
- Lowest readmission ratio (0.915)
- Only ownership type with PSI‑90 below 1.0 (0.938 vs. national benchmark 1.0)

They win on both quality and spending efficiency.

### Q7 — Do hospitals with emergency services have different complication rates than those without?

Hospitals without emergency departments perform better on safety metrics. A controlled environment (no emergency intake) significantly reduces the risk of errors and infections.  
**The paradox:** Large hospitals with EDs have great doctors and nurses, but also high patient volumes and unplanned visits, making it harder to prevent incidents. This suggests we need to investigate hospital size separately — from extra‑small to extra‑large — rather than comparing all hospitals together.

### Q8 — Is there a relationship between patient experience scores and clinical outcomes?

Patient feelings and clinical outcomes do not move in sync. To truly judge a hospital, you must look at both its "report card" (medical facts) and its "reviews" (patient surveys) separately — they measure completely different things.


## Geographic and Structural Patterns

### Q9 — Which states have the highest concentration of hospitals performing worse than the national rate?

Big states like California always have the highest raw counts, so instead I looked at **failure rate** (percentage of hospitals underperforming).

Among large states (100+ hospitals), **New York and Florida** come out worst. In New York, about 21% of health indicators are worse than the national average. This creates a "quality gap": even though New York has some of the world's best elite hospitals, it also has many crowded or underfunded hospitals pulling the system down.

Meanwhile, **Oregon, Vermont, South Carolina, and Mississippi** show the highest mortality concentration rates (14–18%) — roughly 1 in 6 hospitals flagged worse than national on at least one mortality measure. These states share a profile: rural geography, lower median household income, and historically underfunded rural hospital networks. The problem appears systemic and policy‑driven, not just individual hospital failure.

### Q10 — How does hospital size (patient volume) relate to quality scores?

As hospitals get larger, clinical survival rates tend to improve slightly.  
**Conclusion:** Large hospitals are clinically superior (better at the science of survival) but systemically overwhelmed (worse at the logistics of safety). They get flagged as "Worse" not because their doctors are bad, but because their environments are massive, crowded, and statistically exposed.


## The Project's Core Goal — Risk Scoring

### Q11 — Can you build a composite risk score that identifies hospitals most likely to harm patients or waste Medicare resources?

Yes. This is the axis that changes the results. Even if it can't be applied uniformly across every hospital, it remains the heart of my analyzer. To make this function shine, it should be connected to updated data in a dashboard that allows users to explore different variables.  
That is the next step for this project.

## Overall Conclusion

The healthcare industry needs more investigation, though hospitals are genuinely performing well across most measures — even without access to detailed patient‑level data.

A recurring paradox in this project: a hospital can be measured very differently depending on whether you look at mortality rates versus safety rates. The best hospital on one dimension can be the worst on another.

**Final recommendations:**
- The 35 hospitals identified as overspending should be investigated further.
- The hospitals counted among the best should receive additional staffing support — because doctors and nurses are not machines. Patients who receive better care deserve that same level of care everywhere.
- Emergency departments should be available in every hospital across the United States, with funding and support equivalent to large hospitals. Lives matter in every state, and quality care should not depend on hospital size or location.


## What I Built From Scratch

I started with 7 raw CSV files from a US government healthcare database and ended up with a complete analytical system that:

- Cleaned and standardized 7 tables across 95,000+ rows using a professional pipeline I understand end‑to‑end
- Pivoted long‑format data into analysis‑ready wide format
- Built a composite hospital quality scoring system using MinMaxScaler normalization across 5 clinical dimensions
- Identified 35 hospitals simultaneously failing patients on mortality, safety, patient experience, readmissions *and* overspending
- Found that physician‑owned hospitals outperform all other ownership types across every dimension
- Showed that Oregon, Vermont, and Mississippi have systemic mortality problems at the state level
- Proved that larger hospitals are better at keeping patients alive but worse at preventing safety incidents
- Built 10+ publication‑quality visualizations including heatmaps, scatter plots, normalized bar charts, and stacked charts


### Dashboard Pages
1/2. Overview — Quality & Star Ratings
A high-level map of hospital distribution across the U.S. with KPI cards for average star rating, readmission rate, safety score, mortality rate, and patient experience. Filterable by hospital type.
<img width="985" height="564" alt="image" src="https://github.com/user-attachments/assets/20084918-c9bd-498f-8800-65ac97045542" />


3/4. Hospital Risk Analysis — Readmissions vs. Complications
Scatter plot analysis comparing individual hospitals on two key risk dimensions: readmission ratio and PSI-90 complication score. Hospitals above 1.0 on either axis are performing worse than the national average.
<img width="888" height="521" alt="image" src="https://github.com/user-attachments/assets/dff4f523-6998-4e80-a7ed-05e2dbd51fdc" />


5/6. The Spending Trap — High Cost, Poor Outcomes
Identifies the 26 hospitals with the highest average spending per episode and overlays their clinical outcome scores. Core finding: these hospitals show above-average readmissions, mortality, and patient incidents simultaneously — high spending is not buying better care.
<img width="901" height="515" alt="image" src="https://github.com/user-attachments/assets/dadf74bf-a2f2-4d45-ad05-00174a57dbf6" />


7. Does Ownership Predict Quality?
Radar/composite analysis across all ownership types (physician-owned, non-profit, government, proprietary). Key finding: physician-owned hospitals outperform all others on every metric — lowest readmission ratio (0.915), highest patient experience (90.2), and the only group with PSI-90 below 1.0.
<img width="906" height="523" alt="image" src="https://github.com/user-attachments/assets/5a54bb8c-3eb3-4677-813d-e544c232d468" />


⚠️ Caveat applied: Physician-owned hospitals tend to treat lower-risk elective patients. The analysis explicitly flags that their superior scores partially reflect patient mix, not just quality of care — a real-world bias that a naive analysis would miss.

8. Emergency Department Effect on Quality
Compares hospitals with and without 24/7 emergency services on three metrics: mortality rate, complication score (PSI-90), and infection ratio (SIR). To ensure a fair comparison, three analytical filters were applied:

<img width="909" height="522" alt="image" src="https://github.com/user-attachments/assets/59fdf880-f70e-41b1-ad60-234f72f9437d" />


Acute Care Only — excluded Critical Access and Psychiatric hospitals with different reporting rules
ID Standardization — enforced 6-digit Facility IDs to prevent data loss during merge
Risk-Adjusted Scores — used CMS standardized scores to account for patient severity

Finding: Non-ED hospitals show meaningfully lower infection and complication rates, consistent with their controlled, elective-only environment.
9/10. Systemic Risk by State
Rather than ranking states by raw count of underperforming hospitals (which would always favor large states), this page measures the failure rate — the percentage of a state's hospitals performing below the national average. Finding: New York (21% failure rate) and Florida lead large states, despite housing some of the country's best-ranked elite hospitals — a "Quality Gap" paradox driven by overcrowding and funding disparities.
<img width="871" height="507" alt="image" src="https://github.com/user-attachments/assets/696d53f8-1bb5-4e26-93c5-3fe30f691463" />


11. Hospital Archetypes — The Core Risk Scoring Model
The project's analytical centerpiece. Hospitals are segmented into 7 archetypes based on a composite score across spending, mortality, complications, and patient experience

<img width="873" height="505" alt="image" src="https://github.com/user-attachments/assets/26b0deaf-58cd-4ab6-8374-52856f095add" />


Built by *Fatima-Zahra Boutkhil* as part of a self-directed data analyst portfolio.
Focused on building real analytical projects using public datasets — not tutorials.
