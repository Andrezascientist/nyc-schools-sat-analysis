# NYC Schools SAT – Exploratory Case Study

**Author:** Andreza Eufrasio

**Stack:** Python, pandas, numpy, matplotlib. SciPy

**Notebook:** nyc_school_sat_score_case_study.ipynb

Analyze NYC schools’ SAT scores to uncover subject-level and overall performance patterns and provide clear, data-driven insights that can guide education policiy and family school choice.

---
## Business Context
Every year, U.S. high school students take the SAT, a standardized exam with three sections:reading, math, and writing; each scored up to 800 points. Analyzing school performance on these tests helps educators, policymakers, researchers, and families indetify excellences, gaps, and variability. In New York City, understanding SAT results across schools and boroughs supports data-driven decisions on resource allocation, program design, and school selection while advancing college-readiness efforts.

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
  
* **Actionable recommendations** highlighting strengths, gaps, and where to focus resources.
---

## Dataset

* **File** data/schools.csv
* **Source:** DataCamp for educational purposes
* **Description:** NYC high-school SAT dataset with school/borough identifiers, **average subject scores** — Math, Reading, Writing (**0–800** each) — and **percent\_tested** (**0–100**), share of students who took the SAT. The project derives **total\_SAT** (sum of the three subjects, **0–2400**) and the participation flags **low_participation, pt_note** and **participation_ok** used  for “strict vs. unscreened” analyses.
---

## Data Dictionary: NYC School SAT Performance Metrics

* **school\_name:** *(string)* School name.
  
* **borough:** *(string)* NYC borough.

* **building\_code:** *(string)* NYC DOE building/school code.
  
* **average\_math:** *(float, 0–800)* Average SAT Math score.
  
* **average\_reading:** *(float, 0–800)* Average SAT Reading score.
  
* **average\_writing:** *(float, 0–800)* Average SAT Writing score.
  
* **percent\_tested:** *(float, 0–100)* Percent of enrolled students who took the SAT; may be **NaN** if not reported.

**Derived in notebook**
  
* **total\_SAT:** *(float, 0–2400)* Sum of **average\_math + average\_reading + average\_writing** (uses available values; **NaN** only if all three are missing).
  
* **low\_participation:** *(bool)* Flag for **SAT participation below threshold** — `percent_tested < PT` when reported; highlights potentially **unrepresentative** results and used to **exclude** rows in strict analyses. *(PT=50 by default.)*
  
* **pt\_note:** *(string)* Participation status in **unscreened** tables (no rows dropped):
  * `""` → meets threshold (≥ PT)
  * `"⚠️ <PT% tested"` → below threshold
  * `"(percent_tested NA)"` → participation missing
    *(PT=50 by default.)*
    
* **participation\_ok:** *(bool)* `True` when `percent_tested` is **reported** and **≥ PT**; `False` otherwise. Used to include rows in the **strict (participation-aware)** view. *(PT=50 by default.)*
---

## Requirements

* Python 3.12.7
* pip install -r requirements.txt
---

## How to Reproduce

### Option A — JupyterLab (recommended)

1. **Get the data:** place `data/schools.csv` in the repo’s `data/` folder.
   *(If your file lives elsewhere, update `CSV_PATH` at the top of the notebook.)*
2. **Launch JupyterLab** from the repo root:


   ```bash
   jupyter lab
   ```

   
3. **Open** `nyc_schools_sat_score_case_study.ipynb`.
4. In JupyterLab, enable the left **Table of Contents** via **View → Table of Contents**.
5. **Run the analysis:** **Run → Run All Cells** (top to bottom).
6. **Inspect results:** Answers to **Q1–Q11** (plots, tables, insights, recommendations) appear under each section.

### Option B — Start in Classic Notebook, then switch to JupyterLab

1. Launch Classic Notebook:


   ```bash
   jupyter notebook
   ```
   
2. Open `nyc_schools_sat_score_case_study.ipynb`.
3. In the top menu, choose **View → Open in JupyterLab** to switch.
   *(This opens the same notebook in JupyterLab so you can use the sidebar Table of Contents.)*
4. Then follow steps **4–6** from **Option A**. 
---


## Skills Demonstrated
- **Data wrangling**: Header normalization, type coercion, duplicate handling, and NA diagnostics.

- **Feature Engineering:** Build **total_SAT** and participation flags (**low_participation, pt_note, participation_o**).

* **Exploratory Data Analysis (EDA):** Distributions, skew, outliers; borough comparisons; top/bottom schools; quartile breakdowns.

* **Statistical Insights:** Central-tendency and variability metrics: mean, median, standard deviation, range, robust spread (IQR, p90–p10) and Pearson/Spearman correlations.

* **Data Visualization** Histograms/boxplots with median lines, ranked bars, scatter plots, and ompact summary tables.

* **Comparative & ranking work:** Boroughs ranking (highest/lowest, dispersion), top math (≥640) and top-10 total SAT list, below-median tiering, quartile gaps, subject-rank consistency (Spearman ρ).

* **Communication & reproducibility:** Per-question insights and “why this matters,” data dictionary, participation rules, and a clean, reproducible JupyterLab notebook.
---

## Summary of Insights

* **Distributions & center:** SAT scores are **right-skewed**; typical (median) subject scores sit in the **low–mid 400s** — **Math \~415**, **Reading \~413**, **Writing \~403**. Means are slightly higher than medians because a few top schools pull the right tail.
  
* **Variability:** **Math varies the most** across schools (widest IQR); **Writing** is the lowest on average.
  
* **Top vs. bottom:** The **max–min gap** across schools is **\~1220 points** (2144–924), but the **typical spread** is much smaller (**IQR ≈ 170–214**, **p90–p10 ≈ 398–455**).
  
* **Participation matters, not the story:** A **strict view** (**percent\_tested ≥ 50%** & not missing) removes **\~28%** of below-median schools, yet conclusions and rankings are **stable**; unscreened adds participation context.
  
* **Below-median landscape:** Most schools are **near (0–50 pts)** or **moderately (51–150)** below the median; a **smaller tail (≥150)** drives the worst gaps.
  
* **Borough patterns:** **Staten Island** has the **highest** borough average; the **Bronx** the **lowest**. **Borough gaps are modest** (≈50–60 points) vs **within-borough** schools differences. Dispersion is largest in **Manhattan/Staten Island** (by view); **Brooklyn/Bronx** house many below-median schools.
  
* **Size ≠ performance:** The **number of schools** in a borough is **not correlated** with its average SAT.
  
* **Subject consistency:** Borough ranks are **similar across math, reading, and writing** (high rank agreement).
  
* **Quartiles (Q1→Q4):** Median **total\_SAT** climbs by **\~+395 points** bottom to top; **participation rises** with performance. **Q1** over-indexes **Bronx/Brooklyn**, **Q4** over-indexes **Manhattan/Queens/SI**.
  
* **Subject balance (school level):** Some schools are balanced across subjects; others have a **clear single-subject weakness** (often writing). 
---

## Recommendations for Stakeholders

**For policymakers**
* Prioritize **school-level** supports where need is densest (especially **Bronx/Brooklyn**).
* Use the **strict view** for reporting; publish an unscreened appendix for transparency.
* Set goals around **median/IQR** and **quartile mobility** (Q1→Q2→Q3→Q4).

**For educators**
* Lift **writing** (lowest median) and manage **math variability** via coherent pathways and targeted tutoring.
* Borrow **portable practices** from exemplars (course sequencing, extended time, tutoring/club models).
* Plan supports by **gap-to-median tiers** (near/moderate/far-below) and track movement up tiers.

**For researchers**
* Study drivers of **within-borough spread** and **participation** (socio-economic factors, program access).
* Evaluate the impact of **screened/specialized** models using matched comparisons.
* Quantify which interventions move schools across quartiles.

**For parents/students**
* Compare schools using **median/IQR** and **participation %** (strict view), not just averages.
* Check **subject balance** and a school’s **quartile** within its borough.
* Favor schools showing **consistent improvement** (quartile movement), not only headline ranks.
