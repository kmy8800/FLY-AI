# ML

### Cross-validation
- Over-fitting을 방지
- validation dataset: 학습 결과를 검증하기 위해 사용
- 

### Label Encoding
- 문자로 표현된 범주형 데이터를 숫자로 변환
- A, B, C 학점: 점수로 표현 가능
- A형, B형, O형: one-hot encoding으로 feature 수를 늘림

### Normalization
#### Z-Score Normalization
- 평균과 표준편차를 활용한 normalization
- z - x-u / sigma

#### Min-Max Normalization
- 0~1
- x - min / xmax - smin

### Outlier

### Imbalanced Data
- sampling
  - Over-sampling: 소수 클래스의 샘플 개수를 늘림(Resampling, SMOTE, ADASYN)
  - Under-sampling: 다수 클래스의 샘플 개수를 줄임
  
### Confusion Matrix
+예측, +정답 (TP; True Positive)
+예측, -정답 (FP; False Positive)
-예측, +정답 (TN; True Negative)
-예측, -정답 (FN; False Negative)

- 정밀도, 민감도(재현율), 특이도, 정확도

- F1-score: 2 * (정밀도*재현율) / (정밀도+재현율)  # 조화평균, 정밀도 재현율이 한 쪽으로 편향되지 않도록 추가 보완하는 지표


### ROC
- Threshold 값을 변화시키면서 True Positive Ratio와 False Positive Ratio를 그래프로 나타냄
- 밑면적이 클수록 정확한 분류기

## Regression
- Regression: 오차가 최소값을 갖도록 모델을 최적화하는 알고리즘
- Error = y - y_pred
- mse
- 결정계수 R2(R square): 독립 변수가 종속변수를 얼마나 설명하고 있는지 나타내는 지표
- R2값이 0.3이라면, 독립변수가 종속변수의 30%를 설명한다.


## K-Nearest Neighbor(KNN)
- K개의 가장 가까운 유사도를 가진 기존 데이터에 따라 분류


### Distance
- Euclidean: 공간 상에서 두 점 사이의 거리 sqrt(x^2 + y^2)
- Manhattan Distance: 격자에서의 두 점 사이의 거리

- y가 연속형인 경우(Regression): 가장 가까이에 있는 데이터의 평균으로 새로운 데이터를 예측
- KNN-Hyperparameter: k, 최근접 이웃을 몇 개로 설정할 것인가.
- K=1: over-fitting
- K값이 커질수록 결정경계가 완만해지지만 과소적합이 발생할 수 있다.
- 일정 범위 내에서 k를 변경해가며, 가장 좋은 예측 결과를 보이는 k를 선정(Validation Error가 최소값을 갖는 k, Grid Search)

## Support Vector Machine(SVD)
- 선형, 비선형 판별 가능
- 복잡한 분류 문제에 적합
- 가장 전방에 있는 두 평행선찾아 거리(margin)가 최대가 되는 분류 경계선 찾음
- Soft Margin Classification: 에러(threshold는 설정해야함)를 고려한 SVD
- 다변량(다차원)은 결정경계가 면(Hyperplan)이 된다.
- 비선형 SVM: 커널트릭(kernel trick)
  - 커널을 통해 차원을 바꾸어 분류
  - 원래의 차원에서는 비선형분류
- Params
  - C: 클수록 hard margin, 에러를 인정하지않음
  - kernel: rbf(가우시안 커널), linear, poly, sigmoid, ...
  - degree: 다항식 커널의 차수 결정
  - gamma: 클수록 면이 구불거림, overfitting 가능성 증가
  - coef: 상수항
