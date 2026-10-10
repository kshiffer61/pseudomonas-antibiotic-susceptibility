# Antibiotic susceptibility in Pseudomonas aeruginosa

Exploratory analysis of Basel respiratory laboratory samples (2015-2018),
using conditional probability to estimate the added coverage of antibiotic pairs.

## Analyses

- **Main_Analysis.Rmd:** sampling frequency, joint results, conditional
  probabilities, added coverage, and a binomial likelihood heatmap.
- **Antibiotic_Comparisons.Rmd:** testing availability and a common-sample
  comparison of five drugs, with 2x3 added-coverage and total-coverage heatmaps.
- **scripts/prepare_data.R:** pinned downloads, cleaning, one result per
  laboratory order, and first eligible order per patient-year.

The reports show their analysis code. Figures and numerical summaries are
written to outputs/figures/ and outputs/tables/.

## Run

Keep the folder together. Open either Rmd in RStudio and click Knit, or run
the following from this directory:

```r
install.packages(c("rmarkdown", "knitr", "dplyr", "tidyr", "readr", "ggplot2"))
rmarkdown::render("Main_Analysis.Rmd")
rmarkdown::render("Antibiotic_Comparisons.Rmd")
```

The notebooks run independently. Missing source files are downloaded to
data/cache/; the download cache is excluded by .gitignore.

## Data and cohorts

Source: [DRIAMS antibiotic results](https://github.com/gvisona/MultimodalAMR/blob/209bcfc8d09da0f954d396f29b7601e37bf5fc15/processed_data/DRIAMS_combined_long_table.csv)
and [Basel annual metadata](https://github.com/BorgwardtLab/maldi_amr/tree/bcd88097f1962bac594324edea4d0b8b240c5507/amr_maldi_ml/DRIAMS_preprocessing/id_files/stratification).
The script pins both sources to commits.

Clear responses are coded 0 = susceptible, 1 = nonsusceptible. Mixed and missing
pip-tazo entries are unclassified. Conflicting clear measurements of an order
are unclassified; a single clear result is retained when other measurements
are missing. Each patient contributes the first eligible order within a year.

| Analysis | Eligibility | N | Pip-tazo NS | Added cipro coverage |
|---|---|---:|---:|---:|
| Main | Pip-tazo and cipro results | 350 | 56 | 34/350 |
| Comparisons | All five selected results | 349 | 57 | 35/349 |

Eligibility is evaluated separately: the comparison cohort can select a later
order and is not simply the main cohort minus one observation. Coverage uses
historical laboratory labels and describes susceptibility rather than clinical
recovery. Testing frequency does not measure prescribing frequency.

The main jittered plot adapts the course's empirical-conditioning diagram.
Point displacement is for display only. The repeat-sampling dotplot and stacked
proportion bars follow the visualization approaches in Ciprian Crainiceanu's
Lecture 10 (October 8, 2026). Histograms, density estimates, and QQ plots are
omitted for the binary drug outcomes.
