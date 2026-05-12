# Demographic-Based Site Selection Automation

This notebook simulates how a healthcare or drug development company could use demographic data to decide where to focus clinical research and marketing efforts for a drug that targets receptors more common in certain demographic groups.

Using U.S. Census-based demographic data by county, it identifies which counties have the largest populations for each demographic group to answer questions like:

- *If our drug is designed for a specific demographic, where in the U.S. should we prioritize clinical trial sites and outreach?*
- *If a drug is biologically more effective in a certain demographic due to genetic or epidemiological factors, where does that population live?*
- *Where in the U.S. can we find the highest concentration of the population our drug is intended for?*
- *Does the study population reflect the population likely to use the drug?*

## Why Demographic Data Matters in Drug Development

**1. Genetic Variation Across Populations**

Certain genetic variants that influence how people respond to medications occur at different frequencies across ancestral backgrounds — including differences in drug-metabolizing enzymes (such as CYP450 variants), receptor expression, and immune-related markers. Because these biological factors can affect a drug's safety, efficacy, or optimal dosing, understanding where these populations live helps researchers plan clinical trials that include the right participants.

**2. Differences in Disease Prevalence**

Many diseases occur at higher rates in specific demographic groups. Sickle cell disease is more common in individuals of African ancestry, cystic fibrosis is more common in people of Northern European ancestry, and Type 2 diabetes is more prevalent in Hispanic/Latino and Native American populations. When a drug treats a condition that disproportionately affects a particular group, identifying where those populations are concentrated is essential for adequate recruitment and representative results.

## Dataset

**Source:** U.S. Census Bureau — 2020 Decennial Census Demographic and Housing Characteristics (DHC)  
**Table:** P9 — Hispanic or Latino, and Not Hispanic or Latino by Race  
**Coverage:** All 3,221 U.S. counties  
**Link:** https://data.census.gov/table/DECENNIALDHC2020.P9?t=Race+and+Ethnicity&g=010XX00US$0500000  
**File:** `DECENNIALDHC2020.P9-2026-04-06T011050.csv`

## Notebook

[Open in Google Colab](https://colab.research.google.com/drive/12RnIYKNSPgBxXV8IVd3Q51UnCPHrmJRo?usp=sharing)

## Video Walkthrough

[Watch on Loom](https://www.loom.com/share/6fb96e7483e74e4db0bcec01a51290ef)

## How It Works

1. **Load & reshape** — The wide-format Census CSV (counties as columns, demographic labels as rows) is melted and pivoted into a county-per-row analysis table
2. **Convert to numeric** — A loop strips comma formatting and casts all demographic columns to float
3. **Compute ratios** — Every demographic count is divided by county total to produce population share ratios
4. **Score counties** across three dimensions:

| Score | What It Measures | Weight |
|---|---|---|
| Diversity score | `1 − largest single group ratio` — how evenly groups are represented | 40% |
| Underrepresented score | Combined share of Hispanic/Latino, Black, AIAN, Asian, NHOPI, and multiracial populations | 40% |
| Population scale | County total relative to the national maximum — ensures recruitment feasibility | 20% |

5. **Filter** — Counties under 50,000 residents are excluded to ensure viable recruitment pools
6. **Rank & visualize** — Top counties are ranked by combined site potential score with bar and scatter plots

## Scoring Rationale

The 40/40/20 weighting balances representation, equity, and feasibility — three critical factors in clinical trial site selection. Diversity and underrepresented share are weighted equally to align with FDA Diversity Action Plan and NIH inclusion requirements, while population size ensures that selected counties can actually support recruitment.

## Limitations

- **Census data age** — The dataset is from 2020; population shifts since then may affect accuracy
- **County-level granularity** — Counties can contain highly diverse neighborhoods; finer units (ZIP codes, census tracts) would provide more precise insights
- **Socioeconomic factors not included** — Income, education, insurance coverage, and healthcare access also influence recruitment feasibility
- **Overlap between groups** — Some demographic categories overlap (e.g., Hispanic individuals may also be counted in racial categories)
- **Assumed linear scaling** — Population scaling assumes feasibility increases linearly with population size, which may not always hold

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
