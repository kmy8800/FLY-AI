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
    def \__init__(self, value)
      self.value = value
  ```
  
### User Interface Programming

- 
  
  



