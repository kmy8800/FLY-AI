
# ML Framework

### Boosting

#### Gradient Boosting

- 학습 시 앞의 분류기의 오차를 학습

- XGBoost
- LightGBM
- CatBoost: 범주형 데이터가 많을 때


### Stacking

- 학습 결과를 다시 회귀모형에 학습시켜 최적화


# Linear Regression
* 선형 회귀 모델
- 종속변수 y를 독립변수 x들의 선형 관계를 표현한 모델
- 오차
  - RSS(Residual Sum of Squared): 잔차 제곱합, (y_true - y_pred)^2 / 2
  - squared: 미분가능
  
  - MAE(Mean Absolute Error): 평균 절대값 오차
  - MSE(Mean Squared Error): 평균 제곱 오차, (y_true - y_pred)^2 / 2N
  - RMSE(Root Mean Squared Error): 평균 제곱근 오차 root(y_true - y_pred)^2 / 2N
  
- 최소 제곱법(Ordinary Least Squares)
  - 오차(RSS)의 편미분이 0이 되는 w
 
- 경사 하강법(Gradient Descent)
  - 여러 종류의 문제에서 최적의 해법을 찾을 수 있는 최적화 알고리즘
  - Cost Function을 최소화하기 위해 반복적으로 파라미터 조정
  - Cost Function: Loss Function(손실 함수)  ex) MSE, ...
  - 편미분을 통해 얻은 기울기 값의 learning rate를 곱해 반대방향으로 이동, 
  - 특성 스케일링
  
  - Batch Gradient Descent
  - Stochastic Gradient Descent(SGD*)
  - Mini-batch Gradient Descent

* 다중 회귀
- 독립변수가 여러 개

* 다항 회귀(Polynomial Regression)
- 2차 곡선을 그리기 위한 선형 회귀(w간의 관계는 선형)
- x의 n제곱 텀을 feature로 추가하여 회귀
- y = w1x + w2x^2 + w3x^5 + b
- 규제(regularization)
  - 과적합되지 않게 차수가 높은 항들의 weight를 0으로 가깝게 함
  - 손실함수에 w^2을 추가함(L2 Norm) -> w가 0에 가까운 쪽으로 학습됨
  - L1 Norm: Lasso Regularization
  - L2 Norm: Ridge Regularization

  
