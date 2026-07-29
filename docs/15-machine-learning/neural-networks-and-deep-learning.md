# Neural Networks & Deep Learning

> Architectures for learning complex patterns from large amounts of data.

> **Related:** [PyTorch](pytorch.md) | [scikit-learn](scikit-learn.md) | [What Is Machine Learning?](what-is-machine-learning.md)

---

## What Is It?

Deep learning uses multi-layer neural networks to learn hierarchical representations from data. It excels at unstructured data: images, audio, text, and video.

## The Neuron

A single neuron computes a weighted sum of its inputs, adds a bias, and passes through an activation function:

```
inputs  weights
x1 ──── w1 ──┐
x2 ──── w2 ──┼── Σ(w·x + b) → activation → output
x3 ──── w3 ──┘
```

## Activation Functions

| Function | Range | Used In | Formula |
|----------|-------|---------|---------|
| ReLU | `[0, ∞)` | Hidden layers | `max(0, x)` |
| Sigmoid | `(0, 1)` | Binary classification output | `1/(1+e^-x)` |
| Tanh | `(-1, 1)` | Hidden layers (older) | `(e^x-e^-x)/(e^x+e^-x)` |
| Softmax | `(0, 1)` sum=1 | Multi-class output | `e^x_i / Σ e^x_j` |

## Architectures

### Feedforward (MLP)

The basic building block: layers of neurons where each layer feeds into the next.

```
Input → Dense → ReLU → Dense → ReLU → Dense (output)
```

Use for: tabular data, regression, small-scale classification.

### Convolutional Neural Networks (CNN)

Designed for grid-structured data (images). Uses convolutional filters that slide over the input, detecting local patterns.

```
Input (image) → Conv → Pool → Conv → Pool → Dense → Output
```

| Component | What It Does |
|-----------|-------------|
| Convolution | Learnable filter slides over image, detects edges/textures |
| Pooling | Down-samples, reduces spatial size |
| Fully Connected | Makes final prediction based on learned features |

Use for: image classification, object detection, segmentation.

### Recurrent Neural Networks (RNN)

Processes sequences by maintaining a hidden state across time steps.

```
Input[t-1] → RNN → hidden[t-1]
Input[t]   → RNN → hidden[t]
Input[t+1] → RNN → hidden[t+1] → Output
```

| Variant | Key Feature |
|---------|-------------|
| LSTM | Long Short-Term Memory — handles long-range dependencies |
| GRU | Gated Recurrent Unit — simpler than LSTM, similar performance |

Use for: text, time series, audio, sequential data.

### Transformers

Process sequences in parallel (not sequentially) using self-attention. The dominant architecture for NLP and increasingly for vision.

```
Input → Self-Attention → LayerNorm → FFN → LayerNorm → Output
```

| Component | What It Does |
|-----------|-------------|
| Self-Attention | Each token attends to every other token |
| Multi-Head Attention | Multiple attention patterns in parallel |
| Positional Encoding | Injects order information |

Use for: text, translation, code generation, multi-modal models.

## When to Use Deep Learning

| Good Fit | Use Something Else |
|----------|-------------------|
| 100K+ training examples | Small dataset (<10K) |
| Images, audio, video | Tabular data with clear features |
| Complex patterns (translation, generation) | Simple patterns (linear relationships) |
| You have a GPU | No GPU and can't cloud |

## Best Practices

- **Start with a simple architecture** — one hidden layer before adding complexity
- **Use transfer learning** — start from a pre-trained model, fine-tune on your data
- **Monitor train/validation loss** — diverging curves signal overfitting
- **Regularize** — dropout, weight decay, early stopping, data augmentation
- **Normalize inputs** — zero mean, unit variance per channel

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Too few data | Overfitting immediately | Use transfer learning or simpler model |
| Learning rate too high | Loss diverges (NaN) | Lower LR, use learning rate schedulers |
| No normalization | Training is unstable | Normalize inputs, use batch normalization |
| Too deep for the data | Last layers learn nothing | Match depth to problem complexity |
| Ignoring overfitting | Great train, bad test | Dropout, weight decay, more data |

## What's Next?

Implement these architectures in [PyTorch](pytorch.md), or back up to [scikit-learn](scikit-learn.md) for classical approaches.
