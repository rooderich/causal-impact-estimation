# Promotion Incrementality & Uplift Targeting

End-to-end causal uplift project using a randomized advertising experiment to estimate promotion incrementality and evaluate budget-constrained targeting policies.

## Project Summary

This project analyzes the Criteo Uplift Prediction dataset, a large-scale randomized advertising experiment with 13.9M users. The goal is to move from average treatment effect analysis to user-level uplift targeting:

```text
uplift(x) = P(conversion | treatment = 1, X = x) - P(conversion | treatment = 0, X = x)
```

In product terms, the project asks:

> If we can only target a subset of users, can an uplift model identify users who are more likely to convert because of treatment?

## Key Results

- Validated randomized experiment quality using treatment/control balance checks and standardized mean differences.
- Estimated an average treatment effect of approximately 0.12 percentage points, equivalent to about 59% relative lift over control.
- Trained baseline S- and T-learner uplift models to estimate heterogeneous treatment effects.
- Evaluated targeting policies using cumulative gain curves, Qini curves, AUUC, and top-k budget simulations.
- Identified a 10% treatment-budget policy that captured approximately 779% more estimated incremental conversions than random targeting on the sampled offline test set.

## Methods

Experiment validation:

- Treatment/control conversion comparison
- Average treatment effect estimation
- Difference-in-proportions confidence interval
- Missing value checks
- Covariate balance diagnostics using standardized mean differences

Uplift modeling:

- S-learner baseline
- T-learner baseline
- Predicted treated/control conversion probabilities
- User-level uplift scores

Policy evaluation:

- Cumulative incremental gain curves
- Qini curves
- AUUC
- Qini AUC versus random targeting
- Top-k treatment budget simulation

## Repository Structure

```text
causal-impact-estimation/
|-- data/
|   |-- raw/                 # raw Criteo dataset, not committed
|   `-- processed/           # generated scored samples, not committed
|-- notebooks/
|   |-- 01_experiment_eda.ipynb
|   |-- 02_uplift_modeling.ipynb
|   `-- 03_policy_evaluation.ipynb
|-- reports/
|   |-- phase_1_experiment_readout.md
|   |-- phase_2_modeling_readout.md
|   |-- phase_3_policy_readout.md
|   `-- final_project_summary.md
|-- requirements.txt
`-- README.md
```

## How To Run

Create and activate a virtual environment:

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m ipykernel install --user --name causal-uplift --display-name "Python (causal-uplift)"
```

Place the raw dataset here:

```text
data/raw/criteo-uplift-v2.1.csv
```

Run notebooks in order:

```text
01_experiment_eda.ipynb
02_uplift_modeling.ipynb
03_policy_evaluation.ipynb
```

Notebook 2 saves the scored test set used by Notebook 3:

```text
data/processed/uplift_scores_sample.parquet
```

## Important Caveats

The current results are based on sampled offline evaluation, not a deployed policy experiment. The S- and T-learner baselines also produced some unstable individual uplift predictions because conversion is rare. For production use, the next step would be stronger regularization, larger training samples, LightGBM/X-learner comparisons, calibration checks, and a follow-up randomized policy test.
