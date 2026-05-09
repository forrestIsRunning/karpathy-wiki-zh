# micrograd

**GitHub:** https://github.com/karpathy/micrograd
**Stars:** 15.8k | **Forks:** 2.4k | **Language:** Jupyter Notebook (90.3%), Python (9.7%)
**License:** MIT

## Description

A tiny Autograd engine (with a bite!). Implements backpropagation (reverse-mode autodiff) over a dynamically built DAG, along with a small neural networks library on top with a PyTorch-like API. Both components are tiny — approximately 100 and 50 lines of code respectively. The DAG operates only over scalar values, meaning each neuron is broken down into its individual adds and multiplies. Despite this, it can build entire deep neural networks for binary classification. Potentially useful for educational purposes.

## Installation

```
pip install micrograd
```

## Example Usage

```python
from micrograd.engine import Value

a = Value(-4.0)
b = Value(2.0)
c = a + b
d = a * b + b**3
c += c + 1
c += 1 + c + (-a)
d += d * 2 + (b + a).relu()
d += 3 * d + (b - a).relu()
e = c - d
f = e**2
g = f / 2.0
g += 10.0 / f
print(f'{g.data:.4f}') # prints 24.7041, the outcome of this forward pass
g.backward()
print(f'{a.grad:.4f}') # prints 138.8338, i.e. the numerical value of dg/da
print(f'{b.grad:.4f}') # prints 645.5773, i.e. the numerical value of dg/db
```

## Training a Neural Net

The notebook `demo.ipynb` provides a full demonstration of training a 2-layer neural network (MLP) binary classifier. This is done by initializing a neural net from the `micrograd.nn` module, implementing a simple SVM "max-margin" binary classification loss, and using SGD for optimization.

## Tracing / Visualization

The notebook `trace_graph.ipynb` produces graphviz visualizations. For example, a simple 2D neuron can be visualized by calling `draw_dot`.

## Running Tests

To run unit tests, PyTorch must be installed (used as reference for gradient verification). Then run `python -m pytest`.

## License

MIT

---

*Fetched from https://github.com/karpathy/micrograd on 2026-05-09*