# Phase 3 Policy Readout

## Objective

Evaluate whether uplift scores improve budget-constrained targeting compared with random targeting.

## Method

Users were ranked by predicted uplift score. For each targeting budget, cumulative incremental conversions were estimated as:

```text
treated conversions - control conversions * (treated users / control users)
```

The uplift policies were evaluated using:

- Cumulative incremental gain curves
- Qini curves
- AUUC
- Qini AUC versus random targeting
- Top-k treatment budget simulations

## Key Finding

At a 10% treatment budget, the best offline uplift policy captured an estimated 62.4 incremental conversions versus 7.1 under random targeting.

This corresponds to approximately 779% more estimated incremental conversions than random targeting at the same budget.

## Interpretation

The cumulative gain and Qini curves showed clear improvement at low treatment budgets, suggesting that the uplift ranking can concentrate incremental conversions among top-ranked users.

This is the core product decision insight: when treatment budget is constrained, targeting by uplift can outperform random allocation by prioritizing users with higher estimated incremental response.

## Recommendation

Treat the current uplift scores as an offline policy candidate, not a production-ready rule. Before deployment, validate the targeting policy with a follow-up randomized policy test against random allocation or the current production targeting rule.

## Caveat

These results are based on a sampled offline test set. The final project should rerun the strongest learner on a larger sample or the full dataset before reporting final production-level estimates.
