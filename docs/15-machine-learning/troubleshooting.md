# Machine Learning Troubleshooting

> Common ML failures and how to diagnose them.

---

## Training Issues

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| Loss is NaN | Learning rate too high, or division by zero | Lower LR, check for zeros in data, gradient clipping |
| Loss not decreasing | Wrong learning rate, bad initialization | Try cyclic LR, Xavier/Glorot init |
| Training loss is flat | Model isn't learning | Check data labels, try different architecture |
| Validation loss increases | Overfitting | Regularize, add dropout, reduce model size, more data |
| Training and val loss both high | Underfitting | Larger model, more epochs, fewer constraints |

## Data Issues

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| Model looks too good | Data leakage | Check for time-based leakage or feature leakage |
| Great on train, terrible on test | Train/test distribution mismatch | Ensure test set represents real-world data |
| All predictions are the same class | Class imbalance | Use class weights, resampling, or different metric |
| Model performs randomly | No signal in features | Revisit feature engineering, check correlation |
| Performance degrades over time | Data drift | Monitor input distributions, retrain periodically |

## Numerical Issues

| Problem | Fix |
|---------|-----|
| Division by zero | Add epsilon `1e-8` to denominators |
| Log of zero | `np.log1p()` instead of `np.log()` |
| Overflow in softmax | Use `log_softmax` + `NLLLoss` instead |
| Exploding gradients | Gradient clipping, lower learning rate |
| Vanishing gradients | ReLU activations, batch normalization, residual connections |

## Debugging Workflow

```
1. Start with a tiny subset (100 examples) — model should overfit
2. If it can't overfit 100 examples, something is fundamentally wrong
3. Gradually add more data and regularization
4. Plot train/val loss curves after every change
5. Compare against a simple baseline (mean prediction, linear model)
```

## Reproducibility

```python
import random
import numpy as np
import torch

def set_seed(seed=42):
    random.seed(seed)
    np.random.seed(seed)
    torch.manual_seed(seed)
    torch.cuda.manual_seed_all(seed)
    torch.backends.cudnn.deterministic = True
    torch.backends.cudnn.benchmark = False
```

## Common Pitfalls

| Pitfall | Why It Hurts | Prevention |
|---------|-------------|------------|
| Scaling all data together | Test data leaks into training | Fit scaler on train only |
| Tuning on test data | Overly optimistic final score | Test set: one evaluation, at the end |
| Not shuffling data | Order bias in training | Shuffle before train/val split |
| Wrong loss function | Model optimizes wrong thing | Match loss to problem (BCE vs MSE vs CE) |
| Too many epochs | Wasted compute, overfitting | Early stopping on validation loss |
| Pretrained model on wrong domain | Poor transfer, negative adaptation | Fine-tune more layers, check domain similarity |

## Best Practices to Prevent Issues

- **Baseline first** — simple model (mean prediction, linear regression) before complex
- **Start small** — 10% of data, 1 epoch, 1 layer — verify pipeline works
- **Log everything** — hyperparameters, metrics, data version, seed
- **Use a fixed validation set** — same examples every time for consistent comparison
- **Check predictions manually** — look at examples the model got wrong

---

> **Related:** [Data Preparation](data-preparation.md) — data quality | [Model Evaluation](model-evaluation.md) — diagnosing performance
