# Object Discovery in 3D Scenes via Shape Analysis

## Metadata
- **Title:** Object Discovery in 3D Scenes via Shape Analysis
- **Authors:** Andrej Karpathy, Stephen Miller, Li Fei-Fei
- **Venue:** International Conference on Robotics and Automation (ICRA 2013)
- **Year:** 2013
- **URL:** https://cs.stanford.edu/~karpathy/discovery/
- **Dataset:** 58 indoor scenes captured via open-source Kinect Fusion implementation

## Abstract
The work presents a method for discovering object models from 3D meshes of indoor environments. The pipeline decomposes a scene into candidate mesh segments and ranks each by "objectness" -- a quality separating objects from clutter.

Five intrinsic shape measures are proposed: compactness, symmetry, smoothness, local convexity, and global convexity. A recurrence measure is also introduced, based on the idea that frequently occurring geometries are more likely to correspond to complete objects.

## Results
- Evaluated on 58 indoor scenes captured via an open-source Kinect Fusion implementation.
- Achieved an Average Precision score of 0.92 in distinguishing objects from clutter.
- The dataset was released publicly.
- Evaluated in both supervised and unsupervised settings.

## Code & Data
- Code released (C++, Matlab) requiring Point Cloud Library.
- 58 scenes of .ply colored mesh files released (kinfu_scenes.zip, 178.4 MB).
- Annotation interface provided for labeling data.

## BibTeX
```
@inproceedings{Karpathy_ICRA2013,
  author = "Andrej Karpathy and Stephen Miller, and Li Fei-Fei",
  title = "Object Discovery in 3D Scenes via Shape Analysis",
  booktitle = "International Conference on Robotics and Automation (ICRA)",
  year = "2013",
}
```

## Acknowledgments
Partially supported by an Intel ISTC research grant. Stephen Miller was supported by the Hertz Foundation Google Fellowship and the Stanford Graduate Fellowship.

## 三岁版
这个研究教电脑看3D房间（就像用3D扫描仪拍下来的房间），让它自己发现房间里有哪些"东西"。电脑学会通过形状来判断——圆圆的可能是"球"，方方的可能是"桌子"——不需要人告诉它这是什么。就像小朋友第一次进一个房间，自己就能看出"这里是沙发，那里是台灯"一样。