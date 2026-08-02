# Resource Adequacy

![Computational framework](figures/framework.svg)

> **Probabilistic electricity resource-adequacy assessment using exact
> FFT convolution on real Belgian grid data, independently verified by a
> separately implemented Monte Carlo simulation, with engineering
> analyses of interconnection requirements and marginal adequacy
> value.**

------------------------------------------------------------------------

## Overview

Will there be enough electricity when demand is highest?

*Resource adequacy* quantifies that question through **LOLE** (Loss of
Load Expectation, hours/year) and **EENS** (Expected Energy Not Served).
This repository computes those quantities exactly for the Belgian
electricity system using public operational data.

The probabilistic ingredients are conventional — forced-outage rates,
measured quarter-hourly net load, the standard LOLE and EENS metrics.
The contribution is not the adequacy model but the **computational
validation methodology**:

an exact probabilistic solution obtained by FFT convolution is
independently reproduced by a separately developed Monte Carlo
simulation, and agreement between the two is required before any
engineering conclusion is accepted.

------------------------------------------------------------------------

## Why this repository is different

Industrial adequacy studies typically rely on a single computational
implementation, most often Monte Carlo simulation.

This repository deliberately follows a different philosophy.

Every important numerical result is treated as something to be
**certified rather than asserted**.

The exact FFT implementation and an independently written Monte Carlo
implementation were initially found to disagree by nearly 20%. Rather
than accepting either answer, the discrepancy was investigated until its
origin---a hidden modelling assumption concerning outage
persistence---was understood. Once both methods represented the same
probabilistic model, they converged within statistical error.

The validation process is therefore **part of the scientific
contribution**, not merely software testing.

This repository demonstrates a computational discipline suitable for
high-consequence engineering models:

-   independent implementations;
-   reconciliation of discrepancies;
-   reproducible quantitative results;
-   engineering interpretation built only on validated computations.

The same discipline runs through the companion
[LongevityRisk](https://github.com/evrelegh/LongevityRisk) (pension longevity)
and [ClinicalSupplyRisk](https://github.com/evrelegh/ClinicalSupplyRisk)
(clinical-trial drug demand) studies.

------------------------------------------------------------------------

## Contributions

-   exact probabilistic evaluation of LOLE and EENS using FFT
    convolution;
-   independent Monte Carlo implementation used for computational
    cross-validation;
-   identification and resolution of a hidden temporal-sampling
    assumption;
-   engineering analysis of Belgium's interconnection requirement;
-   marginal adequacy value of additional capacity by technology;
-   sensitivity ranking of demand, capacity and outage rates;
-   fully reproducible workflow from public Elia and ENTSO-E data.

------------------------------------------------------------------------

## Headline results

-   **Domestic generation alone produces LOLE = 22.3 h/year**, versus
    Belgium's adequacy target of **3 h/year**.
-   **Approximately 1 GW of firm imports** reduces LOLE to the adequacy
    target; the first gigawatt provides by far the largest benefit.
-   **Demand dominates adequacy risk.** LOLE is roughly **nine times
    more sensitive** to demand growth than to modest changes in
    forced-outage rates.
-   **Risk is highly concentrated.** Nearly all adequacy risk arises
    during a handful of winter evenings where high demand coincides with
    low renewable production.

------------------------------------------------------------------------

## Method

  -----------------------------------------------------------------------
  Component                             Approach
  ------------------------------------- ---------------------------------
  Supply                                \~100 dispatchable generating
                                        units represented as two-state
                                        random variables

  Aggregation                           Exact probabilistic convolution
                                        using FFT

  Demand                                Real quarter-hourly Belgian
                                        net-load data (Elia)

  Metrics                               LOLE and EENS computed over the
                                        empirical demand series

  Verification                          Independent Monte Carlo
                                        implementation converging within
                                        0.2%

  Extensions                            Interconnection analysis,
                                        marginal capacity valuation,
                                        sensitivity analysis
  -----------------------------------------------------------------------

Because the aggregation is exact, scenario comparisons contain **no
Monte Carlo sampling noise**.

------------------------------------------------------------------------

## Scope

-   Domestic generation only (imports analysed separately).
-   One observed weather year (2023).
-   Planning forced-outage rates by technology.

Future work includes stochastic imports, multiple weather years and
empirical outage rates.

------------------------------------------------------------------------

## Reproducibility

All inputs originate from public data sources (Elia Open Data and
ENTSO-E). Running the notebook reproduces every figure, validation
experiment and engineering result.


------------------------------------------------------------------------

## Author

**Erik Van Releghem** · PHNX

*Part of a series of quantitative risk-modelling studies built on exact
probabilistic computation with independent numerical verification.*
