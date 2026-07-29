# Data Preparation

> Cleaning, transforming, and splitting data — the most important step in any ML project.

> **Related:** [What Is Machine Learning?](what-is-machine-learning.md) | [scikit-learn](scikit-learn.md) | [Model Evaluation](model-evaluation.md)

---

## What Is It?

Data preparation transforms raw data into a clean format suitable for machine learning models. It's often 60-80% of the work in an ML project.

## The Pipeline

```
Raw Data → Clean → Transform → Split → Train/Val/Test
```

## Loading Data

```python
import pandas as pd
import numpy as np

# Common formats
df = pd.read_csv("data.csv")
df = pd.read_parquet("data.parquet")
df = pd.read_json("data.json")
```

## Cleaning

```python
# Inspect
df.info()
df.describe()
df.isnull().sum()

# Handle missing values
df.dropna(subset=["critical_col"])      # drop rows missing critical fields
df["col"].fillna(df["col"].median())   # fill with median
df["col"].fillna("unknown")             # fill categorical with placeholder

# Remove duplicates
df = df.drop_duplicates()

# Handle outliers (example: cap at 99th percentile)
cap = df["price"].quantile(0.99)
df["price"] = df["price"].clip(upper=cap)
```

## Feature Engineering

```python
# Numeric transformations
df["log_feature"] = np.log1p(df["feature"])      # log transform for skewed data
df["binned_age"] = pd.cut(df["age"], bins=[0, 18, 65, 120])

# Date features
df["year"] = pd.to_datetime(df["date"]).dt.year
df["month"] = pd.to_datetime(df["date"]).dt.month
df["day_of_week"] = pd.to_datetime(df["date"]).dt.dayofweek

# Text features
df["text_length"] = df["text"].str.len()
df["word_count"] = df["text"].str.split().str.len()

# Interaction features
df["area"] = df["width"] * df["height"]
df["price_per_sqft"] = df["price"] / df["sqft"]
```

## Encoding Categorical Data

```python
# One-hot encoding
df_encoded = pd.get_dummies(df, columns=["color", "size"])

# Label encoding for ordinal categories
from sklearn.preprocessing import LabelEncoder
df["size_encoded"] = LabelEncoder().fit_transform(df["size"])
# small=0, medium=1, large=2
```

## Scaling

```python
from sklearn.preprocessing import StandardScaler, MinMaxScaler

# Standardization (mean=0, std=1) — preferred for many models
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Min-max scaling (range [0,1])
scaler = MinMaxScaler()
X_scaled = scaler.fit_transform(X)
```

## Train/Validation/Test Split

```python
from sklearn.model_selection import train_test_split

# Simple split
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
X_train, X_val, y_train, y_val = train_test_split(
    X_train, y_train, test_size=0.25, random_state=42
)
# Result: 60% train, 20% val, 20% test
```

| Set | Purpose | Size |
|-----|---------|------|
| Training | Fit the model | 60-80% |
| Validation | Tune hyperparameters, early stopping | 10-20% |
| Test | Final unbiased evaluation | 10-20% |

> **Warning:** Never use the test set for decisions during development. It must be used exactly once — at the end.

## Handling Imbalanced Data

```python
from imblearn.over_sampling import SMOTE

# Synthetic oversampling
smote = SMOTE(random_state=42)
X_resampled, y_resampled = smote.fit_resample(X_train, y_train)
```

| Method | How | When |
|--------|-----|------|
| Class weights | Penalize majority class heavier | Built into many models |
| Oversampling | Duplicate minority class | Simple, can overfit |
| SMOTE | Synthetic samples | Better than oversampling |
| Undersampling | Drop majority class | Only if you have plenty of data |

## Best Practices

- **Inspect data before cleaning** — plot distributions, check for impossible values
- **Fit scalers/encoders on training data only** — transform val/test with the same fitted transformer
- **No data leakage** — don't use future information or test-set statistics during training
- **Version your datasets** — data changes over time; tag which version was used for each model
- **Document decisions** — why was a feature dropped? Why was an outlier capped?

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Fitting scaler on full dataset | Test data influences training | Fit on train, transform all |
| Dropping too many rows | Losing signal | Impute instead of drop |
| Leaking future data | Model looks great, fails in production | Split by time, not randomly |
| Not handling class imbalance | Model predicts majority class always | Use class weights or resampling |
| Too many features | Overfitting, slow training | Start simple, add features iteratively |

## What's Next?

With clean data, move to [scikit-learn](scikit-learn.md) for building models or [PyTorch](pytorch.md) for deep learning.
