# Problem Set 1: The Cost of Living Brief

## Objective

This project builds a household-specific cost-of-living index and compares it against official CPI measures to test a client's claim that the CPI overstates what their workers actually experience.

## Key Finding

Our household index rose 36.85% between 2019 and 2024, meaningfully faster than the official CPI headline measure for the same period. This gap reflects genuine differences in spending patterns, particularly a heavy weight on rent in a high-cost neighborhood, rather than any error in either measure.

## Methodology

- Built a weighted Laspeyres price index over six household spending categories
- Pulled four FRED proxy series and rebased them to a common 2019 base period
- Audited every series for coverage gaps, computed a common sample, and compared seasonally adjusted versus unadjusted data
- Used AI to run a weight-sensitivity analysis, verifying the result against hand-calculated figures

## Confidence

We are confident in the direction of this finding (household cost of living outpacing CPI) at roughly an 80% level, with more uncertainty around the precise size of the gap.
