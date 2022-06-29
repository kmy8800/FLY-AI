# MLflow
- ML Management
  - model source code
  - Evaluation Metric 결과
  - parameters
  - Model.pkl 파일
  - 학습 data
  - 데이터 전처리 코드
  - 전처리된 데이터
  - ...
  
- MLflow
![im](https://helloailab.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fe2542765-f453-4878-8077-9109e8a5e394%2FUntitled.png?table=block&id=f7147728-76e4-4f20-bf4d-35806d394944&spaceId=671307dc-84e2-4a4c-8ff5-ade4dd0d922d&width=1920&userId=&cache=v2)
![im](https://helloailab.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fdaef255f-7972-4e35-8c8c-e5b4bd963e77%2FUntitled.png?table=block&id=68fdaffe-b149-4dfa-b8ca-d94b4b324f14&spaceId=671307dc-84e2-4a4c-8ff5-ade4dd0d922d&width=1860&userId=&cache=v2)

## 1. MLflow 설치
- anaconda 설치(MLflow models serve시 필요)
https://velog.io/@boom109/Anaconda-%EC%84%A4%EC%B9%98-on-Ubuntu-20.04-LTS
- python3.6이상
```bash
mkdir mlflow-tutorial
cd mlflow-tutorial

python -V

pip install mlflow==1.20.2

mlflow --version
# mlflow, version 1.20.2
```
