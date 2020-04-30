<!-- md preview: Show the rendered HTML markdown to the right of the current editor using ctrl-shift-m.-->

# Scan Context

---
## NEWS (April, 2020)
- C++ implementation released!
  - See the directory `cpp/module/Scancontext`
  - Features 
    - Light-weight: a single header and cpp file named "Scancontext.h" and "Scancontext.cpp"
      - Our module has KDtree and we used <a href="https://github.com/jlblancoc/nanoflann"> nanoflann </a>. nanoflann is an also single-header-program and that file is in our directory.
    - Easy to use: A user just remembers and uses only two API functions; `makeAndSaveScancontextAndKeys` and `detectLoopClosureID`.
    - Fast: tested the loop detector runs at 10-15Hz (for 20 x 60 size, 10 candidates)
  - Example: Real-time LiDAR SLAM
    - We integrated the C++ implementation within the recent popular LiDAR odometry code, <a href="https://github.com/RobustFieldAutonomyLab/LeGO-LOAM"> LeGO-LOAM </a>.
    - That is, LiDAR SLAM = LiDAR Odometry (LeGO-LOAM) + Loop detection (Scan Context) and closure (GTSAM)
    - For details, see `cpp/example/lidar_slam` or refer this <a href="https://github.com/irapkaist/SC-LeGO-LOAM"> repository </a>.
---


- Scan Context is a global descriptor for LiDAR point cloud, which is proposed in this paper and details are easily summarized in this <a href="https://www.youtube.com/watch?v=_etNafgQXoY"> video </a>.

```
@INPROCEEDINGS { gkim-2018-iros,
  author = {Kim, Giseop and Kim, Ayoung},
  title = { Scan Context: Egocentric Spatial Descriptor for Place Recognition within {3D} Point Cloud Map },
  booktitle = { Proceedings of the IEEE/RSJ International Conference on Intelligent Robots and Systems },
  year = { 2018 },
  month = { Oct. },
  address = { Madrid }
}
```
- This point cloud descriptor is used for place retrieval problem such as place
recognition and long-term localization.


## What is Scan Context?

- Scan Context is a global descriptor for LiDAR point cloud, which is especially designed for a sparse and noisy point cloud acquired in outdoor environment.
- It encodes egocentric visible information as below:
<p align="center"><img src="example/basic/scmaking.gif" width=400></p>

- A user can vary the resolution of a Scan Context. Below is the example of Scan Contexts' various resolutions for the same point cloud.
<p align="center"><img src="example/basic/various_res.png" width=300></p>


## How to use?: example cases
- The structure of this repository is composed of 3 example use cases.
- Most of the codes are written in Matlab.
- A directory _matlab_ contains main functions including Scan Context generation and the distance function.
- A directory _example_ contains a full example code for a few applications. We provide a total 3 examples.
 1. _**basics**_ contains a literally basic codes such as generation and can be a start point to understand Scan Context.

 2. _**place recognition**_ is an example directory for our IROS18 paper. The example is conducted using KITTI sequence 00 and PlaceRecognizer.m is the main code. You can easily grasp the full pipeline of Scan Context-based place recognition via watching and following the PlaceRecognizer.m code. Our Scan Context-based place recognition system consists of two steps; description and search. The search step is then composed of two hierarchical stages (1. ring key-based KD tree for fast candidate proposal, 2. candidate to query pairwise comparison-based nearest search). We note that our coarse yaw aligning-based pairwise distance enables reverse-revisit detection well, unlike others. The pipeline is below.
<p align="center"><img src="example/place_recognition/sc_pipeline.png" width=600></p>

 3. _**long-term localization**_ is an example directory for our RAL19 paper. For the separation of mapping and localization, there are separated train and test steps. The main training and test codes are written in python and Keras, only excluding data generation and performance evaluation codes (they are written in Matlab), and those python codes are provided using jupyter notebook. We note that some path may not directly work for your environment but the evaluation codes (e.g., makeDataForPRcurveForSCIresult.m) will help you understand how this classification-based SCI-localization system works. The figure below depicts our long-term localization pipeline. <p align="center"><img src="example/longterm_localization/sci_pipeline.png" width=600></p> More details of our long-term localization pipeline is found in the below paper and we also recommend you to watch this <a href="https://www.youtube.com/watch?v=apmmduXTnaE"> video </a>.
```
@ARTICLE{ gkim-2019-ral,
    author = {G. {Kim} and B. {Park} and A. {Kim}},
    journal = {IEEE Robotics and Automation Letters},
    title = {1-Day Learning, 1-Year Localization: Long-Term LiDAR Localization Using Scan Context Image},
    year = {2019},
    volume = {4},
    number = {2},
    pages = {1948-1955},
    month = {April}
}
```

  4. _**SLAM**_ directory contains the practical use case of Scan Context for SLAM pipeline. The details are maintained in the related other repository _[PyICP SLAM](https://github.com/kissb2/PyICP-SLAM)_; the full-python LiDAR SLAM codes using Scan Context as a loop detector.

## Acknowledgment
This work is supported by the Korea Agency for Infrastructure Technology Advancement (KAIA) grant funded by the Ministry of Land, Infrastructure and Transport of Korea (19CTAP-C142170-02), and [High-Definition Map Based Precise Vehicle Localization Using Cameras and LIDARs] project funded by NAVER LABS Corporation.

## Contact
If you have any questions, contact here please
 ```
 paulgkim@kaist.ac.kr
 ```
