# FLY-AI

#0628
nginx: 가벼운 web server
docker에 올려서 사용

docker ps -a 
모든 container 확인

##### create docker file

```bash
touch Dockerfile
```
빈 file 생성
Dockerfile: 미리 작성된 명령어를 통해 표준형 container 생성

vi Dockerfile 
editor로 Dockerfile 작성

press i(INSERT MODE)

```bash
FROM ubuntu:18.04

RUN apt-get update

CMD ["echo", "Hello Docker"]
```

esc(exit INSERT MODE)
:wq  # (write, quit)

확인 시
cat Dockerfile

##### docker 말기
```bash
docker build -t my-image:v1.0.0 .

docker images | grep my
docker run my-image:v1.0.0

docker run -d -p 5000:5000 --name registry registry    # -d: background에서도 계속 run / -p: publish a container's port to the host, port number

docker tag my-image:v1.0.0 localhost:5000/my-image:v1.0.0
```

REPOSITORY localhost:5000/my-image와 my-image는 IMAGE ID가 같다.
```bash
docker push localhost:5000/my-image:v1.0.0
```
push 하면 registry 안에 쌓인다.
```bash
curl -X GET http://localhost:5000/v2/_catalog  # registry 안에 뭐가 있나
curl -X GET http://localhost:5000/v2/my-image/tags/list  # Docker image 정보
```
```bash
docker tag my-image:v1.0.0 yunoi/my-image:v1.0.0  # tag
docker push yunoi/my-image:v1.0.0  # hub.docker.com cloud상에 push
```
