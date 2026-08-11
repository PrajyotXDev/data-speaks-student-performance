# DATA SPEAKS!! — Website-Ready ML Content

## Methodology

The modelling stage uses the cleaned and encoded Student Performance mathematics dataset. Final grade **G3** is treated as a numerical regression target, while **G1 and G2 are excluded** to prevent target leakage from previous-period grades. The data is divided into 80% training and 20% testing observations using a fixed random seed of 42. Three regression algorithms—Linear Regression, Random Forest Regressor, and Gradient Boosting Regressor—are trained on the same predictor set. Linear Regression uses standardization inside an sklearn pipeline, while the tree-based models are trained without scaling. Performance is evaluated on the unseen test set using Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), and R². The best model is selected using test RMSE, with MAE and R² also reported for transparent comparison. Feature importance from the strongest tree-based model is used to identify predictive patterns, and residual/actual-versus-predicted plots are used to assess model behaviour.

## Model Comparison

The three models were evaluated on the same held-out test set. Lower MAE and RMSE indicate smaller prediction errors, while higher R² indicates stronger predictive performance relative to a mean-only baseline.

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| Random Forest Regressor | 3.0810 | 3.8602 | 0.2733 |
| Gradient Boosting Regressor | 3.2513 | 4.0570 | 0.1973 |
| Linear Regression | 3.3953 | 4.1957 | 0.1415 |

**Best overall model:** Random Forest Regressor, selected using the lowest test RMSE of **3.8602**. It also achieved the lowest MAE (**3.0810**) and highest R² (**0.2733**).

## Key Findings

- **Random Forest Regressor** performed best overall, with MAE = **3.0810**, RMSE = **3.8602**, and R² = **0.2733**.
- The best tree-based model was **Random Forest Regressor**.
- The top predictive features from the Random Forest model were: **absences, failures, health, goout, age**.
- `failures` showed a negative Spearman association with G3 (-0.3612), suggesting that students with more recorded past failures tended to have lower final grades in this dataset.
- `Medu` and `Fedu` had positive Spearman associations with G3 (0.2250 and 0.1700), although their model importance was lower than absences and failures.
- `absences` had the highest tree-model importance (0.2069), but its Spearman association with G3 was weakly positive (0.0177); this illustrates why importance and simple correlation should not be treated as the same measure.

## Conclusion

The machine-learning stage shows that final mathematics grades can be predicted to a limited extent from non-grade student and school-related variables. The Random Forest model provided the strongest test-set performance among the three evaluated approaches. The feature analysis highlights variables such as absences and previous failures as important predictive signals, while association analysis provides additional direction for selected variables. However, the dataset is observational and relatively small, so the findings should be interpreted as predictive associations rather than causal effects. Further validation on larger and more diverse student populations would be needed before generalizing these patterns.