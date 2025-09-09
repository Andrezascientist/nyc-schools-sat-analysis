# NYC Schools SAT – Exploratory Case Study

**Author:** Andreza Eufrasio

**Stack:** Python, pandas, numpy, matplotlib

**Notebook:** nyc_school_sat_score_case_study.ipynb

Analyze NYC schools’ SAT scores to uncover subject-level and overall performance patterns. Provide clear, data-driven insights that can guide education policies and family school choices.

---
## Business Context
Every year, U.S. high school students take the SAT, a standardized exam with three sections:reading, math, and writing; each scored up to 800 points and crucial for college admissions. Analyzing school performance on these tests provides valuable insights for stakeholders including educators, policymakers, researchers, and families. In New York City, understanding SAT results across schools and boroughs helps identify excellence, gaps, and variability, enabling data-driven decisions on resource allocation, program design, and school selection while supporting efforts to improve college readiness.

---

## Key Questions:
1. What is the distribution of scores across math, reading, and writing?
2. How do average scores compare across subjects?
3. Which NYC schools have the best math results? (≥ 640 / 800)
4. What are the top 10 performing schools based on combined SAT scores?
5. Which schools fall below NYC’s median SAT performance?
6. What is the performance gap between the highest and lowest schools?
7. Which boroughs have the highest and lowest average SAT scores?
8. Which single borough has the largest standard deviation in combined SAT scores? 
9. Is there a relationship between number of schools in a borough and its average SAT?
10. Do boroughs show consistent subject strengths (math vs reading vs writing)?
11. If we rank schools into quartiles by total SAT, what characteristics do top-quartile schools share vs bottom-quartile schools?
---

## Deliverables

* **Answers to 11 research questions** on NYC high-school SAT performance, using both **strict** (participation ≥50% & known) and **unscreened** views where relevant.
  
* **School-level analysis:** distributions (hist/box), medians & IQR (with means for context), subject comparisons, **high-math (≥640)** list, **top-10 total SAT**, and **below-median** tiering (near/moderate/far-below).
  
* **Borough-level analysis:** rankings (highest/lowest), means/medians, **dispersion** (IQR/SD), **subject strengths**, and stability across screens.
  
* **Gap analysis:** **max–min** extremes plus **robust spread** (IQR, p90–p10) to contextualize outliers.
  
* **Quartile breakdowns (Q1–Q4):** profiles by total SAT, subject medians, participation, and borough mix.
  
* **Participation-aware reporting:** `percent_tested`, `low_participation`, and `pt_note` flags; transparency via unscreened tables.
  
* **Reproducible Jupyter notebook** with clean preprocessing (column normalization, type coercion, `total_SAT` build, NA handling), structured code, and commentary.
  
* **Actionable recommendations for stakeholders** highlighting strengths, gaps, and where to focus resources.
---

## Data Dictionary: NYC School SAT Performance Metrics

* **school\_name:** *(string)* Name of the school.
  
* **borough:** *(string)* NYC borough the school is in.

* **building\_code:** *(string)* NYC DOE building/school code.
  
* **average\_math:** *(float, 0–800)* School’s average SAT Math score.
  
* **average\_reading:** *(float, 0–800)* School’s average SAT Reading score.
* **average\_writing:** *(float, 0–800)* School’s average SAT Writing score.
* **percent\_tested:** *(float, 0–100)* Percent of enrolled students who took the SAT. May be **NaN** if not reported.
* **total\_SAT:** *(float, 0–2400)* Sum of **average\_math + average\_reading + average\_writing** (uses available values; **NaN** only if all three are missing).
* **low\_participation:** *(bool)* Flag for **SAT participation below threshold** — `percent_tested < PT` when reported. Use to identify possibly **unrepresentative** results (small tested cohort) and to **exclude** rows in strict analyses. *(PT=50 by default.)*
* **pt\_note:** *(string)* Participation status shown in **unscreened** tables (no rows dropped):
  * `""` → meets threshold (≥ PT)
  * `"⚠️ <PT% tested"` → below threshold
  * `"(percent_tested NA)"` → participation missing
    *(PT=50 by default.)*
* **participation\_ok:** *(bool)* `True` when `percent_tested` is **reported** and **≥ PT**; `False` otherwise. Used to include rows in the **strict (participation-aware)** view. *(PT=50 by default.)*
---

## Dataset

* **File** data/schools.csv
* **Source:** Provided by DataCamp for educational purposes
* **Description:** NYC high-school SAT dataset with school/borough identifiers, **average subject scores** — Math, Reading, Writing (**0–800** each) — and **percent\_tested** (**0–100**, share of students who took the SAT). The project also derives **total\_SAT** (sum of the three subjects, **0–2400**) and participation flags used in the analysis.

## Requirements

* Python 3.12.7
* pip install -r requirements.txt
---

## How to Reproduce

1. **Get the data**
   * Place `data/schools.csv` in the repo’s `data/` folder.
     *(If your file lives elsewhere, update `CSV_PATH` at the top of the notebook.)*
2. **Open in JupyterLab (recommended)**
   * From the repo root, launch:
     
     jupyter lab
    
   * Open `nyc_schools_sat_score_case_study.ipynb`.
   * In JupyterLab, turn on the left **Table of Contents** via **View → Table of Contents**.
     *(Classic Jupyter Notebook doesn’t show this by default—use JupyterLab for the sidebar ToC.)*
3. **Run the analysis**
   * In the notebook, choose **Run → Run All Cells** (top to bottom).
4. **Inspect results**
   * Answers to **Q1–Q11** (plots, tables, insights, recommendations) appear inline under each section.

---

## Skills Demonstrated
- **Data wrangling**: Header normalization, type coercion, duplicate handling, and NA diagnostics.

- **Feature Engineering:** Created a combined total_SAT metric and participation flags (low_participation, pt_note, participation_ok).

* **Exploratory Data Analysis (EDA):** Distributions, skew, outliers; borough comparisons; top/bottom schools; quartile breakdowns.

* **Statistical Insights:** Applied central-tendency and variability metrics—mean, median, standard deviation, range, robust spread (IQR, p90–p10)—and Pearson/Spearman correlations to surface performance differences across schools and boroughs.

* **Data Visualization** Histograms/boxplots with median lines, ranked bars, scatter plots with annotations, and compact summary tables.

* **Comparative & ranking work:** Ranked boroughs (highest/lowest, dispersion), identified top math (≥640) and top-10 total SAT schools, tiered below-median schools, measured quartile gaps, evaluated school-level subject balance, and checked rank consistency across subjects (Spearman ρ).

* **Communication & reproducibility:** Per-question insights + “why this matters,” data dictionary, participation rules, and a reproducible JupyterLab notebook with clear structure.
---

## Summary of Insights

* **Distributions & center:** SAT scores are **right-skewed**; typical (median) subject scores sit in the **low–mid 400s** — **Math \~415**, **Reading \~413**, **Writing \~403**. Means are slightly higher than medians because a few top schools pull the right tail.
  
* **Variability:** **Math varies the most** across schools (widest IQR), while **Writing** is the lowest of the three subjects on average.
  
* **Top vs. bottom:** The **max–min school gap** is **\~1220 points** (2144–924), but the **typical spread** is much smaller (**IQR ≈ 170–214**, **p90–p10 ≈ 398–455**).
  
* **Participation matters, not the story:** Using a **strict view** (only schools with **percent\_tested ≥ 50%** and not missing) removes **\~28%** of below-median schools for low/unknown participation, yet **rankings and conclusions are essentially unchanged**; the unscreened view simply adds transparency with participation notes.
  
* **Below-median landscape:** Most below-median schools are **near (0–50 pts)** or **moderately (51–150)** below the city median; a **smaller tail (≥150)** drives the worst gaps.
  
* **Borough patterns:** **Staten Island** has the **highest** borough average; the **Bronx** the **lowest**. **Borough gaps are modest** (≈50–60 points) compared with **school-to-school** differences *within* boroughs. Dispersion is largest in **Manhattan/Staten Island** depending on view; **Brooklyn/Bronx** contain many below-median schools.
  
* **Size doesn’t predict performance:** The **number of schools** in a borough is **not correlated** with its average SAT.
  
* **Subject consistency by borough:** Borough rankings are **similar across math, reading, and writing** (high rank agreement), so strengths/weaknesses are **not** typically single-subject illusions.
  
* **Quartiles (Q1→Q4):** Median **total\_SAT** climbs by **\~+395 points** from bottom to top quartile; **participation rises** with performance. **Q1 over-indexes Bronx/Brooklyn**, **Q4** over-indexes **Manhattan/Queens/SI**.
  
* **Subject balance at school level:** Some schools are balanced across subjects; others have a **clear weakness in one area** (often writing). Quartiles reveal these patterns cleanly.

---

## Recommendations for Stakeholders

**For policymakers**
* Prioritize **school-level** supports where need is densest (especially **Bronx/Brooklyn**).
* Use the **strict view** (percent\_tested ≥ 50%) for reporting; publish an unscreened appendix for transparency.
* Set goals around **median/IQR** and **quartile mobility** (Q1→Q2→Q3→Q4), not just top-10 lists.

**For educators**
* Lift **writing** (lowest median) and manage **math variability** with coherent pathways + targeted tutoring.
* Borrow **portable practices** from exemplars (course sequencing, extended time, tutoring/club models).
* Plan supports by **gap-to-median tiers** (near/moderate/far-below) and track movement up tiers.

**For researchers**
* Study drivers of **within-borough spread** and **participation** (socio-economic factors, program access).
* Assess the impact of **screened/specialized** models using matched comparisons.
* Quantify which interventions (tutoring dosage, scheduling, coursework) move schools across quartiles.

**For parents/students**
* Compare schools using **median/IQR** and **participation %** (strict view), not just averages.
* Check **subject balance** (math vs. reading/writing) and a school’s **quartile** within its borough.
* Favor schools showing **consistent improvement** (quartile movement), not only headline ranks.
