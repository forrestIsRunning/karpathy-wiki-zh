# REINFORCEjs

**GitHub:** https://github.com/karpathy/reinforcejs
**Stars:** 1.5k | **Forks:** 354 | **Language:** HTML (65.4%), JavaScript (34.6%)
**License:** MIT

## 项目介绍

一个强化学习库，实现了多种常见的强化学习算法，全部带有网页演示。算法在浏览器中运行，无需安装任何软件。

REINFORCEjs 是教电脑"自己学会玩游戏"的工具。就像教小狗学会坐下就给零食一样，电脑做对了就"奖励"它，做错了就"扣分"，慢慢它就学会怎么玩得更好。一切都在浏览器里运行，不用装任何东西。

### 包含的算法

- **动态规划（Dynamic Programming）**方法——适用于已知环境动态的有限状态/动作空间
- **（表格型）时序差分学习（Temporal Difference Learning）**——SARSA/Q-Learning
- **深度 Q 学习（Deep Q-Learning）**——使用神经网络进行函数近似的 Q-Learning
- **随机/确定性策略梯度（Stochastic/Deterministic Policy Gradients）**以及适用于连续动作空间的 Actor-Critic 架构（标注为"非常早期，很可能有 bug，或者至少很不稳定且不一致"）

## 代码结构

导出两个全局变量：`R` 和 `RL`。

- `R`——用于构建表达式图（例如 LSTM）和执行自动反向传播的工具。来自 Karpathy 的另一个项目 [recurrentjs](https://github.com/karpathy/recurrentjs) 的分支。
- `RL`——包含算法实现：`RL.DPAgent`、`RL.TDAgent`、`RL.DQNAgent`

## 使用示例

```javascript
var env = {};
env.getNumStates = function() { return 8; }
env.getMaxNumActions = function() { return 4; }

var spec = { alpha: 0.01 };
agent = new RL.DQNAgent(env, spec);

setInterval(function(){
  var action = agent.act(s); // s 是一个长度为 8 的数组
  // 在环境中执行动作并获得奖励
  agent.learn(reward); // agent 改进它的 Q 值、策略、模型等
}, 0);
```

完整的文档和演示可在[主页面](https://cs.stanford.edu/people/karpathy/reinforcejs/)上找到。

## 许可证

MIT

---

*数据获取自 https://github.com/karpathy/reinforcejs (2026-05-09)*