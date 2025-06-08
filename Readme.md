# NIH Budget Alluvial

This repository explores how the recently proposed restructuring of the National Institutes of Health (NIH) fits into decades of historical funding patterns.  In March 2025, HHS unveiled the “Make America Healthy Again” reorganization, which collapses the 27 existing NIH institutes and centers into eight new institutes and realigns several functions.  We asked: **How do those new groupings compare to NIH’s budget trajectory back to FY 2000?**

## How the Analysis Works

1. **Data Ingestion**  
   - **`budgets.csv`**: Contains historical budgets for each *old* IC in FY 2000, 2010, 2020, 2024, plus the FY 2026 proposed totals at the *new institute* level (from the HHS FY 2026 Budget in Brief).  
   - **`mapping.csv`**: Maps each *old* IC into its proposed FY 2026 *new institute*.

2. **Proportional Allocation of FY 2026**  
   - We sum each new institute’s total FY 2026 request.  
   - For each *old* IC in a group, we calculate
     ```math
     \text{IC}_{2026} = \frac{\text{IC}_{2024}}{\sum_{\text{group}} \text{IC}_{2024}} \;\times\; \text{NewInstitute}_{2026}.
     ```
   - This gives every old IC a “destination” value in 2026, so ribbons can flow into the correct new‐institute node.

3. **Building the Alluvial (“Lodes”) Data**  
   - We combine the four historical years (2000–2024) at the *old* IC level with the apportioned FY 2026 flows.  
   - We order strata so that, in each column, institutes are stacked by their FY 2026 group (smallest → largest), and within each group the old ICs are ordered by their FY 2024 size.

4. **Plotting**  
   - A single `ggplot2 + ggalluvial` call renders five vertical slices (2000, 2010, 2020, 2024, 2026), with colored ribbons tracing each IC’s budget over time into its new institute.

5. **Interactive Table**  
   - We include a **DT** table of the final lodes data so you can sort, search, and inspect every flow.

## Motivation & Links

- **HHS FY 2026 Budget in Brief**  
  President’s request and proposed NIH totals:  
  https://www.hhs.gov/sites/default/files/fy-2026-budget-in-brief.pdf

- **Fact Sheet: HHS’ Transformation to Make America Healthy Again**  
  Overview of the reorganization, including NIH workforce changes:  
  https://www.hhs.gov/press-room/hhs-restructuring-doge-fact-sheet.html

- **NIH Historical Appropriations**  
  IC‐level budget history going back to FY 1938:  
  https://www.nih.gov/about-nih/nih-almanac/appropriations-section-1

- **CRS Report: NIH Funding FY1996–FY2025**  
  Congressional Research Service summary of recent trends:  
  https://crsreports.congress.gov/product/pdf/R/R43341

## Files in This Repo

- **`budgets.csv`** — Raw IC budgets and FY 2026 proposal totals  
- **`mapping.csv`** — Old → new institute assignments  
- **`plot_data.csv`** — Prepared “lodes” data for plotting  
- **`nih_budget_alluvial.Rmd`** — R Markdown with analysis, static figure, and interactive table  
- **`nih_budget_alluvial.html`** — Knit output ready for GitHub Pages

---

*This work lets you see not only how much each IC has grown or shrunk over the last 25 years, but also exactly how its funding “flows” into the new institute structure proposed for FY 2026.*  

# Attribution
This project was written and coded using ChatGPT o4-mini-high, and fixed by me to actually get it to work. You can read the entire chat [here](https://chatgpt.com/share/68459935-01b8-8012-bffc-9bf730d6f977).
