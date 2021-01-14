---
title: "Visual SLAM"
date: 2021-01-14 09:53:00 -0400
categories: slam
---


# Feature-based SLAM
### **Mono SLAM**
- 특징점 몇개만 잡아서 사용
- 공간이 커질 수록 계산량이 많아지기 때문에 방 하나 사이즈에 적합함

### **PTAMA**
- Thread를 분리해서 사용
- 매들어오는 이미지의 feature를 통해 keyframes 생성 (Tracking)
- 그 때마다 mapping
- 성능 생각보다 좋음

### **ORB SLAM**
- 자동으로 첫이미지를 따고 키프레임이 나올 때까지 대기 (homography와 fundamental matrix 중 더 좋은 결과로 초기화, 둘 다 실패시 다시 뽑음)
- homography: 평면에 feature point가 있을 경우, socore 높음
- fundamental matrix: 3D point가 3차원 공간에 퍼져있는 경우, score 높음
- 상업용으로 좋은 이유 - user input 필요 X
- rotation에 약함
<br/><br/>

# Direct SLAM
- dense -> semi-dense -> sparse
- High frame rate 카메라 필요

### **LSD SLAM**
- point 기반의 feature를 뽑는게 아니라 Line 기반으로 feature를 뽑음
- CPU 단독으로 적용 가능
- semi-dense

### **SVO**
- frame-to-frame tracking
- mapping 시에는 keyframes만 활용

### **SVO2**
- Multi camera / 드론 타겟팅

### **DSO**
- No feature-based 방식
- Loop closure가 없음
- 그럼에도 불구하고 성능이 좋음
<br/><br/>

# Visual-Inertial SLAM
- SVO + KF: Low CPU usage, but high error
- OKVIS: Connot run at low clock CPU
- ROVIO: 성능은 보통이나 Laptop, sbc에서 같은 성능
- VINS-Mono: CPU 사용량이 큼
- Filtering-based approach vs Optimization appoach
- Optimization appoach가 우세하기는 하지만 높은 CPU usage 때문에 Filtering-based approach를 놓지 못함

### VINS MOMNO
- VI SLAM의 끝판왕, 그러나 무거움
- Odometry 구성에 있어서는 ORB 보다 안 좋을 수 있음
<br/><br/>
# ORB SLAM2 vs RTAPMAP
*Paper: Benchmark of Visual SLAM Algorithms: ORB-SLAM2 vs RTAB-Map*
## **ORB-SLAM2**
- 특징점 추적, 매핑, 루프 폐쇄, localization
- 정확한 위치 추정 가능
- 카메라 궤적과 3D 재구성 하는 단안, 스테레오, RGB-D 카메라 용 실시간 SLAM 라이브러리
- 단안 ORB-SLAM2
	- 단 하나의 카메라만 사용
	- 1. 이미지를 회색조로 변경
	- 2. 지형지물 감지, map, 위치 초기화 (단안 SLAM은 단일 이미지에서 깊이를 알 수 없기에 초기 map을 만드는 절차가 필요)
	- 3. 초기화되면 맵 생성
- 스테레오 ORB-SLAM2
	- 스테레오 카메라 사용
	- 스테레오 SLAM의 특징 감지는 단안 SLAM 보다 낫다
	- 초기화는 빠르며 단안 SLAM에 비해 많은 장점을 갖고있다.
	- 두개의 ORB에 대해 일치하는 항목을 검색한다
	- 일치하는 항목을 사용하여 스테레오 키프인트를 생성
- RGB Depth ORB-SLAM2
	- depth가 있는 RGB 이미지가 필요하다.
	- RGB-D 카메라의 경우 RGB 이미지에서 ORB 기능을 추출하고 좌표가있는 각 기능에 대해 깊이 값 d를 *(논문 식 1)* 에 넣는다.
		- Fx는 수평 초점 거리, b는 적외선 카메라와 structured light projector 사이의 기준선
## **RTAP-MAP SLAM**
- RTAP-Map은 Real TIme Appearance Based Mapping을 의미
- RTAB-Map은 2013년 부터 오픈 소스 라이브러리 배포
- RTAB-Map은 비주얼 및 라이더 SLAM을 모두 지원하여 사용자가 다양한 로봇 및 센서를 사용하여 다양한 애플리케이션에 대해 다양한 3D 및 2D 솔루션을 구현하고 
비교할 수 있는 도구를 하나의 패키지로 제공
- RGB 이미지와 depth이미지를 사용하여 맵을 구성한다. (그래프 생성됨)
- 그래프가 업데이트되면 RTAB-Map은 새 이미지를 모든 이미지와 비교하여 루프 폐쇠찾음
- 그래프의 각 노드에 대해 RGB 및 depth 이미지 에서 포인트 클라우드를 생성
- 포인트 클라우드는 노드의 포즈를 사용하여 변환된다
- 다음 3D 맵 생성
## **5장 - 결론**
- ORB SLAM
	-  단안 ORB-SLAM은 매핑 중에 포인트를 잃고 초기화 속도가 매우 느리고 단안 ORB-SLAM을 제외하고 완벽하게 작동한다.
	- *(논문 fig. 3)* odometry와 특징점을 추적하는데 효율적이다.
	- ORB SLAM은 3D 맵을 생성
	- ORB SLAM은 실내.외 환경에서 맵을 만들고 궤적을 만드는데 성공
	- 루프 폐쇠를 성공적으로 감지
	- *(논문 fig 4,5)* 단안 ORB SLAM의 유일한 문제점은 초기화시 느리고 매핑 중에 포인트를 읽는것, 이로 인해 ORB SLAM은 위치를 잃고 매핑을 지속할수 없다.
	- 문제점을 해결하기 위해서는 스테레오, RGB-D 카메라를 사용하는 것(ORB-SLAM2)
	- *(논문 표1)* ORB-SLAM2를 사용하여 Ground Truth와 비교한 결과
	- 실내에서는 ground Truth, ORB Stereo, ORB RGBD 모두 결과가 정확하게 나왔지만 실외 에서는 스테레오 카메라가 RGBD에 비해 더 나은 결과를 보여줌 (논문 fig 7)
- RTAB-MAP SLAM
	- RTAP-MAP SLAM은 실내에서만 테스트 진행
	- 지도를 만들고 루프 폐쇠를 감지하는 데 성공
	- *(논문 표2)* RTAPMAP의 매핑 및 궤적 추정은 매우 좋지만 거리 측정은 그렇지 않다. RTAPMAP에 의해 추정 된 거리는 ORB SLAM의 거리보다 좋지 않다.
	- ORB SLAM  VS RTAP-MAP SLAM
	- *(논문 표 3)* 거리측정 결과는 RTAP-MAP 보다 ORB SLAM 이 더 정확하다고 볼수 있다. 
## **6장 - 마무리**
- ORB SLAM은 정확한 궤도를 추정하고 정확한 odomerty 제공
- 하지만 단안 ORB SLAM은 좋은 궤적이나 거리를 추정을 제공하지 못함
- RTAPMAP은 궤도 추정은 정확하지만 odomerty는 ORB SLAM만큼 정확하지 않음
- 궤도 추정에 있어서 ORB SLAM과 RTAPMAP 비교할 때 RTAPMAP이 더 나은것으로 나타남
- 그러나 거리 측정에서는 ORB SLAM이 더 좋다