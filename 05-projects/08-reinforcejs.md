# REINFORCEjs

**GitHub:** https://github.com/karpathy/reinforcejs
**Stars:** 1.5k | **Forks:** 354 | **Language:** HTML (65.4%), JavaScript (34.6%)
**License:** MIT

## Description

A Reinforcement Learning library that implements several common RL algorithms, all with web demos. Algorithms run in the browser with no installation required.

### Included Algorithms

- **Dynamic Programming** methods — for finite state/action spaces with environment dynamics
- **(Tabular) Temporal Difference Learning** — SARSA/Q-Learning
- **Deep Q-Learning** — Q-Learning with function approximation using Neural Networks
- **Stochastic/Deterministic Policy Gradients** and Actor Critic architectures for continuous action spaces (noted as "very alpha, likely buggy or at the very least finicky and inconsistent")

## Code Structure

Two global variables are exported: `R` and `RL`.

- `R` — utilities for building expression graphs (e.g. LSTMs) and performing automatic backpropagation. Fork of Karpathy's other project, [recurrentjs](https://github.com/karpathy/recurrentjs).
- `RL` — holds algorithm implementations: `RL.DPAgent`, `RL.TDAgent`, `RL.DQNAgent`

## Example Usage

```javascript
var env = {};
env.getNumStates = function() { return 8; }
env.getMaxNumActions = function() { return 4; }

var spec = { alpha: 0.01 };
agent = new RL.DQNAgent(env, spec);

setInterval(function(){
  var action = agent.act(s); // s is an array of length 8
  // execute action in environment and get the reward
  agent.learn(reward); // agent improves its Q,policy,model, etc.
}, 0);
```

Full documentation and demos available on the [main webpage](https://cs.stanford.edu/people/karpathy/reinforcejs/).

## License

MIT

---

*Fetched from https://github.com/karpathy/reinforcejs on 2026-05-09*

## 三岁版

REINFORCEjs 是教电脑"自己学会玩游戏"的工具。就像你教小狗学会坐下就给零食一样，电脑做对了就"奖励"它，做错了就"扣分"，慢慢它就学会怎么玩得更好。一切都在浏览器里运行，不用装任何东西。