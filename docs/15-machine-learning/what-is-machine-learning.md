# What Is Machine Learning?

> Building systems that improve with experience — finding patterns in data without being explicitly programmed for every case.

> **Related:** [Data Preparation](data-preparation.md) | [scikit-learn](scikit-learn.md) | [Model Evaluation](model-evaluation.md)

---

## What Is It?

Machine learning is a subset of AI where algorithms learn patterns from data instead of following hard-coded rules. The model's performance improves as it sees more examples.

## ML vs Traditional Programming

```
Traditional:  Data + Rules → Answers
ML:           Data + Answers → Rules (the model)
```

| Aspect | Traditional | ML |
|--------|-------------|----|
| Input | Code + data | Data + labels (or just data) |
| Output | Deterministic result | A model that can make predictions |
| Maintenance | Update code for new cases | Retrain with new data |
| Best for | Well-understood rules | Pattern recognition, complex relationships |

## ML Lifecycle

```
1. Define Problem    →  What are we predicting? How will we measure success?
2. Collect Data      →  Enough? Representative? Labeled?
3. Prepare Data      →  Clean, transform, feature engineer, split
4. Choose Model      →  Based on problem type, data size, interpretability needs
5. Train             →  Fit model to training data
6. Evaluate          →  Validate on held-out data, tune hyperparameters
7. Deploy            →  Serve predictions in production
8. Monitor           →  Track performance drift, retrain as needed
```

## Types of ML

### Supervised Learning

The model learns from labeled examples:

```
Input:  (image, "cat"), (image, "dog"), (image, "cat")...
Output: A model that classifies new images as cat or dog
```

| Type | Goal | Example Algorithms |
|------|------|-------------------|
| Classification | Predict a category | Random Forest, SVM, Neural Networks |
| Regression | Predict a number | Linear Regression, Gradient Boosting |

### Unsupervised Learning

The model finds structure in unlabeled data:

```
Input:  Customer purchase histories (no labels)
Output: Segments of similar customers
```

| Type | Goal | Example Algorithms |
|------|------|-------------------|
| Clustering | Group similar items | K-Means, DBSCAN |
| Dimensionality Reduction | Simplify data | PCA, t-SNE |
| Anomaly Detection | Find unusual patterns | Isolation Forest |

### Reinforcement Learning

An agent learns by interacting with an environment, receiving rewards or penalties:

```
Agent → Action → Environment → New State + Reward → Agent updates policy
```

Used for games, robotics, recommendation systems.

## Terminology

| Term | Meaning |
|------|---------|
| Features (X) | Input variables the model uses to predict |
| Labels (y) | The target variable being predicted |
| Training set | Data used to fit the model |
| Validation set | Data used to tune hyperparameters |
| Test set | Held-out data for final evaluation |
| Overfitting | Model memorizes training data, fails on new data |
| Underfitting | Model is too simple to capture the pattern |
| Hyperparameters | Settings set before training (learning rate, tree depth) |
| Parameters | Values learned during training (weights, biases) |

## When to Use ML

| Good Fit | Bad Fit |
|----------|---------|
| Complex patterns you can't codify by hand | Simple rules are faster, cheaper, more reliable |
| Lots of data available | Little data, or data is expensive to collect |
| The pattern changes over time | The problem is deterministic |
| A wrong answer is tolerable | Errors are catastrophic |

## What's Next?

Start with [Data Preparation](data-preparation.md) — the most important step in any ML project.
