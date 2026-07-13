# Phase 2 Modeling Readout

## Objective

Estimate user-level heterogeneous treatment effects using baseline uplift learners.

## Approach

The modeling notebook trained two meta-learner baselines:

- S-learner: one conversion model trained with treatment assignment included as a feature.
- T-learner: separate conversion models for treated and control users, with uplift estimated as predicted treated conversion probability minus predicted control conversion probability.

The models were trained on a balanced treatment/control sample to make the first-pass workflow easier to debug and interpret.

## Key Findings

- Predicted uplift scores were highly concentrated near zero, which is expected for a rare conversion outcome and small absolute treatment effect.
- Both baseline learners produced some extreme individual uplift estimates, especially in the tails.
- The T-learner showed signs of instability because separate treated/control outcome models can extrapolate differently.
- Response-model diagnostics such as ROC AUC are useful sanity checks, but they do not directly measure uplift ranking quality.

## Interpretation

The first-pass S- and T-learners are useful baselines, but they should not be treated as final production models. The rare conversion rate makes individual probability estimation difficult, and the tree-based models can overfit small pockets of converters.

The main question is therefore not whether every individual uplift estimate is perfectly calibrated. The more important question for targeting is whether the uplift scores rank users better than random allocation.

## Next Step

Evaluate the uplift rankings using policy metrics such as cumulative gain, Qini curves, AUUC, and top-k treatment budget simulations.
