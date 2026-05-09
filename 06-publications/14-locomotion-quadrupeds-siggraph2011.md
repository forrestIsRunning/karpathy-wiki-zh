# Locomotion Skills for Simulated Quadrupeds

## Metadata
- **Title:** Locomotion Skills for Simulated Quadrupeds
- **Authors:** Stelian Coros, Andrej Karpathy, Ben Jones, Lionel Reveret, Michiel van de Panne
- **Venue:** ACM Transactions on Graphics (Proceedings of SIGGRAPH 2011)
- **Year:** 2011
- **URL:** http://www.cs.ubc.ca/~van/papers/2011-TOG-quadruped/index.html

## Description
The paper presents an integrated system of gaits and skills for physics-based quadruped simulation. The simulated dog can perform a wide range of motions: walk, trot, pace, canter, transverse gallop, rotary gallop, leaps on/off platforms and over obstacles, sitting, lying down, standing up, and recovering from a fall.

## Technical Approach
The controllers rely on several key abstractions: gait graphs, a dual leg frame model, a flexible spine model, and the extensive use of internal virtual forces applied via the Jacobian transpose. Optimizations tune these control abstractions to achieve robust gaits and leaps with desired motion styles.

## Results & Evaluation
- Gaits assessed for robustness against push disturbances and travel over uneven terrain.
- Simulated motions compared against motion data captured from a real filmed dog.
- Demonstrated a wide repertoire of quadruped locomotion and behavior skills.

## Materials Available
- Paper PDF (2.1 MB) and supplemental material (0.4 MB)
- Windows binary code with readme
- Embedded video (no audio)

## Funding
- NSERC (Natural Sciences and Engineering Research Council of Canada)
- GRAND NCE (Graphics, Animation, and New Media)

## Affiliations
- University of British Columbia
- Disney Research Zurich
- INRIA/Grenoble University/CNRS

## 三岁版
这个研究在电脑里做了一只"机器狗"，教它怎么走路、跑步、跳跃，甚至能从摔倒自己爬起来。这只虚拟狗狗能像真狗一样走、小跑、狂奔、跳过障碍物。就像给电脑里的小狗装上了一个"运动控制器"，告诉它四条腿该怎么动。