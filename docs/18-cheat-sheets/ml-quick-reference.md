# Machine Learning Quick Reference

> One-page reference for scikit-learn, PyTorch, TensorFlow, and ML workflows. Print this or bookmark it.

---

## ML Workflow

```
1. Define problem
2. Collect data
3. Clean & preprocess
4. Split data (train/val/test)
5. Choose model
6. Train
7. Evaluate
8. Tune hyperparameters
9. Deploy
10. Monitor
```

## Data Preparation (Python)

### Pandas

| Task | Code |
|------|------|
| Load CSV | `pd.read_csv("file.csv")` |
| Load Excel | `pd.read_excel("file.xlsx")` |
| Head | `df.head(5)` |
| Info | `df.info()` |
| Describe | `df.describe()` |
| Drop rows | `df.dropna()` |
| Fill NaN | `df.fillna(0)` |
| Select column | `df["col"]` |
| Filter | `df[df["col"] > 5]` |
| Group by | `df.groupby("col").mean()` |
| One-hot encode | `pd.get_dummies(df)` |

### NumPy

| Task | Code |
|------|------|
| Array | `np.array([1, 2, 3])` |
| Zeros | `np.zeros((3, 4))` |
| Ones | `np.ones((3, 4))` |
| Random | `np.random.randn(3, 4)` |
| Reshape | `arr.reshape(3, 4)` |
| Transpose | `arr.T` |
| Dot product | `np.dot(a, b)` |
| Mean | `np.mean(arr, axis=0)` |
| Standardize | `(arr - mean) / std` |

### Train/Test Split

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
```

## scikit-learn

### Classification

```python
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score, classification_report

model = RandomForestClassifier(n_estimators=100)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)

print(accuracy_score(y_test, y_pred))
print(classification_report(y_test, y_pred))
```

### Regression

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

model = LinearRegression()
model.fit(X_train, y_train)
y_pred = model.predict(X_test)

print(mean_squared_error(y_test, y_pred))
print(r2_score(y_test, y_pred))
```

### Common Models

| Model | Type | When to Use |
|-------|------|-------------|
| LinearRegression | Regression | Simple linear relationships |
| LogisticRegression | Classification | Binary classification |
| RandomForest | Both | Good default, tabular data |
| GradientBoosting | Both | Best performance on tabular |
| SVM | Classification | Small-medium datasets |
| KNN | Both | Simple, small datasets |
| KMeans | Clustering | Unsupervised grouping |
| PCA | Dimensionality reduction | Feature reduction |

### Preprocessing

```python
from sklearn.preprocessing import StandardScaler, LabelEncoder

# Scale features
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# Encode labels
le = LabelEncoder()
y_encoded = le.fit_transform(y)
```

### Evaluation Metrics

| Metric | Use Case | Code |
|--------|----------|------|
| Accuracy | Balanced classification | `accuracy_score(y_true, y_pred)` |
| Precision | Minimize false positives | `precision_score(y_true, y_pred)` |
| Recall | Minimize false negatives | `recall_score(y_true, y_pred)` |
| F1 | Balance precision/recall | `f1_score(y_true, y_pred)` |
| AUC-ROC | Binary classification | `roc_auc_score(y_true, y_prob)` |
| MSE | Regression | `mean_squared_error(y_true, y_pred)` |
| MAE | Regression (robust) | `mean_absolute_error(y_true, y_pred)` |
| R² | Regression goodness of fit | `r2_score(y_true, y_pred)` |

## PyTorch

### Basics

```python
import torch
import torch.nn as nn
import torch.optim as optim

# Tensor
x = torch.randn(3, 4)
x = torch.tensor([1.0, 2.0, 3.0])
x = x.to('cuda')  # GPU

# Check GPU
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
```

### Simple Neural Network

```python
class Net(nn.Module):
    def __init__(self):
        super().__init__()
        self.fc1 = nn.Linear(784, 128)
        self.fc2 = nn.Linear(128, 10)

    def forward(self, x):
        x = torch.relu(self.fc1(x))
        x = self.fc2(x)
        return x

model = Net().to(device)
criterion = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters(), lr=0.001)
```

### Training Loop

```python
for epoch in range(num_epochs):
    model.train()
    for batch_X, batch_y in train_loader:
        batch_X, batch_y = batch_X.to(device), batch_y.to(device)

        optimizer.zero_grad()
        output = model(batch_X)
        loss = criterion(output, batch_y)
        loss.backward()
        optimizer.step()

    model.eval()
    with torch.no_grad():
        val_loss = criterion(model(val_X), val_y)
```

### DataLoader

```python
from torch.utils.data import DataLoader, TensorDataset

dataset = TensorDataset(X_tensor, y_tensor)
loader = DataLoader(dataset, batch_size=32, shuffle=True)
```

## TensorFlow / Keras

```python
import tensorflow as tf

# Simple model
model = tf.keras.Sequential([
    tf.keras.layers.Dense(128, activation='relu'),
    tf.keras.layers.Dropout(0.2),
    tf.keras.layers.Dense(10, activation='softmax')
])

model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)

model.fit(X_train, y_train, epochs=10, validation_split=0.2)
```

## Hyperparameter Tuning

| Method | How | When |
|--------|-----|------|
| Grid search | Try all combinations | Small search space |
| Random search | Random combinations | Medium search space |
| Bayesian | Smart sampling | Large search space |
| Manual | Expert intuition | Quick iteration |

```python
from sklearn.model_selection import GridSearchCV

params = {'n_estimators': [50, 100, 200], 'max_depth': [5, 10, 20]}
grid = GridSearchCV(model, params, cv=5)
grid.fit(X_train, y_train)
print(grid.best_params_)
```

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Data leakage | Looks too good, fails in prod | Split data before feature engineering |
| No validation set | Can't detect overfitting | Always hold out test set |
| Not scaling features | Model biased toward large features | Standardize/normalize |
| Ignoring class imbalance | Model predicts majority class | Use SMOTE, class weights, or resampling |
| Overfitting | Great train, poor test | Regularization, more data, simpler model |
| Not enough data | Model can't generalize | Augment, collect more, or use transfer learning |

---

> **Full section:** [Machine Learning](../15-machine-learning/README.md) | **Next:** [Hackathons](hackathons-quick-reference.md)
