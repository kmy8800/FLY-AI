
### 가상환경

```bash
conda create -n myml python=3.8

conda activate myml

pip install ipykernel

python -m ipykernel install --user --name myml --display-name "myml"

jupyther lab
```

### Numpy

```py
import numpy as np

a = np.zeros((5, ))  # (5, ): shape, tuple input

np.linspace(0, 10, 8) # 8등분

np.zeros_like(arr)

np.random.normal()
np.random.randn()

x * y  # 요소 곱
x @ y  # 행렬 곱

np.multiply(x, y): 요소 곱
np.matmul(x, y): 행렬 곱

np.dot(x, y)  # 1차원 벡터일 때는 내적, 2차원 이상에서는 행렬 곱

x[x>2] = -1  # 조건에 맞는 인덱스에 값 설정

np.concatenate((x, y), axis)

np.vstack((x,y))
np.hstack((x,y))

np.where(x>3, x, 0)  # filter

np.argmax(x, axis=1)  # max index

x = [0, 1, 2, 3, 4]
y = x[:2]  # y = [0, 1]
y[0] = -1  # y = [-1, 1]
-> x = [-1, 1, 2, 3, 4]             # reference의 값이 바뀜,  y = x.copy()로 값 복사

np.getfromtxt('./Iris.txt', delimeter=',', skip_header=True)

np.savez('data.npz', x=x, y=y)

data = np.load('data.npz')
x = data['x']
y = data['y']
```
