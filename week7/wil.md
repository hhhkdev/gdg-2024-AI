# 6회차 스터디

# Object Detection 객체 탐지

어떤 객체각 어떤 위치에 있는지를 파악하는 태스크

### 이미지 분류를 잘 하는 모델이 있다고 치자.

- Object Detection을 잘하는 모델을 만들고 싶음.
  - 객체 같은 것을 Box로 잘라오는 모델을 통해 Object Detection을 진행함.

Bbox Prediction Loss + Class Predict Loss → 2-Stage 모델

## Two-Stage Detector

---

- Proposal Generator

객체가 존재하는가 비존재하는가 → 객체의 대략적인 위치

Region Proposal → NMS 처리

- Box Classifier

해당 객체가 무엇이고 위치가 정확히 어디인가

### Non-Max Suppression

가장 높은 score를 가진 박스 → 나머지 박스들과 IOU를 비교하여 threshold 이상인 박스들을 제거함.

IOU: 박스의 교집합 / 박스의 합집합 → 1에 가까울 수록 같은 object를 가리키고 있을 것.

### R-CNN

selective search로 ROI (Region of Interest)

고정된 크기로 warping → 똑같은 사이즈의 피쳐 맵을 뽑아 냄.

→ CNN feature를 확인하여 Linear SVM으로 classify, Bbox regression 진행

### Feat R-CNN

피쳐 맵을 너무 많이 연산함. → 1번만 CNN을 연산해놓고 가져다가 쓰는 방식

원래는 ConvNet 연산 전에 warping을 했음. → 따로 ROI Pooling을 진행함.

### ROI Pooling

등장 배경: warping은 비율이 꺠지고 원본 정보가 손실됨. → 여러 사이즈의 RoI들을 FC Layer에 넣기 위해 사이즈를 통일 시켜줌

- 단점: 데이터 유실, 원하지 않는 데이터 포함, misalignment

### RPN

앵커 박스 안에 객체가 있는가? → 학습할 수 있는 네트워크

사이즈별 앵커 박스를 만들어서 생성 → 조합

객체의 스코어가 객체일 확률을 NMS로 쳐냄 → 나머지 중 높은 애들을 뽑아서 classification 제안

### Faster R-CNN

RPN을 적용해서 더 빨라짐.

## One-Stage Detector

---

YOLO 시리즈 → 단순하긴 하지만 v1은 정확도가 떨어짐.

박스간 구분하는 이유: 하나의 Bbox가 크기가 다를 수 있음.

동일한 위치에서 두 개의 다른 클래스 예측

🔼 채널이 30인 7\*7 피쳐맵을 이용하는 방법

## Feature Pyramid Network

---

convolutional network에서 얻을 수 있는 피쳐맵을 쌓아올린 상태

각 층을 각자 RPN에 넣어줌. → 완전 하이레벨이 아니여도 처리할 수 있음.

층별로 똑같은 채널로 맞춰줌 (크기는 키우고)

→ CNN을 거칠 때 나올 수 있는 피쳐맵들이 다를 텐데, 이것들을 모아서 더 좋은 결과를 내보겠다!
