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

## What I Proved About Myself

I came in as a self‑taught analyst who sometimes froze on independent work. I leave having:

- Debugged real errors under pressure without giving up
- Made real analytical decisions independently — the `worse_flags_mort` naming correction, the `.between(4,6)` filter, noticing the patient experience bias toward small hospitals
- Written genuinely good analytical markdown that explains *why* findings matter, not just what the numbers say


## Author

**Fatima Zahra Boutkhil**

**Dataset:** [CMS Data](https://data.cms.gov/) – Data that helps you better understand CMS programs

**Tools:** Python (Pandas, Matplotlib, Seaborn)
