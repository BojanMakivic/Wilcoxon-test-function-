# Wilcoxon-test-function

A small R function to run Wilcoxon non-parametric tests and produce a clear graphical summary. The function is intended to make it easy to perform Wilcoxon signed-rank or Wilcoxon rank-sum (Mann–Whitney) tests using data stored in a simple Excel spreadsheet, speeding up routine statistical analyses and producing publication-ready visuals.

## Features
- Run Wilcoxon signed-rank test (paired) or Wilcoxon rank-sum / Mann–Whitney test (unpaired).
- Accepts data read from Excel (.xlsx/.xls) or a data.frame.
- Returns test statistics and p-values in a tidy format.
- Produces a ggplot2-based visualization that illustrates group distributions and test results.
- Minimal dependencies and easy to integrate into analysis scripts.

## Requirements
- R (>= 3.6)
- Recommended packages:
  - readxl (to read Excel files)
  - dplyr (data manipulation)
  - ggplot2 (visualization)
  - tidyr (optional, data reshaping)
  - stats (base R, for wilcox.test)

Install any missing packages with:
```r
install.packages(c("readxl", "dplyr", "ggplot2", "tidyr"))
```

## Data format
The Excel file or data.frame should be in long format. Each row represents a single observation and you should have:
- One column indicating the group or condition (e.g., "Group" or "Condition").
- One column with the numeric measurement values (e.g., "Value").
- For paired tests, an identifier column for each pair (e.g., "SubjectID") is recommended.

Example (long format):
| SubjectID | Group  | Value |
|-----------|--------|-------|
| 1         | before | 5.2   |
| 1         | after  | 6.1   |
| 2         | before | 4.8   |
| 2         | after  | 5.0   |

For unpaired tests:
| Group | Value |
|-------|-------|
| A     | 3.2   |
| A     | 4.1   |
| B     | 5.0   |
| B     | 4.8   |

## Usage

Below are general usage examples showing how to:
1. Read data from Excel.
2. Call the Wilcoxon test function.
3. Inspect results and plot output.

Replace FUNCTION_NAME with the actual function name from the repository (e.g., `wilcoxon_test_function`).

### 1) Read data from Excel
```r
library(readxl)
dat <- read_excel("data/my_measurements.xlsx", sheet = 1)
```

### 2) Example: Paired Wilcoxon signed-rank test
This assumes your data include a SubjectID column and a Group column with two levels (e.g., "before", "after").
```r
# Example function call - replace FUNCTION_NAME with the actual function name
res <- FUNCTION_NAME(
  data = dat,
  value_col = "Value",
  group_col = "Group",
  id_col = "SubjectID",   # use for paired tests
  paired = TRUE,
  alternative = "two.sided" # or "less", "greater"
)

print(res$test)    # test summary (statistic, p-value)
print(res$summary) # group summaries (medians, n)
# Plot results
print(res$plot)
```

### 3) Example: Unpaired Wilcoxon rank-sum test (Mann–Whitney)
```r
res_unpaired <- FUNCTION_NAME(
  data = dat,
  value_col = "Value",
  group_col = "Group",
  paired = FALSE,
  alternative = "two.sided"
)

print(res_unpaired$test)
print(res_unpaired$summary)
print(res_unpaired$plot)
```

Notes
- The structure of the returned object may include:
  - $test: a list or data.frame with test statistic, p-value, method description and alternative.
  - $summary: group-level descriptive stats (n, median, IQR).
  - $plot: a ggplot object showing group distributions (violin/box/dot plots) and annotated p-value.

## Output interpretation
- Wilcoxon test statistic: For the signed-rank test it is typically labelled V; for rank-sum it may be labelled W or U depending on the implementation.
- p-value: Use your chosen significance threshold (commonly 0.05) to decide on rejecting the null hypothesis of no difference between groups.
- The visualization helps assess distribution differences and paired changes.

## Examples and reproducibility
Include a small example dataset (CSV or Excel) in `inst/examples/` or `data/` to demonstrate the function. A recommended reproducible example:
```r
# simulated paired example
set.seed(123)
dat_example <- data.frame(
  SubjectID = rep(1:20, each = 2),
  Group = rep(c("before", "after"), times = 20),
  Value = c(rnorm(20, 5, 1), rnorm(20, 5.5, 1))
)
# Call the function on dat_example as shown above
```

## Contributing
- Bug reports and feature requests: open an issue describing the problem or desired enhancement.
- Pull requests: fork the repository, create a feature branch, and submit a PR with a clear description and example use.
- Please add unit tests or reproducible examples for new features.

## License


## Contact / Author
Author: [Bojan Makivic] (you can add email or GitHub handle)
Repository: https://github.com/BojanMakivic/Wilcoxon-test-function-

