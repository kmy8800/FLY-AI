# DecisionTree

- Gain: Node를 내려갈수록(Root Node -> Leaf Node) 얻는 정보 이득
- Gain이 얼마나 변하느냐가 중요(Scaling이 필요없음), 거리와 상관없음
- 이론적으로는 Encoding이 필요없음
- weak estimator: 약한 분류기  -> ensemble algorithm적용으로 정확도 높임

Max depth: 트리 깊이
Min_sample_split: 분기를 하기위한 최소한의 샘플수
리프노드가 가지고있어야하는 최소한의 샘플수


# 앙상블(Ensemble)
- 강력한 하나의 모델을 사용하는 대신 보다 약한 모델 여러 개를 조합하여 더 정확한 예측에 도움을 주는 방식
  - 보팅(Voting): 같은 데이터로 서로 다른 분류기를 학습시켜 투표하여 결정, 거의 안씀
  - 배깅(Bagging): 하나의 모델을 다양하게 바꿔가며 학습시켜(데이터, 파라미터 등) 가장 투표수가 많은 것을 선택,  RandomForest(DecisionTree를 여러개) 
    부트스트랩(Bootstrap): 데이터로부터 복원(중복허용), 일반화
  - 부스팅(Boosting): 앞선 모델의 결과를 반영하여 이후의 모델을 차례로 학습시켜 연결,  Adaboost, Gradient Boosting, lightGBM, XGBOOST, ...
    
    
  
# Naive Bayes Classifier
## 조건부 확률
- P(A|B): B사건이 발생했을 때, A사건이 발생할 확률 P(AnB) / P(B)

## Bayes Theorem
- P(A|B) = P(B|A) * P(A) / P(B)

## Naive Bayes
- 각 사건이 일어날 확률이 독립적이라고 가정
- 
