# Python

### library, package, module, function
- package: 
  - multiple modules
- module: 
  - \__name__ = "\__main__"
  - a function or multiple functions in .py file
- function
  - def function(args):  
        statements  
        return value
  - name: 동사 or 동사_명사 

### comment 주석
- writer, revised date
- function, parameter
- license


### function
```py
def print_sum(*nums, subft) # 가변적인 개수의 variable
  sum = 0
  for n in nums:
    sum += n
  
  print(subft%sum)
  return
  
if __name__="__main__"
  print_sum(1,2,3,4, subft="sum = %d")
```

#### map
```py
lst = [1, 2, 3, 4, 5]

def square(n):
  return n*n
 
lst2 = list(map(square, lst))
```

```py
lst = [1, 2, 3, 4, 5]

lst2 = list(map(lambda x: x*x, lst))  # lambda input:output   : temporary function
```
#### filter: True or False
```py
lst = [1, 2, 3, 4, 5]

def less3(n):
  if n < 3:
    return True
  else:
    return False

lst2 = list(filter(less3, lst))
```

```py
lst = [1, 2, 3, 4 ,5]

lst2 = list(filter(lambda x: x < 3, lst))
```

#### Recursive function 재귀함수
```py
def recursive(n)
  return recursive(n-1) * n
```


### Obejct Oriented Programming

- 객체(Object): 객체란 어떤 속성(static property)과 행동(behavior property)을 가지고 있는 데이터
- 추상화(Abstraction): 내용은 감춘 상태로 사용할 수 있다.(Hidden)
- Class: 객체를 만들기 위한 설계도, 틀
  - self: 현재 object
  - 생성자(): \__init__
  ```py
  def __init__(self, value):
    self.value = value
  ```
  - 소멸자(): \__del__ (거의 안씀)

- specialization: 큰 범주 -> 작은 범주
- generalization: 작은 범주 -> 큰 범주
- 상속: 객체의 속성을 general class(super class) -> special class(sub class) 로 상속하고 새로운 속성을 추가(specialization)
  ```py
  class subclass(super class):
    super.__init__(self, value)
    def __init__(self, value)
      self.value = value
  ```
  
### User Interface Programming

#### TKinter
- window, box, button 등 모든 것이 widget(object)
```py
import tkinter as tk

root = tk.Tk()  # 생성자, top-level-window 생성

w = tk.Label(root, text="Hello Tkinter!")
w.pack()

root.mainloop()
```

- label
- button: Click event handler
- checkbox: true(1) false(0)
- entry: text input
- canvas: drawing
- sliders
- text widgets


### Flask
- WSGI(Web Server Gateway Interface: 웹 서버와 웹 어플리케이션 사의 범용 인터페이스를 위한 규격
- Jinja2: python 템플릿 엔진

#### 
```py
app = Flask(__name__)  # Flask instance 생성

@app.route('/)  # route(): decorator는 URL을 함수에 바인딩하는 데 사용
def hello_world():
  return 'Hello World'

def index():
  return render_template('... .html')  # templates folder 내의 .html 파일을 렌더링

if __name__ == '__main__':
  app.run()            # app.run을 통해 Flask 어플리케이션 실행
  
```

#### Sending Form
```py
from flask import Flask, render_template, request
app = Flask(__name__)

@app.route('/')
def student():
   return render_template('student.html')

@app.route('/result',methods = ['POST', 'GET'])
def result():
   if request.method == 'POST':
      result = request.form
      return render_template("result.html",result = result)

if __name__ == '__main__':
   app.run(debug = True)
```
