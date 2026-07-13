# Final Project Summary

## Business Problem

Promotion and advertising teams often face limited treatment budgets. A standard response model asks who is likely to convert, but this can waste spend on users who would have converted anyway.

This project instead uses uplift modeling to estimate who is likely to convert because of treatment.

## Workflow

1. Validated the randomized experiment design.
2. Estimated baseline average treatment effect.
3. Trained S- and T-learner uplift models.
4. Evaluated offline targeting policies using Qini, AUUC, cumulative gain, and top-k budget simulations.
5. Translated uplift rankings into a budget-constrained targeting recommendation.

## Results

- Dataset: 13,979,592 users from a randomized advertising experiment.
- Average treatment effect: approximately 0.12 percentage points.
- Relative lift: approximately 59% over control.
- Balance diagnostics: no observed feature exceeded the 0.1 standardized mean difference threshold.
- Best offline policy: top 10% uplift targeting.
- Policy impact: approximately 779% more estimated incremental conversions than random targeting on the sampled test set.

## Decision Science Takeaway

The project shows how to move from experiment analysis to an actionable treatment policy. The strongest insight is not simply that treatment works on average, but that treatment effects can be ranked and used to allocate limited targeting budget more efficiently.

## Limitations

- Current models are first-pass S-/T-learner baselines.
- Conversion is rare, which makes individual uplift estimation noisy.
- Some individual uplift predictions were unstable.
- Results are based on offline sampled evaluation.
- A live randomized policy test is needed before deployment.

## Next Improvements

- Add regularized logistic uplift baselines.
- Train LightGBM-based S-/T-learners.
- Add X-learner for treatment/control imbalance.
- Compare models using a larger held-out sample.
- Add segment-level recommendations and negative-uplift suppression rules.
