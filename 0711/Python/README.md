
# Python
- Compiler approach programming: natural machine self-execution  ex) C programming
  - .exe file contain all resource ( static binding )
- Interpreter approach programming: virtual machine execute program  ex) bash, shell, python
  - call resources when .exe is executed  ( dynamic binding )


- Identifier(변수, 함수이름) 짓는 방법

### 자료형
- 군집자료형
  - 나열형
    - str (immutable) ""
    - list []: sequence elements, 각 element의 data type이 달라도 상관없음(<-> array)
    - tuple (immutable) (): sequence elements, element 수정불가
  - set {}: 중복x
  - dict {}: key:value
* immutable: 값을 변경할 수 없음


### 문자열
- sequential, immutable

- \*object : object가 가리키는 object

### list


#### Insert list element 
- a = \[0, 1, 2, 3, 4]
- a\[1:1] = \['a', 'b']
- -> a = \[0, 'a', 'b', 1, ,2, 3, 4]

- a\[1:1] = \[\['a', 'b']]
- -> a = \[0, \['a', 'b'], 'a', 'b', 1, 2, 3, 4]

#### Copy
- a = \[0, 1, 2, 3, 4]
- b = a\[:]
- c = a
- a\[0] = 10

-> a = \[10, 1, 2, 3, 4]
-> b = \[0, 1, 2, 3, 4]  // Shallow Copy
-> c = \[10, 1, 2, 3, 4]  // Deep Copy: reference(id) 복사

#### Method
- list.method(): behavior properties (copy, count, insert, pop, remove, sort, ...)
- list.sort: list changed
- sorted(list): list not changed
- list.copy(): 새로운 list를 만들어 값 저장, shallow copy ( b = a\[:]와 동일)
- 
