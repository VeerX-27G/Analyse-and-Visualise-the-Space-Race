# 🚀 Analyse and Visualise the Space Race

Exploratory data analysis of every space mission launched since the start of the Space Race between the USA and the Soviet Union in 1957, built with **pandas** and **Plotly** in a single Jupyter notebook.

![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?logo=pandas&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-3F4F75?logo=plotly&logoColor=white)

## Overview

The dataset was scraped from [nextspaceflight.com](https://nextspaceflight.com/launches/past/?page=1) and records the organisation, launch site, date, rocket, cost and outcome of each mission. This project cleans it, wrangles launch locations into country codes, and visualises who launched what, where, at what cost, and how often it went wrong.

### Questions explored

1. Who launched the most missions in any given year?
2. How has the cost of a space mission varied over time?
3. Which months are the most popular for launches?
4. Have space missions gotten safer, or has the chance of failure remained unchanged?

## What's in the notebook

| Section | What it does | Visual |
|---|---|---|
| Data exploration & cleaning | Checks shape, columns, NaNs and duplicates; drops junk index columns | - |
| Launches per organisation | Ranks organisations by number of launches | Horizontal bar chart |
| Active vs. retired rockets | Compares rockets still in service with decommissioned ones | Counts |
| Mission status | Success vs. failure totals | Counts |
| Launch cost distribution | Distribution of launch prices (USD millions) | Histogram |
| Launches by country | Parses the country from each launch location and converts it to an ISO alpha-3 code | Choropleth map |
| Failures by country | Same map, filtered to failed missions | Choropleth map |
| Country → organisation → outcome | Hierarchical breakdown of every mission | Sunburst chart |
| Spending by organisation | Total money spent per organisation | Horizontal bar chart |

## Dataset

`mission_launches.csv`, originally 4,324 rows × 9 columns.

| Column | Description |
|---|---|
| `Organisation` | Company or agency that ran the mission (e.g. NASA, SpaceX, CASC) |
| `Location` | Launch site, ending in a country or region name |
| `Date` | Launch date and time (UTC) |
| `Detail` | Rocket and payload |
| `Rocket_Status` | `StatusActive` or `StatusRetired` |
| `Price` | Launch cost in **USD millions** (missing for many missions) |
| `Mission_Status` | `Success`, `Failure`, `Partial Failure` or `Prelaunch Failure` |

The file also contains two leftover index columns (`Unnamed: 0`, `Unnamed: 0.1`) that are dropped during cleaning.

> **Note:** the CSV is not committed to this repo. Download or export the dataset and place it next to the notebook as `mission_launches.csv` before running.

## Selected results

Figures below come from the rows that have a reported price (964 of the original 4,324 missions), so they describe priced launches rather than all launches.

- **Most launches:** CASC (158), NASA (149), SpaceX (99), ULA (98), Arianespace (96)
- **Outcomes:** 910 successes against 36 outright failures (partial and prelaunch failures are tracked separately)
- **Rocket status:** 586 active vs. 378 retired
- **Launch cost:** median ≈ $62M, mean ≈ $130M, ranging from about $5M to $450M
- **Spending:** NASA accounts for roughly $61B of the ≈ $123B total across priced launches, followed by Arianespace and ULA

## Getting started

```bash
git clone https://github.com/VeerX-27G/Analyse-and-Visualise-the-Space-Race.git
cd Analyse-and-Visualise-the-Space-Race

pip install requirements.txt
```

Add `mission_launches.csv` to the project folder, then launch the notebook:

```bash
jupyter notebook "Space_Missions_Analysis_(start).ipynb"
```

Running on Google Colab? Execute the "Upgrade Plotly" cell at the top first.

## Project structure

```
.
├── Space_Missions_Analysis_(start).ipynb   # Full analysis
├── mission_launches.csv                    # Dataset (add this yourself)
├── README.md
└── .gitignore
```

## Tech stack

- **pandas / NumPy** for cleaning and aggregation
- **Plotly Express** for interactive charts, maps and the sunburst
- **iso3166** for converting country names to ISO alpha-3 codes
- **Matplotlib / Seaborn** imported for static plots

## Data notes and limitations

- Location strings are mapped to countries by taking the last comma-separated token, with manual fixes for names that no longer exist or aren't countries (for example *Russia* → Russian Federation, *Yellow Sea* → China, *New Mexico* → USA, *Barents Sea* → Russian Federation). Missions launched from Baikonur are counted under **Kazakhstan**, not Russia.
- `Price` is unreported for most missions, and dropping those rows shrinks the dataset considerably. Treat counts and rankings as a view of priced missions, not a complete census.

## Acknowledgements

Data courtesy of [nextspaceflight.com](https://nextspaceflight.com/).
