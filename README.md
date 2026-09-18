# econ3916-lab01-data-portfolio
# The Data Portfolio — Big Mac Index Analysis

## Objective

Construct purchasing-power-parity exchange rates and currency valuation estimates
from The Economist's Big Mac Index, and characterise the panel's structure and
missingness properties in order to establish what the resulting valuation
figures can and cannot support.

## Methodology

- **Data ingestion.** Sourced the Big Mac Index directly from The Economist's
  public repository, the authoritative source of record, rather than a
  redistributed copy — 57 countries across 45 publication periods spanning
  April 2000 to July 2026.
- **Schema and type validation.** Verified column dtypes on load, with explicit
  attention to date parsing and to the distinction between local-currency and
  USD-denominated price fields, as downstream arithmetic is silently incorrect
  if either is mistyped.
- **PPP construction.** Derived the implied purchasing-power-parity exchange
  rate for each country-period as the ratio of the local Big Mac price to the
  contemporaneous US price, then computed valuation as the percentage deviation
  of that implied rate from the prevailing market exchange rate. Positive values
  denote overvaluation against the dollar.
- **Structural classification.** Distinguished the three data structures present
  in the same source file — the cross-section (one period, many countries; 54
  observations in the July 2024 panel), the time series (one country, many
  periods), and the full unbalanced panel — and established which questions each
  structure is able to answer.
- **Missingness diagnosis.** Quantified per-country coverage against the maximum
  possible period count to identify incomplete panels. Classified Russia's exit
  from the series as **Missing Not At Random (MNAR)**: publication ceased in
  early 2022 for reasons directly connected to the macroeconomic shock that would
  have driven the missing observations, so the absence is informative and cannot
  be treated as ignorable or imputed without bias.
- **Visualisation.** Produced a ranked horizontal bar chart of cross-sectional
  valuations to display the distribution at a point in time, and a multi-country
  time-series comparison to separate persistent level differences from
  period-specific movement.

## Key Findings

- **Switzerland is persistently the most overvalued currency in the sample**, at
  **+41.8%** against the dollar in the July 2024 cross-section, and it holds the
  top position in every period examined. The persistence is the substantive
  result: a genuine mispricing would be expected to decay, whereas a structural
  price-level differential — driven by non-tradeable inputs such as Swiss wages,
  commercial rent, and protected agricultural prices — will not.
- **Japan is undervalued on average in every decade of the series**, indicating a
  durable gap between its domestic price level and its nominal exchange rate
  rather than a cyclical deviation.
- **Valuation is systematically ordered by income level.** The cross-section
  shows lower-income economies clustered on the undervalued side, consistent
  with the Balassa–Samuelson prediction that price levels rise with productivity
  and income. Raw deviations therefore conflate equilibrium price-level
  differences with genuine currency misvaluation, and should be conditioned on
  income before being read as a trading or policy signal.
- **The panel is unbalanced, which constrains cross-period comparison.** Country
  coverage varies over the sample as constituents enter and exit, so unconditioned
  panel-wide aggregates are weighted toward longer-covered countries, and an
  apparent trend may reflect changing sample composition rather than price
  movement. Comparisons across periods are made on a common country set.
