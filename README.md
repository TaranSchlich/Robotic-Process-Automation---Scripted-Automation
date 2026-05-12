# Demographic-Based Clinical Trial Site Selection

Python automation that scores and ranks U.S. counties as clinical trial site candidates using 2020 Census demographic data. Built to help healthcare and drug development organizations identify where to focus recruitment when a drug targets receptors or conditions that vary by demographic group.

## Business Problem

Drug developers and clinical researchers need to know *where* their target population lives before activating trial sites. Manually cross-referencing Census data across 3,000+ counties to assess diversity, underrepresented population share, and recruitment feasibility is impractical. This automation ingests the raw Census file, computes three scored dimensions for every county, and surfaces the highest-potential sites in seconds — work that would otherwise take hours in a spreadsheet.

It answers questions like:
- *Where in the U.S. should we prioritize clinical trial sites for a drug designed for a specific demographic?*
- *Does our candidate site population reflect the population likely to use this drug?*
- *Which counties offer both high diversity and sufficient population to support recruitment?*

## Why Demographic Data Matters in Drug Development

**Genetic variation** — Variants in drug-metabolizing enzymes (CYP450), receptor expression, and immune markers occur at different frequencies across ancestral backgrounds, affecting safety, efficacy, and dosing.

**Disease prevalence** — Conditions like sickle cell disease (more common in African ancestry), cystic fibrosis (Northern European ancestry), and Type 2 diabetes (Hispanic/Latino and Native American populations) disproportionately affect specific groups, making representative recruitment essential.

## Dataset

**Source:** U.S. Census Bureau — 2020 Decennial Census Demographic and Housing Characteristics (DHC)  
**Table:** P9 — Hispanic or Latino, and Not Hispanic or Latino by Race  
**Coverage:** All 3,221 U.S. counties  
**File:** `DECENNIALDHC2020.P9-2026-04-06T011050.csv`

## Notebook

[Open in Google Colab](https://colab.research.google.com/drive/12RnIYKNSPgBxXV8IVd3Q51UnCPHrmJRo?usp=sharing)

## Video Walkthrough

[Watch on Loom](https://www.loom.com/share/6fb96e7483e74e4db0bcec01a51290ef)

## How It Works

### 1. Load & Clean
The Census CSV is loaded and column names are normalized (lowercase, underscores, stripped whitespace).

### 2. Reshape
The wide-format file (counties as columns, demographic labels as rows) is melted into long format and pivoted into a county-per-row analysis table.

### 3. Convert to Numeric
A loop iterates over all demographic columns, strips comma formatting, and casts values to float.

### 4. Compute Ratios
Every demographic count is divided by the county total to produce a population share ratio for each group.

### 5. Score Each County

| Score | Formula | Weight in Final Score |
|---|---|---|
| **Diversity score** | `1 − (largest single group ratio)` | 40% |
| **Underrepresented score** | Sum of ratios for Hispanic/Latino, Black, AIAN, Asian, NHOPI, multiracial groups | 40% |
| **Population scale** | County total ÷ national max | 20% |

### 6. Filter & Rank
Counties below 50,000 residents are excluded. The remaining counties are ranked by combined site potential score.

### 7. Visualize
- Bar chart: Top 10 counties by site potential score
- Scatter plot: Diversity score vs. population size

## Scoring Rationale

The 40/40/20 weighting balances three factors that matter in trial design:
- **Representation** — broad diversity ensures results generalize across populations
- **Equity** — high underrepresented-group share aligns with FDA Diversity Action Plan and NIH inclusion requirements
- **Feasibility** — minimum population thresholds ensure enough eligible participants exist

## Limitations

- Census data is from 2020; population shifts since then may reduce accuracy
- County-level analysis may obscure neighborhood-level variation; census tracts or ZIP codes would be more precise
- Socioeconomic factors (income, insurance coverage, healthcare access) that affect recruitment are not included
- Some demographic categories overlap (e.g., Hispanic individuals may also appear in racial subcategories)

## Files

| File | Description |
|------|-------------|
| `DECENNIALDHC2020.P9-2026-04-06T011050.csv` | Input — 2020 Census Table P9 county-level demographic data |

## Tools & Libraries

- Python 3
- pandas
- NumPy
- Matplotlib (via pandas `.plot`)
- Google Colab
