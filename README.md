# NYC Schools SAT – Exploratory Case Study


<img width="400" height="300" alt="schoolbus" src="https://github.com/user-attachments/assets/18d86098-2ed8-4dd9-96be-913a94ce94aa" />


**Author:** Andreza Eufrasio

**Stack:** python, pandas, numpy, matplotlib, iPython, sciPy

**Notebook:** [nyc_school_sat_score_case_study.ipynb](nyc_school_sat_score_case_study.ipynb)

Analysis of NYC high school SAT scores to identify subject-level and overall performance patterns across schools and boroughs.

---

## Business Context

Every year, U.S. high school students take the SAT, a standardized exam with three sections: reading, math, and writing, each scored up to 800 points.

This project explores SAT performance across New York City public schools to identify differences among schools and boroughs, examine subject-level patterns, and investigate participation and score variability.

---

## Key Questions:

1. What is the distribution of scores across math, reading, and writing?
2. How do average scores compare across subjects?
3. Which NYC schools have the best math results? (≥ 640 / 800)
4. What are the top 10 performing schools based on combined SAT scores?
5. Which schools fall below NYC’s median SAT performance?
6. What is the performance gap between the highest- and lowest-performing schools?
7. Which boroughs have the highest and lowest average SAT scores?
8. Which borough has the largest variation in combined SAT scores?
9. Is there a relationship between number of schools in a borough and its average SAT score?
10. Do boroughs show consistent performance across math, reading, and writing?
11. Which schools fall into the lowest SAT quartile, and what characteristics distinguish them?

---

## Dataset

* **File** data/schools.csv
* **Source:** DataCamp for educational dataset

The dataset contains NYC high school SAT results, including:

* **Description:** NYC high-school SAT dataset with school/borough identifiers
* **average subject scores** — Math, Reading, Writing (**0–800** each) 
* **percent\_tested** (**0–100**), share of students who took the SAT
* The project derives **total\_SAT** (sum of the three subjects, **0–2400**) and the participation flags **low_participation, pt_note** and **participation_ok** used  for “strict vs. unscreened” analyses.
  
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

## Analysis

The project includes:

- Data cleaning and validation
- Feature engineering for total SAT scores and participation categories
- Exploratory analysis of score distributions and variability
- School-level performance comparisons
- Borough-level comparisons
- Top- and bottom-performing school analysis
- Quartile analysis
- SAT participation analysis
- Correlation and rank-consistency analysis

---

## Summary of Insights

- **Score distribution:** SAT scores are right-skewed, with typical subject scores in the low-to-mid 400s.

- **Subject performance:** Math shows the greatest variability across schools, while writing has the lowest average score.

- **Performance gap:** A substantial gap exists between the highest- and lowest-performing schools, although most schools are much closer to the citywide median.

- **Participation:** SAT participation varies across schools, but applying a stricter participation threshold does not substantially change the overall performance patterns.

- **Borough patterns:** Staten Island has the highest average SAT performance and the Bronx the lowest. Differences among schools within the same borough are larger than the differences between borough averages.

- **Borough size:** The number of schools in a borough is not correlated with its average SAT performance.

- **Subject consistency:** Borough rankings are similar across math, reading, and writing.

- **Subject balance:** Some schools perform consistently across subjects, while others show a clear weakness in one subject, most often writing.

---

## Requirements

- Python 3.12.7
- Dependencies listed in `requirements.txt`

Install the required packages with:

```bash
pip install -r requirements.txt
```

---

## How to Reproduce

1. Clone or download this repository.
2. Make sure `schools.csv` is located in the `data/` folder.
3. Install the required dependencies:

```bash
pip install -r requirements.txt
```

4. Launch JupyterLab:

```bash
jupyter lab
```

5. Open `nyc_school_sat_score_case_study.ipynb`.
6. Run the notebook from top to bottom.
