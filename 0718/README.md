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
