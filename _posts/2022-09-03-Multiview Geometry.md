---
title: "Multiview Geometry"
date: 2022-09-03 23:18:00 -0400
categories: slam
use_math: true
---

### Bundle Adjustment

- **Unknown**
    - `Position of 3D points` and `each camera’s relative pose` ($6n+3m$ DoF)
- **Given**
    - Point correspondence
    - camera matrices
    - position of 3D points
    - each camera’s relative pose
- **Constraints**
    - $n \times m \times \text { projection } \mathbf{x}_i^j=\mathrm{P}_j \mathbf{X}_i=\mathrm{K}_j\left[\mathrm{R}_j \mid \mathbf{t}_j\right] \mathbf{X}_i$
- **Solution** ⇒ Non-linear least-square optimization
    - Cost Function
        - `Reprojection error`
            
            $\sum\limits_i^n \sum\limits_j^m v_i^j\left\|\mathbf{x}_i^j-\mathrm{P}_j \mathbf{X}_i\right\|_{\Sigma}^2 \quad \text { where } \quad v_i^j= \begin{cases}1 & \text { if } \mathbf{x}_i^j \text { is visible } \\ 0 & \text { otherwise }\end{cases}$
            
    - Optimization
        - Levenberg–Marquardt method
        - Gauss-Newton method

### Bundle Adjustment and Optimization Tools

- **OpenCV**
    - No function (but [cvsba](https://github.com/willdzeng/cvsba) is available as a sba wrapper.)
- **Bundle adjustment**
    - [sba](http://users.ics.forth.gr/~lourakis/sba/) (Sparse Bundle Adjustment)
    - [SSBA](https://github.com/chzach/SSBA/) (Simple Sparse Bundle Adjustment)
    - [pba](http://grail.cs.washington.edu/projects/mcba/) (Multicore Bundle Adjustment)
- (Graph) **Optimization**
    - [g2o](https://github.com/RainerKuemmerle/g2o) (General Graph Optimization)
    - [iSAM](http://people.csail.mit.edu/kaess/isam/) (Incremental Smoothing and Mapping)
    - [GTSAM](https://bitbucket.org/gtborg/gtsam/src/develop/)
    - [Ceres Solver](http://ceres-solver.org/) (Google)