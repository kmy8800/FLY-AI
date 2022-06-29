# Kubernetes

## Deployment

### 1. Deployment(배포)

- Pod와 Replicaset에 대한 "관리"를 제공하는 단위  
  - 관리: Self-healing, Scaling, Rollout(무중단 업데이트) 등  
    - Self-healing: container가 잘 작동하는지 ping을 통해 확인  
    - Scale out: component 수를 늘림(웹 서버)  
    - Scale up: component 용량을 늘림(데이터베이스)  
    - Kubernetes는 container의 수를 늘리는 Scale out을 주로 사용  
    - Rollout: component를 순차적으로 업데이트하여 중단 없이 업데이트  
    
### 2. Deployment 생성
#### Deployment.yaml
```bash
apiVersion: apps/v1 # kubernetes resource 의 API Version
kind: Deployment # kubernetes resource name
metadata: # 메타데이터 : name, namespace, labels, annotations 등을 포함
  name: nginx-deployment
  labels:
    app: nginx
spec: # 메인 파트 : resource 의 desired state 를 명시
  replicas: 3 # 동일한 template 의 pod 을 3 개 복제본으로 생성합니다.
  selector:
    matchLabels:
      app: nginx
  template: # Pod 의 template 을 의미합니다.
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx # container 의 이름
        image: nginx:1.14.2 # container 의 image
        ports:
        - containerPort: 80 # container 의 내부 Port
```

```bash
kubectl apply -f deployment.yaml
```

### 3. Deployment 조회

```bash
kubectl get deployment
kubectl get deployment,pod
```

### 4. Deployment Auto-healing
```bash
kubectl delete pod <pod name>
```
pod를 삭제하더라도 replicas 수를 맞추기 위해 pod가 자동으로 복구됨
