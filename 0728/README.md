# Deep Learning

## Perceptrons
- 두 종류의 클래스를 직선으로 분류하는 선형 분류기
- XOR 문제를 풀기 위해선 2개 이상의 Perceptron 필요
- MLP(Multi Layer Perceptron)

### Backpropagation(오차 역전파)
- Total Error에 대해 weight의 편미분 값으로 weight 조정
- MLP에서는 chain rule을 통해 오차 전파
- Vanishing Gradient: 입력층으로 갈수록 역전파 과정에서 미분값이 0에 가까워 지면서 학습이 되지 않음
- ReLU(Rectified Linear Unit): 입력 x가 0보다 작으면 0, 크면 x

### Optimizer
- GD, SGD, Momentum, Adam*, ...

### Dropout
- overfitting 방지

### Regularization
- L2 Norm

### Weight Initialization
- Xavier Glorot 초기화: 활성화 함수가 Sigmoid일 때 사용
- He: ReLU일 때

### Batch Normalization
- 가중치의 초기값과 관계없이 활성화값을 표준정규분포로 정규화 -> gradient vanishing/exploding 해결
- 학습 속도 향상, 초기값 강건, overfitting 억제

### Data Augmentation
- 데이터 증강을 통해 overfitting 방지

### Early Stopping
- Validation loss의 감소(기울기)가 0에 가까워지면 학습 중단 -> overfitting 방지

### Hyperparameter 탐색
