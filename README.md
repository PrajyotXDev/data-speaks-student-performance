# DATA SPEAKS!! — Student Performance Analysis

Machine-learning completion for the Mathematics for Data Science group project using the UCI Student Performance mathematics dataset.

## Project pipeline

`Dataset → Preprocessing → EDA → Machine Learning → Evaluation → Interpretation → Website`

The existing preprocessing/EDA notebook is preserved as `01_eda_preprocessing.ipynb`. The ML stage is implemented in `02_regression_model.ipynb`.

## ML setup

- Target: `G3` (final mathematics grade, 0–20)
- Excluded predictors: `G1`, `G2` to avoid target leakage
- Split: 80% train / 20% test
- Random state: 42
- Models:
  - Linear Regression
  - Random Forest Regressor
  - Gradient Boosting Regressor
- Metrics: MAE, RMSE, R²

## Actual test-set results

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| Random Forest Regressor | 3.08098 | 3.86023 | 0.27328 |
| Gradient Boosting Regressor | 3.25133 | 4.05697 | 0.19732 |
| Linear Regression | 3.39526 | 4.19568 | 0.14149 |

The Random Forest Regressor is the overall model selected by the lowest test RMSE. It also has the lowest MAE and highest R² among the three models.

## Top predictive features

According to the best tree-based model (Random Forest), the strongest predictive features are:

1. `absences`
2. `failures`
3. `health`
4. `goout`
5. `age`
6. `studytime`
7. `Fedu`
8. `Medu`
9. `Walc`
10. `freetime`

These are predictive associations, not causal effects.

## Outputs

- `outputs/figures/model_comparison.png`
- `outputs/figures/actual_vs_predicted.png`
- `outputs/figures/residual_analysis.png`
- `outputs/figures/feature_importance.png`
- `outputs/results/model_comparison.csv`
- `outputs/results/feature_importance.csv`
- `outputs/results/top_feature_associations.csv`
- `outputs/results/best_model_predictions.csv`
- `outputs/results/ml_summary.csv`
- `website_ready_content.md`

## Running the ML notebook

From this project directory:

```bash
pip install -r requirements.txt
jupyter notebook 02_regression_model.ipynb
```

The notebook was executed from top to bottom successfully with the included cleaned dataset.

## Statistical caution

This is an observational educational dataset. Model feature importance and correlations describe predictive/associational patterns and do not establish causation.
