# Model Card

## Model Description

**Input:** 
The input to the model is a brand-user interaction matrix where each entry represents the weighted interaction scroe a user has had with a specific brand. In this case, the interaction matrix includes a normalized interaction score between 0 and 1.

**Output:** 
The output of the model is a predicted rating for a given user-brand pair. These predictions can be used to recommend to users brands that they are most likely to interact with.

**Model Architecture:** 
The model uses Singular Value Decomposition (SVD) as implemented in the scikit-surprise library. SVD is a matrix factorisation technique that decomposes the user-brand interaction matrix into three matrices, which are used to predict missing entries in the matrix.

## Performance

### Summary Metrics
Cross-validation evaluation of RMSE and MAE over 5 split(s).

| Metric          | Fold 1  | Fold 2  | Fold 3  | Fold 4  | Fold 5  | Mean    | Std    |
|-----------------|---------|---------|---------|---------|---------|---------|--------|
| RMSE  | 0.1859  | 0.1844  | 0.1857  | 0.1849  | 0.1857  | 0.1853  | 0.0006 |
| MAE   | 0.1474  | 0.1462  | 0.1468  | 0.1460  | 0.1469  | 0.1467  | 0.0005 |
| Fit time        | 6.99    | 6.86    | 7.17    | 6.94    | 6.80    | 6.95    | 0.13   |
| Test time       | 0.06    | 0.18    | 0.06    | 0.06    | 0.06    | 0.09    | 0.05   |

- **RMSE (Test set)**: 0.1578
- **MAE (Test set)**: 0.1229  

Performance is evaluated using 5-fold cross-validation on the user-brand interaction dataset. The metrics used for evaluation are Root Mean Squared Error (RMSE) and Mean Absolute Error (MAE).

## Limitations

- The model assumes that the interaction data is static and does not account for changes over time, such as users' evolving preferences.
- It performs well on dense matrices but may not be as effective on highly sparse datasets where the number of interactions per user/item is very low.
- The model does not handle cold-start problems effectively (i.e., recommending items to new users or recommending new items to existing users).

## Trade-offs

- **Overfitting vs. Generalization**: The low error values suggest good performance, but there is a risk of overfitting to the training data. Cross-validation helps mitigate this, but the model's real-world performance should be monitored.
- **Complexity vs. Interpretability**: SVD provides good accuracy but is more complex and less interpretable than simpler models like user or item average predictors.