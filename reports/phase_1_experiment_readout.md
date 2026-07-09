# Phase 1 Experiment Readout

## Objective

Validate whether the randomized advertising experiment is suitable for incrementality and uplift modeling.

## Key Findings

- The experiment contains 13,979,592 users, with 11,882,655 assigned to treatment.
- Treatment conversion rate was approximately 0.31% versus a control conversion rate of approximately 0.19%.
- The average treatment effect was approximately 0.12 percentage points, equivalent to a 59.45% relative lift.
- Covariate balance looked good, with a maximum absolute SMD of 0.0488.
- The experiment appears suitable for heterogeneous treatment effect and uplift modeling.

## Interpretation

The treatment group converted at a higher rate than the control group, suggesting that the advertising treatment generated incremental conversions. Although the absolute lift is small, the effect is meaningful at scale because the experiment contains nearly 14 million users.

Covariate balance diagnostics show no observed feature exceeded the 0.1 standardized mean difference threshold. This supports the validity of the randomized setup and makes the dataset appropriate for uplift modeling.

## Next Step

Build uplift models to estimate which users are persuadable, neutral, or negatively affected by treatment.