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
