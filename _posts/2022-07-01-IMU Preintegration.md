---
title: "IMU Preintegration"
date: 2022-07-01 09:07:00 -0400
categories: slam
use_math: true
---

## IMU Preintegration

### [Keyframe](https://www.notion.so/devshin/IMU-Preintegration-c57d7d74c5494aee9c593af8642b992b#3b2763bad0674ea4a17dcffc37809eb5)

### [Rotation from 2D to 3D](https://www.notion.so/devshin/IMU-Preintegration-c57d7d74c5494aee9c593af8642b992b#954b3f740c614c90bfbed398100d7784)

### [Uncertainty Description in SO(3)](https://www.notion.so/devshin/IMU-Preintegration-c57d7d74c5494aee9c593af8642b992b#f4c4f19f7f214a9a89899f1c0f2c1f45)

- Rotation에 대한 uncertainty
- Graph SLAM 관점에서의 uncertainty
- manifold에서 IMU preintegration의 목적

### [IMU Model and Motion Integration](https://www.notion.so/devshin/IMU-Preintegration-c57d7d74c5494aee9c593af8642b992b#1f78ec3bb0f844a4aba45ba5eec7fda6)

- discrete-time system 상에서 Hz가 높은 IMU sensor를 통해 motion을 어떻게 표현할까?
- IMU 센서 특성
- Motion Integration

### [Preintegrated IMU Measurements](https://www.notion.so/devshin/IMU-Preintegration-c57d7d74c5494aee9c593af8642b992b#5d7eecedbf8e451788f227b2372927fb)

- Definition & Assumption
- Derivation of Preintegrated IMU Measurements
  - Preintegrated Rotation Measurements
  - Preintegrated Velocity Measurements
  - Preintegrated Position Measurements
- Do the Uncertainties behave like Gaussian distribution?
- Bias Update
- 결론

---

#### 위 내용은 [Hyungtae Lim님의 IMU Preintegration 시리즈](https://limhyungtae.github.io/2022-04-01-IMU-Preintegration-(Easy)-1.-Introduction/)를 재정리 한 포스트 입니다.