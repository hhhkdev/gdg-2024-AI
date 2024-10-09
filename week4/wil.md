# 3회차 스터디

# 모델이 어떻게 학습하는지

Loss Function, Optimization

### Loss Function

---

선형 분류기에서 Weight matrix를 어떤 값으로 정해야 하는가?

→ Weight matrix: 입력 이미지를 정확하게 분류하기 위함. → Loss Function을 이용

⇒ 예측과 실제 정답 간의 차이(오차)를 수치화 → Weight Matrix 값 업데이트

> Loss를 최소화하여 분류 정확도를 최대화함.

- 문제의 특성, 데이터 유형에 따라 Loss Function을 선택할 수 있음.

  - 회귀 문제 → MSE(Mean Squared Error)
    - 연속형 변수를 예측할 때 사용함.
  - 분류 문제 → SVM Loss, Cross-Entropy Loss
    ### SVM Loss
    - **각 확률 값들 사이에서, 정답과의 차이 값 + 1을 Loss로 결정함.**
    → 정답이 틀렸을 경우, 본인보다 높은 값들과의 차 + 1을 모두 합한게 Loss값
    → 해당 Loss값의 합을 데이터 개수로 나누면 L값.
    ### Cross-Entropy Loss
    정답 Label이 단 하나만 1인 벡터임. → 네트워크 출력을 확률로 해석하고 싶으면 실수인 raw 출력을 바꿈.
    Softmax 함수로 뽑아낸 벡터(의 각각 log를 씌운 값)와 정답 벡터 사이의 계산.
    > 정답을 1에 가깝게 예측해냈는가?에 따라 Loss 값이 달라짐.
    ### Softmax vs. SVM
    Cross-Entropy가 확률 분포 차이에 더 민감하게 반응함.

- SVM : 분류 경계(결정 경계)에 가까운 데이터들 → 해당 범위 마진을 키우는게 목표.

### Regularization

- Overfitting
  - 모델이 훈련 데이터에 너무 가깝게 맞춰짐 → 새 데이터에 대응을 못함.
  - → 모델이 적당히 복잡하도록 하는 것이 Regularization
    - 가중치 w가 작아지도록 함. → 노이즈에 영향을 덜 받음.

⇒ Regularization으로 Overfitting을 막아야 함!

> 적절한 가중치를 갖는 걸 목표로 함.

- L2: 매끄러운 그래프를 원할 때. 큰 가중치에 큰 패널티. 모든 특성이 극단적이지 않도록 함.
- L1: 분류기가 복잡할 때. 가중치 값에 0이 많도록 함.

### Optimization

Loss Function이 줄어들도록?

w는 초기에는 랜덤 초기화 → 2차 함수 형식에서는 최저치로 이동시키게 하면 됨.

- 가장 빠르게 손실함수 줄어드는 방향 → 가장 가파르게 감소. ⇒ 최소 지점으로 가기 위해서 가장 가파르게 감소하는 방향으로.

> Gradient Descent

- Vanila Gradient Descent: 로컬 미니멈을 일반화할 수 없는 문제 해결.
  → Global Minimum을 찾기 위해 노력해야 함.
  - Momentum(관성): 이전 방향을 고려해서 현재 방향에 반영함.
  - Adaptive Learning rate: 과거의 정보를 통해 각 파라미터마다 다른 학습률
  - Learning rate: 초기에 높은 학습률 → 빠르게 최적점을 찾긴함. ⇒ **적절한 시점에 학습률을 높여야 로컬 미니멈을 탈출함.**
    - 고정된 상수값이 아님. 학습을 하면 할 수록 lr을 조정해나감.
