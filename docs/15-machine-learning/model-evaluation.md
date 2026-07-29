# Model Evaluation

> Measuring how well your model performs — and knowing when it's good enough.

> **Related:** [scikit-learn](scikit-learn.md) | [What Is Machine Learning?](what-is-machine-learning.md) | [Data Preparation](data-preparation.md)

---

## What Is It?

Model evaluation measures how well a trained model generalizes to unseen data. The right metric depends on your problem type and business goal.

## Classification Metrics

### Confusion Matrix

```
              Actual Positive    Actual Negative
Predicted Pos      TP                 FP
Predicted Neg      FN                 TN
```

```python
from sklearn.metrics import confusion_matrix, ConfusionMatrixDisplay

cm = confusion_matrix(y_test, y_pred)
ConfusionMatrixDisplay(cm).plot()
```

### Key Metrics

| Metric | Formula | What It Measures | When to Use |
|--------|---------|-----------------|-------------|
| Accuracy | `(TP+TN)/(TP+TN+FP+FN)` | Overall correctness | Balanced classes |
| Precision | `TP/(TP+FP)` | How many predicted positives are correct | Minimize false positives (spam) |
| Recall | `TP/(TP+FN)` | How many actual positives were found | Minimize false negatives (disease) |
| F1 Score | `2*(P*R)/(P+R)` | Harmonic mean of precision and recall | Imbalanced classes |
| Specificity | `TN/(TN+FP)` | How many negatives were correctly identified | Balanced view |

```python
from sklearn.metrics import classification_report

print(classification_report(y_test, y_pred))
```

```
              precision    recall  f1-score   support
           0       0.94      0.97      0.95       100
           1       0.88      0.79      0.83        50
    accuracy                           0.92       150
```

### ROC & AUC

ROC curve plots True Positive Rate vs False Positive Rate at various thresholds. AUC is the area under that curve — 1.0 is perfect, 0.5 is random.

```python
from sklearn.metrics import roc_curve, roc_auc_score
import matplotlib.pyplot as plt

y_prob = model.predict_proba(X_test)[:, 1]
fpr, tpr, thresholds = roc_curve(y_test, y_prob)
auc = roc_auc_score(y_test, y_prob)

plt.plot(fpr, tpr, label=f"AUC={auc:.3f}")
plt.plot([0, 1], [0, 1], "k--")
plt.xlabel("False Positive Rate")
plt.ylabel("True Positive Rate")
plt.legend()
```

## Regression Metrics

| Metric | Formula | Scale | When to Use |
|--------|---------|-------|-------------|
| MSE | `mean((y - y_pred)²)` | Same as y², squared | Penalize large errors heavily |
| RMSE | `sqrt(MSE)` | Same as y | Interpretable (same units as target) |
| MAE | `mean(|y - y_pred|)` | Same as y | Robust to outliers |
| R² | `1 - MSE/var(y)` | [0, 1] | Proportion of variance explained |

```python
from sklearn.metrics import mean_squared_error, mean_absolute_error, r2_score

mse = mean_squared_error(y_test, y_pred)
rmse = mean_squared_error(y_test, y_pred, squared=False)
mae = mean_absolute_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)
```

## Bias-Variance Tradeoff

```
       Underfitting          Balanced          Overfitting
        (High bias)                         (High variance)
Train:    Poor    ──→       Good       ──→      Great
Val:      Poor    ──→       Good       ──→      Poor
```

| Symptom | Likely Issue | Fix |
|---------|-------------|-----|
| Both train and val loss high | Underfitting (high bias) | More complex model, more features, fewer constraints |
| Train loss low, val loss high | Overfitting (high variance) | More data, regularization, simpler model |
| Train and val loss similar, both acceptable | Good fit | Ship it |

## Cross-Validation

```python
from sklearn.model_selection import cross_validate

scores = cross_validate(
    model, X_train, y_train,
    cv=5,
    scoring=["accuracy", "f1_macro", "roc_auc"],
    return_train_score=True
)

for metric in ["test_accuracy", "test_f1_macro", "test_roc_auc"]:
    print(f"{metric}: {scores[metric].mean():.3f} +/- {scores[metric].std():.3f}")
```

## Learning Curves

Plot train and validation scores against training set size:

```
Score
  ^
  |   Train ─────
  |         ╲
  |   Val   ╲────
  |               ╲
  +──────────────────→ Training examples

If curves haven't converged → more data will help.
If curves are close but low → model is too simple.
If curves are far apart → overfitting (regularize or simplify).
```

## Best Practices

- **Pick one primary metric** — optimize for it, track others for context
- **Don't tune on test data** — use validation or cross-validation
- **Compare against a baseline** — dumb heuristic beats complex model? Reconsider.
- **Check for data leakage** — if val performance is suspiciously high, suspect leakage
- **Monitor after deployment** — model performance drifts as data changes

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Only looking at accuracy | Misleading with imbalanced classes | Use F1, precision, recall, or AUC |
| Tuning until test score is great | Overfitting to test set | Set test data aside, touch it once |
| Ignoring confidence intervals | Single CV fold is noisy | Report mean + std across folds |
| Comparing models on different splits | Unfair comparison | Use same CV folds for all models |
| No business context for metrics | 99% accuracy on rare event is useless | Choose metric that matches the cost of errors |

## What's Next?

If your model performs well, learn how to prepare better data in [Data Preparation](data-preparation.md). If performance is poor, check [Troubleshooting](troubleshooting.md).
