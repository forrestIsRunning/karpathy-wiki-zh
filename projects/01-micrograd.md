# micrograd

**GitHub:** https://github.com/karpathy/micrograd
**Stars:** 15.8k | **Forks:** 2.4k | **Language:** Jupyter Notebook (90.3%), Python (9.7%)
**License:** MIT

## 项目介绍

一个微型的 Autograd 引擎（别看它小，咬人可疼！）。它在动态构建的计算图（DAG）上实现了反向传播（reverse-mode autodiff），并在此基础上提供了一个带有 PyTorch 风格 API 的小型神经网络库。这两个组件都非常小——分别只有大约 100 行和 50 行代码。计算图仅对标量值进行操作，也就是说每个神经元都被分解成了单独的加法和乘法运算。尽管如此，它依然能够构建完整的深度神经网络来解决二分类问题。对教学目的来说非常有用。

这就像一个小小的"数学积木盒"，教电脑怎么自己学会做决定——比如猜一张图是猫还是狗。就像搭积木一样，它把很复杂的数学拆成一粒一粒的小珠子，一个个算清楚。虽然它很小，但里面藏着"深度学习"的大秘密！

## 安装

```
pip install micrograd
```

## 使用示例

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
print(f'{g.data:.4f}') # 输出 24.7041，这是前向传播的结果
g.backward()
print(f'{a.grad:.4f}') # 输出 138.8338，即 dg/da 的数值
print(f'{b.grad:.4f}') # 输出 645.5773，即 dg/db 的数值
```

## 训练神经网络

`demo.ipynb` 笔记本提供了训练一个 2 层神经网络（MLP）二分类器的完整演示。通过从 `micrograd.nn` 模块初始化神经网络，实现一个简单的 SVM "最大间隔"二分类损失函数，并使用 SGD 进行优化。

## 追踪与可视化

`trace_graph.ipynb` 笔记本可以生成 graphviz 可视化图形。例如，可以通过调用 `draw_dot` 来可视化一个简单的二维神经元。

## 运行测试

运行单元测试需要安装 PyTorch（用作梯度验证的参考）。然后执行 `python -m pytest`。

## 许可证

MIT

---

*数据获取自 https://github.com/karpathy/micrograd (2026-05-09)*