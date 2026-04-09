**Author:** Fatima Zahra Boutkhil
**Dataset:** https://data.cms.gov/ -- Data that helps you better understand CMS programs
**Tools:** Python (Pandas, Matplotlib, Seaborn) + SQL (SQLite)

---



# What You're Actually Sitting On 
## Before the questions, understand what these 7 tables represent together. CMS evaluates hospitals from 5 completely different angles — and you have data for all 5:
---
WHO they are       → general_info
HOW SAFE they are  → complications & deaths, HAI
HOW PATIENTS FEEL  → HCAHPS 
HOW MUCH IT COSTS  → medicare spending
HOW OFTEN PATIENTS COME BACK → unplanned visits, readmissions

---
No single table tells the full story. A hospital can score beautifully on patient experience but have terrible mortality rates. Another can have low readmissions but astronomical spending. Your project's power comes from combining all five lenses simultaneously — that's what makes it an analyzer, not just a report.


### Table by Table — What the Data Is Actually Saying

**General Info** is your hospital passport. It tells you what kind of institution each hospital is, who owns it, where it sits, and CMS's pre-computed star rating. The star rating is a single number summarizing everything — your job is to go deeper than that number and understand what drives it.

**Complications & Deaths answers**: did patients survive their care, and did anything go wrong during it? The MORT measures are 30-day mortality rates — the percentage of patients who died within 30 days of discharge. The PSI measures are patient safety indicators — events that should rarely or never happen (falling in the hospital, getting a bedsore, a surgical instrument left inside a patient). Lower is better for all of these.

**HCAHPS answers**: how did patients experience their stay? It's a standardized survey sent to discharged patients asking about nurse communication, doctor communication, cleanliness, quietness, pain management, and whether they'd recommend the hospital. It's the only table that captures the human side — a hospital can have perfect clinical outcomes but leave patients feeling ignored or disrespected.

**Medicare Spending answers**: how much did each hospital cost Medicare per episode of care? An episode covers the period before admission, during the stay, and after discharge. It's broken down by claim type — inpatient costs, outpatient costs, skilled nursing, home health, hospice. A hospital that spends far above the national average isn't necessarily providing better care — it might just be inefficient or over-treating.

**Unplanned Visits answers**: how often did patients have to come back? The EDAC measures count excess days patients spent in hospital within 30 days of discharge — not just readmissions but also ER visits and observation stays. The READM measures count straight 30-day readmission rates. Higher numbers mean patients are leaving too sick, or not being supported properly after discharge.

**Readmissions (HRRP) answers**: is this hospital being penalized by CMS for excessive readmissions? The Excess Readmission Ratio is the key number — it compares actual readmissions to what was expected given that hospital's patient mix. Above 1.0 means worse than expected. CMS uses this to financially penalize hospitals — so hospitals take it very seriously.

**Healthcare Associated Infections answers**: did patients catch something dangerous while they were there? HAI measures track infections patients acquired in the hospital — central line infections, catheter infections, MRSA, C. difficile. These are largely preventable and represent serious failures in infection control protocols.

---

## Questions That Lead to Your Project Goal

**Understanding Individual Hospital Quality**

Q1 — What does a hospital's overall quality profile look like across all dimensions?
Definition: quality profile = a hospital's combined scores across safety, experience, spending, and readmissions — not just one number.
This is the core output of your analyzer. For any given hospital you want to see all five lenses at once. Does a hospital that scores well on patient experience also score well clinically? Or are these unrelated? 
 
Q2 — How aligned is the CMS star rating with actual clinical outcomes?
Definition: star rating = CMS's 1-5 summary score, computed from a weighted formula across multiple measure groups.
Sometimes a hospital has a 4-star rating but a mortality rate worse than the national average. Understanding where the star rating misleads or oversimplifies is analytically valuable.

---

**Identifying Risk**
Q3 — Which hospitals have an Excess Readmission Ratio above 1.0 across multiple conditions simultaneously?
Definition: Excess Readmission Ratio = actual readmissions ÷ expected readmissions. Above 1.0 means the hospital readmits more patients than expected for its patient population. CMS penalizes these hospitals financially.
A hospital above 1.0 on just one condition might be unlucky. A hospital above 1.0 on four conditions has a systemic problem.

Q4 — Which hospitals have both high readmission rates AND high patient safety incidents (PSI scores)?
Definition: PSI = Patient Safety Indicator — events like hospital-acquired pressure ulcers, post-operative blood clots, or falls that represent preventable harm during a hospital stay.
These two together suggest a hospital that both harms patients during the stay AND sends them home before they're ready.

Q5 — Which hospitals spend significantly above the national average but have worse-than-average outcomes?
Definition: spending per episode = total Medicare cost for one complete care episode including pre-admission, hospital stay, and 30-day post-discharge period.
High spending + poor outcomes is the worst combination — it means the hospital is inefficient AND harmful. High spending + good outcomes is a different conversation.

---

**Understanding What Drives Quality**
Q6 — Does hospital ownership type predict quality outcomes?
Definition: ownership type = who runs the hospital — government, voluntary non-profit, or proprietary (for-profit). Each has different financial incentives and governance structures.
For-profit hospitals have shareholders. Non-profits reinvest revenue into care. Does that financial difference show up in patient outcomes?

Q7 — Do hospitals with emergency services have different complication rates than those without?
Definition: emergency services = 24/7 emergency department capacity. Hospitals without it are often specialty or elective-only facilities.
Emergency hospitals treat sicker, more complex patients — so raw comparison isn't fair. But after controlling for patient mix, do they perform differently?


Q8 — Is there a relationship between patient experience scores and clinical outcomes?
Definition: patient experience = HCAHPS survey results measuring how patients perceived their care — communication, responsiveness, cleanliness.
Does a hospital where nurses communicate well also have lower mortality rates? Or are these completely independent dimensions of quality?

---

**Geographic and Structural Patterns**
Q9 — Which states have the highest concentration of hospitals performing worse than the national rate?
Definition: worse than national rate = CMS's flag in the compared_to_national column, meaning the hospital's score is statistically significantly worse than the US average.
State-level patterns can reveal systemic issues — rural access problems, funding disparities, or regulatory differences.

Q10 — How does hospital size (measured by patient volume/denominator) relate to quality scores?
Definition: denominator = number of patients used to calculate a measure. Larger denominators mean more statistically reliable scores.
Large hospitals treat more patients and may have more specialized staff. Small hospitals may have stronger community relationships but fewer resources. Neither is automatically better.

---

**The Project's Core Goal — Risk Scoring**
Q11 — Can you build a composite risk score that identifies hospitals most likely to harm patients or waste Medicare resources?
Definition: composite risk score = a single calculated number combining multiple quality signals — readmission ratios, mortality rates, PSI scores, spending, and HAI rates — weighted by their importance.

This is the final deliverable. Not "which hospital is bad at one thing" but "which hospitals are consistently underperforming across multiple dimensions simultaneously." That's the Hospital Quality & Readmission Risk Analyzer.

---

# How These Questions Connect
Q1-Q2   → Understand the landscape
Q3-Q5   → Identify the highest-risk hospitals
Q6-Q8   → Understand WHY some hospitals perform worse
Q9-Q10  → Find geographic and structural patterns
Q11     → Build the risk score that ties it all together







