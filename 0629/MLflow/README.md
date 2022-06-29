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

pip install protobuf==3.20.0   # package종속

mlflow --version
# mlflow, version 1.20.2
```
## 2. MLflow ui
Microsoft Azure와 같은 cloud 환경에서 할 경우, 네트워킹 포트(여기선 5000)를 열어야함  
Microsoft Azure -> 네트워킹 -> 인바운드 포트 규칙 추가, 아웃바운드 포트규칙 추가

```bash
# local 환경
~/mlflow-tutorial$ mlflow ui -p <PORT-NUMBER> # http://localhost:5000 에서 MLflow ui 확인 가능 default port num:5000

# cloud 환경
~/mlflow-tutorial$ mlflow ui -h 0.0.0.0 -p <PORT-NUMBER> # 외부에서 접속 허용
```
mlflow ui 실행시, 해당 디렉토리에 mlruns/0/meta.yaml 파일 생성

## 3. MLflow Example

```bash
~/mlflow-tutorial$ wget https://raw.githubusercontent.com/mlflow/mlflow/master/examples/sklearn_elasticnet_diabetes/linux/train_diabetes.py

python train_diabetes.py
python train_diabetes.py  0.01 0.01   # parameter를 바꿔가며 실험
python train_diabetes.py  0.01 0.75
python train_diabetes.py  0.01 1.0
python train_diabetes.py  0.05 1.0
python train_diabetes.py  0.05 0.01
python train_diabetes.py  0.5 0.8
python train_diabetes.py  0.8 1.0
```
