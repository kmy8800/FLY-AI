# Kubernetes Service

## 1. Service란
  - Service는 쿠버네티스에 배포한 애플리케이션(Pod)을 외부에서 접근하기 쉽게 추상화한 리소스
  - Pod에 할당받은 IP는 내부 사설 IP(private IP, ex) 172.17.0.x)로 고정되어 있지 않음
  - Pod에 접근할 때 Pod의 IP가 아닌 Service를 통해 접근
  - Service는 고정된 IP를 가지며, Service는 하나 혹은 여러 개의 Pod와 매칭

- Private IP로는 접근 불가능
```bash
~$ curl -X GET <POD IP> -vvv
Note: Unnecessary use of -X or --request, GET is already inferred.
*   Trying 172.17.0.5:80...
* TCP_NODELAY set
* connect to 172.17.0.5 port 80 failed: No route to host
* Failed to connect to 172.17.0.5 port 80: No route to host
* Closing connection 0
curl: (7) Failed to connect to 172.17.0.5 port 80: No route to host
```

- Deployment를 매칭시킨 Service 생성
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-nginx
  labels:
    run: my-nginx
spec:
  type: NodePort # Service 의 Type 을 명시하는 부분입니다. 자세한 설명은 추후 말씀드리겠습니다.
  ports:
  - port: 80
    protocol: TCP
  selector: # 아래 label 을 가진 Pod 을 매핑하는 부분입니다.
    app: nginx 
```
