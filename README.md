# Robotic Process Automation — Scripted Automation

Python automation that processes 2020 U.S. Census demographic data (Table P9) to analyze Hispanic/Latino and racial composition across U.S. counties, generating filtered summaries and county-level reports for market research and demographic decision-making.

## Business Problem

Organizations conducting market research, resource allocation, or diversity reporting need quick access to county-level demographic breakdowns. Manually downloading and parsing Census Bureau data for hundreds of counties is time-consuming and error-prone. This automation ingests the raw Census Table P9 file, loops through demographic categories and counties, and produces clean, readable summaries — turning hours of manual work into a repeatable one-click process.

## Dataset

**Source:** U.S. Census Bureau — 2020 Decennial Census Demographic and Housing Characteristics (DHC)  
**Table:** P9 — Hispanic or Latino, and Not Hispanic or Latino by Race  
**Coverage:** All U.S. counties  
**File:** `DECENNIALDHC2020.P9-2026-04-06T011050.csv`

## Notebook

[Open in Google Colab](https://colab.research.google.com/drive/12RnIYKNSPgBxXV8IVd3Q51UnCPHrmJRo?usp=sharing)

## Video Walkthrough

[Watch on Loom](https://www.loom.com/share/6fb96e7483e74e4db0bcec01a51290ef)

## Features

- Loads and parses the Census CSV with pandas
- Loops through demographic groupings (Hispanic/Latino, racial subcategories) for each county
- Filters and ranks counties by population share for a selected demographic group
- Outputs a formatted summary report

## Files

| File | Description |
|------|-------------|
| `DECENNIALDHC2020.P9-2026-04-06T011050.csv` | Input — 2020 Census Table P9 county-level data |

## Tools & Libraries

- Python 3
- pandas
- Google Colab
