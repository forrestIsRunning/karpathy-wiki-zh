# World of Bits: An Open-Domain Platform for Web-Based Agents

## Metadata
- **Title:** World of Bits: An Open-Domain Platform for Web-Based Agents
- **Authors:** Tianlin Shi, Andrej Karpathy, Linxi Fan, Jonathan Hernandez, Percy Liang
- **Venue:** Proceedings of the 34th International Conference on Machine Learning (ICML 2017)
- **Publisher:** PMLR, Volume 70, Pages 3135-3144
- **Year:** 2017
- **URL:** http://proceedings.mlr.press/v70/shi17a.html
- **PDF:** http://proceedings.mlr.press/v70/shi17a/shi17a.pdf

## Abstract
While simulated game environments have greatly accelerated research in reinforcement learning, existing environments lack the open-domain realism of tasks in computer vision or natural language processing. The paper introduces World of Bits (WoB), a platform designed to advance reinforcement learning research in open-domain, realistic web environments. WoB requires agents to complete real internet tasks using low-level keyboard and mouse actions. Two key challenges are addressed: (1) curating a large, diverse set of web-based tasks, and (2) ensuring well-defined reward structures and reproducibility despite the web's transient nature. The methodology involves crowdworkers creating tasks from natural language questions and demonstrating solutions on real websites; HTTP traffic is cached to create a reproducible offline approximation of the web site. The paper demonstrates that agents trained through behavioral cloning and reinforcement learning can successfully complete a range of web-based tasks.

## Notes
- Introduces a platform for web-based RL agents interacting with real websites via keyboard and mouse actions.
- Uses HTTP caching for reproducibility.
- Combines behavioral cloning and RL for agent training.

## 三岁版
这个研究做了一个叫"World of Bits"的玩具，教电脑像小朋友一样上网。电脑要学会自己用鼠标点、用键盘打字，完成在网上买东西或者查资料的任务。就像教一个三岁小孩自己上网买东西一样，只不过是对电脑说的。