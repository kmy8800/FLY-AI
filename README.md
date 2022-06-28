# FLY-AI

0628
nginx: 가벼운 web server
docker에 올려서 사용

docker ps -a 
모든 container 확인

create docker file

touch Dockerfile
빈 file 생성
Dockerfile: 미리 작성된 명령어를 통해 표준형 container 생성

vi Dockerfile 
editor로 Dockerfile 작성

press i(INSERT MODE)

FROM ubuntu:18.04

RUN apt-get update

CMD ["echo", "Hello Docker"]

esc(exit INSERT MODE)
:wq(write, quit)

확인 시
cat Dockerfile
