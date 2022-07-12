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
