# Evolution of the Center in the NBA

An analysis of how the center position has changed since the introduction of the three-point line, using ANOVA, principal component analysis, hierarchical clustering, and ARIMA time series forecasting.

---

## Motivation

The modern NBA center looks nothing like the centers of the 1980s and 1990s. Where Patrick Ewing and Hakeem Olajuwon defined success through interior dominance, today's centers, such as Nikola Jokić, Joel Embiid, and Karl-Anthony Towns, are expected to shoot from the perimeter, facilitate offense, and space the floor. But is this shift real and quantifiable, or more narrative than statistical reality?

This project examines four decades of NBA center statistics to test whether the position has genuinely changed, identify distinct center archetypes across that period, and forecast where the position is headed.

---

## Analysis Overview

The full analysis is contained in `evolution_of_the_center.Rmd`, which knits to a self-contained HTML document. It proceeds in four stages:

**1. Era Comparisons (ANOVA)**
One-way ANOVA with Tukey HSD post-hoc comparisons tests whether centers from different decades differ significantly in three-point attempts, assists per 36 minutes, defensive win shares, and total rebounds. Results confirm that the 2010s+ era is significantly different from all prior decades on offensive metrics, with the shift concentrated in the most recent era rather than being a gradual trend.

**2. Dimension Reduction (PCA)**
With over 40 statistical variables in the dataset, principal component analysis reduces dimensionality before clustering. Six components were retained, explaining over 75% of the total variance, with interpretable structure around scoring efficiency, three-point shooting, and defensive production.

**3. Clustering (Hierarchical / Ward's Method)**
Hierarchical clustering on the PCA components identifies five distinct center archetypes. The average season year of the scoring and three-point shooting clusters falls in 2013 and 2017 respectively, confirming that these archetypes are predominantly recent phenomena.

**4. Time Series Forecasting (ARIMA)**
ARIMA models fit to the yearly proportion of centers belonging to each cluster project the future composition of the position. Scoring and shooting cluster proportions are forecast to grow; the traditional defensive and rebounding cluster is forecast to shrink.

---

## Technical Stack

| Component | Tools |
|---|---|
| Data wrangling | R, `dplyr` |
| Era comparisons | Base R `aov`, `TukeyHSD` |
| PCA | `FactoMineR` |
| Clustering | `FactoMineR` (`HCPC`), Ward's criterion |
| Visualization | `ggplot2`, `factoextra` |
| Time series | `forecast` (`auto.arima`) |

---

## Repository Structure

```
├── README.md
├── evolution_of_the_center.Rmd   # Full analysis document
└── screenshots/
    ├── screenshot_clusters.png
    ├── screenshot_arima.png
    └── screenshot_boxplots.png
```

---

## Data

Data was sourced from [Basketball Reference](https://www.basketball-reference.com/) and contains season averages for all NBA players from 1950 to 2022. The analysis filters to centers only, seasons from 1980 onward, and players who appeared in at least half their team's games.

The raw data file is not included in this repository. To reproduce the analysis, download the season averages data from Basketball Reference and save it as `season_stats.csv` in the repository root.

---

## Running the Analysis

With `season_stats.csv` in place, open `evolution_of_the_center.Rmd` in RStudio and knit to HTML. Required packages:

```r
install.packages(c("dplyr", "ggplot2", "factoextra", "FactoMineR", "cluster", "forecast"))
```
