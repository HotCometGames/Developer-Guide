# scikit-learn

> The standard library for classical ML in Python — consistent API, broad algorithm coverage, production-ready.

> **Related:** [Data Preparation](data-preparation.md) | [Model Evaluation](model-evaluation.md) | [PyTorch](pytorch.md)

---

## What Is It?

scikit-learn provides a unified interface for dozens of ML algorithms, preprocessing tools, model selection utilities, and evaluation metrics. Every estimator follows the same `fit`/`predict` pattern.

## The Estimator API

```python
# Every model follows this pattern:
model = SomeEstimator(hyperparameters)
model.fit(X_train, y_train)      # learn from data
y_pred = model.predict(X_test)    # make predictions
```

## Common Models

```python
from sklearn.linear_model import LinearRegression, LogisticRegression
from sklearn.ensemble import RandomForestClassifier, GradientBoostingClassifier
from sklearn.svm import SVC
from sklearn.cluster import KMeans
from sklearn.decomposition import PCA

# Classification
model = RandomForestClassifier(n_estimators=200, max_depth=10)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)

# Regression
model = GradientBoostingRegressor(n_estimators=100, learning_rate=0.1)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
```

## Pipeline

Chains preprocessing and modeling into a single object:

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.ensemble import RandomForestClassifier

pipeline = Pipeline([
    ("scaler", StandardScaler()),
    ("classifier", RandomForestClassifier(n_estimators=100)),
])

pipeline.fit(X_train, y_train)
y_pred = pipeline.predict(X_test)  # automatically scales then predicts
```

### ColumnTransformer

Apply different preprocessing to different columns:

```python
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder

numeric_features = ["age", "income"]
categorical_features = ["education", "city"]

preprocessor = ColumnTransformer([
    ("num", StandardScaler(), numeric_features),
    ("cat", OneHotEncoder(), categorical_features),
])

pipeline = Pipeline([
    ("preprocessor", preprocessor),
    ("model", RandomForestClassifier()),
])
```

## Cross-Validation

```python
from sklearn.model_selection import cross_val_score, KFold

scores = cross_val_score(
    pipeline, X_train, y_train,
    cv=5,                      # 5-fold cross-validation
    scoring="f1_macro"         # evaluation metric
)
print(f"F1: {scores.mean():.3f} +/- {scores.std():.3f}")
```

| CV Method | When |
|-----------|------|
| K-Fold (default 5) | General purpose |
| Stratified K-Fold | Imbalanced classification |
| Group K-Fold | Related samples in groups |
| Time Series Split | Temporal data |
| Leave-One-Out | Very small datasets |

## Hyperparameter Tuning

```python
from sklearn.model_selection import GridSearchCV

param_grid = {
    "model__n_estimators": [100, 200, 300],
    "model__max_depth": [10, 20, None],
    "model__min_samples_split": [2, 5],
}

grid_search = GridSearchCV(
    pipeline, param_grid,
    cv=5, scoring="f1_macro",
    n_jobs=-1, verbose=1
)

grid_search.fit(X_train, y_train)
print(grid_search.best_params_)
print(grid_search.best_score_)
```

| Method | When | Cost |
|--------|------|------|
| GridSearchCV | Small parameter space | Full factorial |
| RandomizedSearchCV | Large parameter space | Samples randomly |
| BayesSearchCV (scikit-optimize) | Continuous params | Smart search |

## Feature Importance

```python
# Tree-based models provide built-in importance
importances = pipeline.named_steps["model"].feature_importances_
feature_names = numeric_features + list(
    pipeline.named_steps["preprocessor"]
        .named_transformers_["cat"]
        .get_feature_names_out(categorical_features)
)

for name, imp in sorted(zip(feature_names, importances), key=lambda x: -x[1])[:10]:
    print(f"{name}: {imp:.3f}")
```

## Model Persistence

```python
import joblib

# Save
joblib.dump(pipeline, "model.pkl")

# Load
loaded = joblib.load("model.pkl")
y_pred = loaded.predict(X_new)
```

## Best Practices

- **Always use a Pipeline** — prevents data leakage between train and test
- **Cross-validate, don't just train/test split** — more reliable performance estimate
- **Start simple** — linear model or shallow tree before complex ensembles
- **Check feature importance** — remove useless features, iterate
- **Use `n_jobs=-1`** for parallel training

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| No Pipeline | Data leakage, inconsistent preprocessing | Wrap everything in a Pipeline |
| Tuning on test data | Overly optimistic performance | Use validation set or CV, not test |
| Default hyperparameters | Suboptimal performance | Always tune at least a few key params |
| Ignoring class imbalance | Model predicts majority class | Set `class_weight='balanced'` |
| Too many features | Overfitting, slow training | Use feature selection or dimensionality reduction |

## What's Next?

Learn how to evaluate your models in [Model Evaluation](model-evaluation.md), or move to [PyTorch](pytorch.md) for deep learning.
