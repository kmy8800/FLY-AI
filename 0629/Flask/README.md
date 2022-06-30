# Flask
## ML Serving
  - ML Serving: 다른 애플리케이션에서 ML model을 사용할 수 있도록 배포
  - Flask: 파이썬 기반 웹 프레임워크 중 하나. 가볍고, 확장성, 유연성이 뛰어남
  
### 1. Flask 설치
```bash
pip install -U Flask==2.0.2
```
  
### 2. Hello World! with Flask

#### 1) app.py 생성
```py
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "<p>Hello, World!</p>"

if __name__ == "__main__":
	app.run(debug=True, host='0.0.0.0', port=5000)
# debug 모드로 실행, 모든 IP 에서 접근 허용, 5000 포트로 사용하는 것을 의미
```

```bash
http://<IP-ADDRESS>:<PORT>

curl -X GET <IP-ADDRESS>:<PORT>
```

### 3. routing
- route() 데코레이터를 통해 python함수를 URl에 mapping

#### modify app.py
```py
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "<p>Hello, World!</p>"

@app.route("/helloai")
def hello_AI():
    return "<p>Hello, AI!</p>"

if __name__ == "__main__":
	app.run(debug=True, host='0.0.0.0', port=5000)
```

```bash
http://<IP-ADDRESS>:<PORT>
http://<IP-ADDRESS>:<PORT>/helloai

curl -X GET <IP-ADDRESS>:<PORT>
curl -X GET <IP-ADDRESS>:<PORT>/helloai
```

### 4. POST method
- route() 데코레이터는 URl 뿐만 아니라 HTTP METHOD 지정 가능하다  
- 원하는 대로 API를 만들 수 있다.

#### modify app.py
```py
from flask import Flask
import json

app = Flask(__name__)

@app.route("/predict", methods=["POST", "PUT"])
def inference():
    return json.dumps({'hello': 'world'}), 200 # http status code 를 200 으로 반환하는 것을 의미합니다.

if __name__ == "__main__":
	app.run(debug=True, host='0.0.0.0', port=5000)
```

```bash
curl -X POST 127.0.0.1:5000/predict
```

### 5. Predict API 구현
#### 1) 모델 학습 및 저장

##### ~/flask-tutorial/train.py
'''py
import os
import pickle

from sklearn.datasets import load_iris
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score, classification_report
from sklearn.model_selection import train_test_split

RANDOM_SEED = 1234

# STEP 1) data load
data = load_iris()

# STEP 2) data split
X = data['data']
y = data['target']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3,
                                                    random_state=RANDOM_SEED)

# STEP 3) train model
model = RandomForestClassifier(n_estimators=300, random_state=RANDOM_SEED)
model.fit(X_train, y_train)

# STEP 4) evaluate model
print(f"Accuracy :  {accuracy_score(y_test, model.predict(X_test))}")
print(classification_report(y_test, model.predict(X_test)))

# STEP 5) save model to ./build/model.pkl
os.makedirs("./build", exist_ok=True)
pickle.dump(model, open('./build/model.pkl', 'wb'))  # w: write, b: binary
```

```bash
python train.py


#Accuracy :  0.9555555555555556  
#              precision    recall  f1-score   support  
#
#           0       1.00      1.00      1.00        16  
#           1       0.94      0.94      0.94        17  
#           2       0.92      0.92      0.92        12  
#  
#    accuracy                           0.96        45  
#   macro avg       0.95      0.95      0.95        45  
#weighted avg       0.96      0.96      0.96        45  
```

#### 2) Flask Server 구현

##### ~/flask-tutorial/flask-server.py
```py
import pickle

import numpy as np
from flask import Flask, jsonify, request

# 지난 시간에 학습한 모델 파일을 불러옵니다.
model = pickle.load(open('./build/model.pkl', 'rb'))  # r: read, b: binary

# Flask Server 를 구현합니다.
app = Flask(__name__)


# POST /predict 라는 API 를 구현합니다.
@app.route('/predict', methods=['POST'])
def make_predict():
    # API Request Body 를 python dictionary object 로 변환합니다.
    request_body = request.get_json(force=True)

    # request body 를 model 의 형식에 맞게 변환합니다.
    X_test = [request_body['sepal_length'], request_body['sepal_width'],
              request_body['petal_length'], request_body['petal_width']]
    X_test = np.array(X_test)
    X_test = X_test.reshape(1, -1)

    # model 의 predict 함수를 호출하여, prediction 값을 구합니다.
    y_test = model.predict(X_test)

    # prediction 값을 json 화합니다.
    response_body = jsonify(result=y_test.tolist())

    # predict 결과를 담아 API Response Body 를 return 합니다.
    return response_body


if __name__ == '__main__':
    app.run(port=5000, debug=True)
```


#### 3) 
