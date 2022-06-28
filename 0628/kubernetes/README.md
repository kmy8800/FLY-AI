# Kubernetes

Kubernetes Master는 Worker Node(server) 중 load가 적은 Node에 일을 부여하는 매니저 역할

Container -> Pod -> Worker Node  
Micro Service Architecture(MSA): 각각의 Container는 기능적인 단위(Service Component)로  
개별적인 업데이트가 가능함

### Install minikube

```bash
curl -LO https://storage.googleapis.com/minikube/releases/v1.22.0/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
### Install minikubectl
```bash
curl -LO https://dl.k8s.io/release/v1.22.1/bin/linux/amd64/kubectl
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

### minikube start
가상머신을 CPU 2개 이상, 메모리 4GB 이상으로 설정
```bash
minikube start --driver=docker
```

```bash
kubectl get pod -n kube-system
```

#### result
NAME                               READY   STATUS    RESTARTS   AGE
coredns-558bd4d5db-2wvtq           1/1     Running   0          8m11s
etcd-minikube                      1/1     Running   0          8m18s
kube-apiserver-minikube            1/1     Running   0          8m18s
kube-controller-manager-minikube   1/1     Running   0          8m18s
kube-proxy-4svhr                   1/1     Running   0          8m11s
kube-scheduler-minikube            1/1     Running   0          8m18s
storage-provisioner                1/1     Running   1          8m23s


Kubernetes에 올라가는 pod, container 등에 대한 정보를 yaml파일로 작성

##### pod.yaml

```bash
apiVersion: v1 # kubernetes resource 의 API Version
kind: Pod # kubernetes resource name
metadata: # 메타데이터 : name, namespace, labels, annotations 등을 포함
  name: counter
spec: # 메인 파트 : resource 의 desired state 를 명시
  containers:
  - name: count # container 의 이름
    image: busybox # container 의 image
    args: [/bin/sh, -c, 'i=0; while true; do echo "$i: $(date)"; i=$((i+1)); sleep 1; done'] # 해당 image 의 entrypoint 의 args 로 입력하고 싶은 부분
```

```bash
kubectl apply -f pod.yaml
```

ImagePullBackoff Error 발생
: Image busybox를 찾을 수 없어 에러 발생

##### 해결방법
docker login & login정보를 kubectl에 저장
```bash
docker login
docker pull busybox
```
```bash
kubectl create secret generic regcred  --from-file=.dockerconfigjson=$HOME/.docker/config.json  --type=kubernetes.io/dockerconfigjson
```

pod.yaml 수정
```bash
apiVersion: v1
kind: Pod
metadata:
  name: counter
spec:
  containers:
    - name: count
      image: busybox
      args: [/bin/sh, -c, 'i=0; while true; do echo "$i: $(date)"; i=$((i+1)); sleep 1; done']
  imagePullSecrets:
    - name: regcred
```

```bash
kubectl apply -f pod.yaml
```

