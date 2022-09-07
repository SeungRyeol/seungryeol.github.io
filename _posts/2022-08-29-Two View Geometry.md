---
title: "Two View Geometry"
date: 2022-08-29 23:33:00 -0400
categories: slam
use_math: true
---

## Planar 2D-2D Geometry (Projective Geometry)

---

### Overview of Perspective Geometry

![Untitled](/assets/images/Two-view%20Geometry%2082b6f4f5e74d40cfa7c85a983c35a456/Untitled.png)

- **Planar Homography Estimation**

    ![Untitled](/assets/images/Two-view%20Geometry%2082b6f4f5e74d40cfa7c85a983c35a456/Untitled%201.png)

    - Unknown
        - `Planar homography (8 DoF)`
    - Given
        - Point correspondence $\left(\mathbf{x}_{1}, \mathbf{x}_{1}^{\prime}\right), \ldots,\left(\mathbf{x}_{n}, \mathbf{x}_{n}^{\prime}\right)$
    - Constraints
        - $n \times \text { projective transformation } \mathbf{x}_{i}^{\prime}=\mathrm{H} \mathbf{x}_{i}$
    - Solutions ($n \geq 4$) ⇒ `4-point algorithm`
        - OpenCV [cv::getPerspectiveTransform()](https://docs.opencv.org/4.x/da/d54/group__imgproc__transform.html#ga20f62aa3235d869c9956436c870893ae) and [cv::findHomography()](apple.com/kr-edu/store)
        - cf. More simplified transformations need less number of minimal correspondence.

            → Affine ($n \geq 3$), similarity ($n \geq 2$), Euclidean ($n \geq 2$)

    - [Note] Planar homography can be decomposed as relative camera pose.
        - OpenCV [cv::decomposeHomographyMat()](https://docs.opencv.org/4.x/d9/d0c/group__calib3d.html#ga7f60bdff78833d1e3fd6d9d0fd538d92)
        - cf. However, the decomposition needs to know camera matrices.

## General 2D-2D Geometry (Epiploar Geometry)

---

### Overview of Epipolar Geometry

![Untitled](/assets/images/Two-view%20Geometry%2082b6f4f5e74d40cfa7c85a983c35a456/Untitled%202.png)

### Fundamental Matrix

![Untitled](/assets/images/Two-view%20Geometry%2082b6f4f5e74d40cfa7c85a983c35a456/Untitled%203.png)

### Essential Matrix

![Untitled](/assets/images/Two-view%20Geometry%2082b6f4f5e74d40cfa7c85a983c35a456/Untitled%204.png)

### Epiplar Geometry

![Untitled](/assets/images/Two-view%20Geometry%2082b6f4f5e74d40cfa7c85a983c35a456/Untitled%205.png)

![Untitled](/assets/images/Two-view%20Geometry%2082b6f4f5e74d40cfa7c85a983c35a456/Untitled%206.png)

- **Relative Camera Pose Estimation (~ Fundamental/Essential Matrix Estimation)**

    ![Untitled](/assets/images/Two-view%20Geometry%2082b6f4f5e74d40cfa7c85a983c35a456/Untitled%207.png)

    - Unknown
        - Rotation and translation $\mathrm{R,t}$ (5 DoF; up-to scale “scale ambiguity”)
    - Given
        - Point correspondence $\left(\mathbf{x}_1, \mathbf{x}_1^{\prime}\right), \ldots,\left(\mathbf{x}_n, \mathbf{x}_n^{\prime}\right)$
        - camera matrices $\mathrm{K,K'}$
    - Constraints
        - $n \times \text { epipolar constraint }\left(\mathbf{x}^{\prime \top} \mathrm{F} \mathbf{x}=0 \text { or } \hat{\mathbf{x}}^{\prime \top} \mathrm{E} \hat{\mathbf{x}}=0\right)$
    - Solutions (OpenCV)
        - **Fundamental matrix**: 7/8-point algorithm (7 DoF)

            → **Estimation**: [cv::findFundamentalMat()](https://docs.opencv.org/3.4/d9/d0c/group__calib3d.html#ga59b0d57f46f8677fb5904294a23d404a) ⇒ 1 solution

            → **Conversion to $\mathrm{E}$**: $\mathrm{E}=\mathrm{K}^{\prime \top} \mathrm{FK}$

            → **Degenerate cases**: No translation, correspondence from a single plane

            → intrinsic & extrinsic camera parameters

        - **Essential matrix**: 5-point algorithm (5 DoF)

            → **Estimation**: [cv::findEssentialMat()](https://docs.opencv.org/3.4/d9/d0c/group__calib3d.html#ga0b166d41926a7793ab1c351dbaa9ffd4) ⇒ $k$ solutions

            → **Decomposition**: [cv::decomposeEssentialMat()](https://docs.opencv.org/3.4/d9/d0c/group__calib3d.html#ga54a2f5b3f8aeaf6c76d4a31dece85d5d) ⇒ 4 solutions “relative pose ambiguity”

            → **Decomposition with positive-depth check**: [cv::recoverPose()](https://docs.opencv.org/4.x/d9/d0c/group__calib3d.html#ga1b2f149ee4b033c4dfe539f87338e243) ⇒ 1 solution

            → **Degenerate case**: No translation ($\because \mathrm{E}=[\mathrm{t}]_{\times} \mathrm{R}$)

            → extrinsic camera parameters

        - **Planar homography**: 4-point algorithm (8 DoF)

            → **Estimation**: [cv::findHomography()](https://docs.opencv.org/3.4/d9/d0c/group__calib3d.html#ga4abc2ece9fab9398f2e560d53c8c9780) ⇒ 1 solution

            → **Conversion to calibrated $\mathrm{H}$**: $\widehat{\mathrm{H}}=\mathrm{K}^{\prime-1} \mathrm{HK}$
            → **Decomposition**: [cv::decomposeHomographyMat()](https://docs.opencv.org/3.4/d9/d0c/group__calib3d.html#ga7f60bdff78833d1e3fd6d9d0fd538d92) ⇒ 4 solutions
            → **Degenerate case**: Correspondence not from a single plane

            → intrinsic & extrinsic camera parameters + plane normal

#### 본 포스트는 최성록 교수님의 [An Inviation to 3D Vision](http://github.com/sunglok/3dv_tutorial) 자료를 정리한 것입니다.
