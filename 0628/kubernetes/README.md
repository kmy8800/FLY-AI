# Kubernetes

Kubernetes Master는 Worker Node(server) 중 load가 적은 Node에 일을 부여하는 매니저 역할

Container -> Pod -> Worker Node
Micro Service Architecture(MSA): 각각의 Container는 기능적인 단위(Service Component)로  
개별적인 업데이트가 가능함

##### Install minikube

```bash
curl -LO https://storage.googleapis.com/minikube/releases/v1.22.0/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
##### Install minikubectl
```bash
curl -LO https://dl.k8s.io/release/v1.22.1/bin/linux/amd64/kubectl
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

##### minikube start
가상머신을 CPU 2개 이상, 메모리 4GB 이상으로 설정
```bash
minikube start --driver=docker
```
