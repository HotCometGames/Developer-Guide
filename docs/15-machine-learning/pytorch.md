# PyTorch

> Flexible deep learning framework with dynamic computation graphs and first-class GPU support.

> **Related:** [Neural Networks & Deep Learning](neural-networks-and-deep-learning.md) | [scikit-learn](scikit-learn.md) | [Model Evaluation](model-evaluation.md)

---

## What Is It?

PyTorch is a Python-first deep learning framework built around tensors and automatic differentiation. It uses define-by-run execution — the computation graph is built on the fly as code runs.

## Tensors

```python
import torch

# Creation
x = torch.tensor([1.0, 2.0, 3.0])
x = torch.randn(3, 4)          # random normal
x = torch.zeros(3, 4)          # zeros
x = torch.ones(3, 4)           # ones

# Operations
x + y, x * y, torch.matmul(x, y.T)
x.mean(), x.std(), x.sum()
x.reshape(2, 6), x.T, x.squeeze(), x.unsqueeze(0)

# GPU
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
x = x.to(device)
```

## Autograd — Automatic Differentiation

```python
x = torch.randn(3, requires_grad=True)
y = x.pow(2).sum()
y.backward()           # compute gradients
print(x.grad)          # dy/dx
```

## Building a Model

```python
import torch.nn as nn
import torch.nn.functional as F

class Classifier(nn.Module):
    def __init__(self, input_size, hidden_size, num_classes):
        super().__init__()
        self.fc1 = nn.Linear(input_size, hidden_size)
        self.fc2 = nn.Linear(hidden_size, hidden_size)
        self.fc3 = nn.Linear(hidden_size, num_classes)
        self.dropout = nn.Dropout(0.2)

    def forward(self, x):
        x = F.relu(self.fc1(x))
        x = self.dropout(F.relu(self.fc2(x)))
        x = self.fc3(x)
        return x

model = Classifier(input_size=784, hidden_size=128, num_classes=10).to(device)
```

## Training Loop

```python
criterion = nn.CrossEntropyLoss()
optimizer = torch.optim.Adam(model.parameters(), lr=0.001)

num_epochs = 10

for epoch in range(num_epochs):
    # Training
    model.train()
    running_loss = 0.0
    for batch_X, batch_y in train_loader:
        batch_X, batch_y = batch_X.to(device), batch_y.to(device)

        optimizer.zero_grad()
        outputs = model(batch_X)
        loss = criterion(outputs, batch_y)
        loss.backward()
        optimizer.step()

        running_loss += loss.item()

    # Validation
    model.eval()
    val_loss = 0.0
    correct = 0
    total = 0
    with torch.no_grad():
        for batch_X, batch_y in val_loader:
            batch_X, batch_y = batch_X.to(device), batch_y.to(device)
            outputs = model(batch_X)
            loss = criterion(outputs, batch_y)
            val_loss += loss.item()
            _, predicted = torch.max(outputs, 1)
            total += batch_y.size(0)
            correct += (predicted == batch_y).sum().item()

    print(f"Epoch {epoch+1}: train_loss={running_loss:.4f}, "
          f"val_loss={val_loss:.4f}, val_acc={correct/total:.4f}")
```

## Data Loading

```python
from torch.utils.data import Dataset, DataLoader, TensorDataset

# From tensors
dataset = TensorDataset(X_tensor, y_tensor)
loader = DataLoader(dataset, batch_size=32, shuffle=True)

# Custom dataset
class MyDataset(Dataset):
    def __init__(self, csv_file):
        self.data = pd.read_csv(csv_file)

    def __len__(self):
        return len(self.data)

    def __getitem__(self, idx):
        row = self.data.iloc[idx]
        x = torch.tensor(row.drop("label").values, dtype=torch.float32)
        y = torch.tensor(row["label"], dtype=torch.long)
        return x, y
```

## Saving and Loading

```python
# Save
torch.save({
    "model_state_dict": model.state_dict(),
    "optimizer_state_dict": optimizer.state_dict(),
    "epoch": epoch,
    "val_loss": val_loss,
}, "checkpoint.pth")

# Load
checkpoint = torch.load("checkpoint.pth", map_location=device)
model.load_state_dict(checkpoint["model_state_dict"])
optimizer.load_state_dict(checkpoint["optimizer_state_dict"])
```

## Common Layers

| Layer | Purpose |
|-------|---------|
| `nn.Linear(in, out)` | Fully connected |
| `nn.Conv2d(in, out, kernel)` | 2D convolution (images) |
| `nn.MaxPool2d(kernel)` | Downsampling |
| `nn.BatchNorm1d/2d` | Normalize activations |
| `nn.Dropout(p)` | Regularization |
| `nn.Embedding(vocab, dim)` | Word/entity embeddings |
| `nn.LSTM(input, hidden)` | Recurrent layer |
| `nn.TransformerEncoder` | Transformer encoder |

## Best Practices

- **Always call `model.train()` and `model.eval()`** — dropout and batch norm behave differently
- **Use `torch.no_grad()` for inference** — no gradient tracking, faster, less memory
- **Gradient clipping** — `torch.nn.utils.clip_grad_norm_(model.parameters(), max_norm=1.0)`
- **Monitor GPU memory** — `nvidia-smi` or `torch.cuda.memory_summary()`
- **Use mixed precision** — `torch.cuda.amp` for faster training on modern GPUs

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Forgetting `.zero_grad()` | Gradients accumulate, training diverges | Call `zero_grad()` before each backward pass |
| Data not on same device | Runtime error | Move both model and data to `device` |
| Not calling `model.eval()` | Inconsistent dropout during validation | Always toggle eval mode |
| No validation loop | Can't detect overfitting | Always track val loss |
| Learning rate too high | Loss explodes to NaN | Lower LR, use schedulers |

## What's Next?

Learn how to evaluate your models in [Model Evaluation](model-evaluation.md), or revisit [Neural Networks & Deep Learning](neural-networks-and-deep-learning.md) for architecture guidance.
