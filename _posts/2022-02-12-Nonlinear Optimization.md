---
title: "Nonlinear Optimization"
date: 2022-02-12 22:58:00 -0400
categories: math
---

## Nonlinear Optimization

---

비선형 최적화에 대해 이해하고, 다양한 최적화 방법들을 알아봅니다.
그리고 ceres, g2o 같은 최적화 툴을 통해 문제를 해결하는 법을 알아봅시다.

### **[최적화 기법의 직관적 이해](https://devshin.notion.site/d1e6c14f76b64e029da59e03c4eca1a9)**

- 일차미분을 이용한 최적화
- 이차미분을 이용한 최적화 기법
- 일차미분 vs 이차미분
- Line Search 방법 (일차미분의 문제점 해결)
- Trust Region 방법 (이차미분의 문제점 해결)
- Damping & Saddle-free 방법
- 다변수 함수에서의 최적화
- 비선형 최소자승 문제 (nonlinear least squares problem)

### **[Nonlinear Optimization (least squares)](https://devshin.notion.site/Nonlinear-Optimization-least-squares-35bb2a3ebcc74074906dd769af372cb3)**

- 최소자승법 & 가중최소자승법
- Gradient Decent 탐색 방법 (경사하강법)
- 뉴턴법 (Newton-Raphson)
- 가우스-뉴턴법 (Gauss-Newton Method)
- Levenberg–Marquardt (레벤버그-마쿼트)
- 정리

### **[Solve Problem with Optimization Tools](https://devshin.notion.site/Solve-Problem-with-Optimization-Tools-8e378c64bf17434e89343a8dced6ee89)**

- Example
- Curve Fitting with Ceres
- Curve Fitting with g2o

## 참고자료

---

[최적화 기법의 직관적 이해](https://darkpgmr.tistory.com/149)

[함수최적화 기법 정리 (Levenberg-Marquardt 방법 등)](https://darkpgmr.tistory.com/142)

[경사하강법(gradient descent)](https://angeloyeo.github.io/2020/08/16/gradient_descent.html)