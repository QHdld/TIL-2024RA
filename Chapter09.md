# 09 파이썬 스타일 코드 2

## 람다 함수
> 함수의 이름 없이 함수처럼 사용할 수 있는 익명의 함수를 말한다

```
f = lambda x,y : x + y
print(f(1,4))

--> 5
```

```
print((lambda x: x + 1)(5))
```

## 맵리듀스

### 01 map() 함수
> 연속 데이터를 저장하는 시퀀스 자료형에서 요소마다 같은 기능을 적용할 때 주로 사용한다.

```
ex = [1,2,3,4,5]
f = lambda x : x**2
print(list(map(f,ex)))

--> [1,4,9,16,25]
```

map(f,ex) ==> '해당 코드로 함수 f를 ex의 각 요소에 맵핑하라'

+ 제너레이터의 사용
<br>
map(f,ex) : X
<br>
list(map(f,ex)) : O
<br>
--> 시퀀스 자료형의 데이터를 처리할 떄 실행 시점의 값을 생성하여 효율적으로 메모리를 관리할 수 있다는 장점 
<br>
<br>
+ ➕ 제너레이터란?<br>
> 제너레이터는 발전기라는 의미처럼 이 객체를 호출할 때마다 yeild가 작동되 값을 순차적으로 산출
<br>
제너레이터를 통해 이터레이터를 생성하면 다음 순서를 기억한 상태로 객체가 생성되고, 호출하기 전에는 모든 값을 메모리에 올리지 않는다. 즉, yield를 호출해 generator를 가동시킴으로써 값을 산출하고 그만큼의 메모리를 사용.
<br>
이를 지연 평가(lazy evaluation) 방식이라 한다.
<br>

+ 한 개 이상의 시퀀스 자료형 데이터의 처리
<br><b>zip()</b> : 2개의 시퀀스 자료형 데이터에서 같은 위치에 있는 값끼리 대응시킴
```
ex = [1,2,3,4,5]
f = lambda x,y : x+y
list(map(f,ex,ex))

--> [2,4,6,8,10]
```

```
[x + y for x,y in zip(ex,ex)]

--> [2,4,6,8,10]
```

+ 필터링 기능
: 리스트 컴프리헨션과 달리 else 문을 반드시 작성해 해당 경우가 존재하지 않는 경우를 지정해주어야 한다.

```
list(map(lambda x: x**2 if x % 2 == 0 else x, ex))

--> [1,4,3,16,5]
```

```
[x ** 2 if x % 2 == 0 else x for x in ex]

--> [1,4,3,16,5]
```

### 02 reduce() 함수
> 리스트와 같은 시퀀스 자료형에 차례대로 함수를 적용한 다음 모든 값을 통합시켜 주는 함수

```
from functools import reduce
print(reduce(lambda x,y : x+y, [1,2,3,4,5]))

--> 15
```

```
x = 0
for y in [1,2,3,4,5]:
    x += y
print(x)

--> 15
```

## 별표의 활용
> 함수의 가변 인수를 사용할 때 변수명 앞에 별표를 붙인다

```
def asterisk_test(a, *args):
    print(a,args)
    print(type(args))

asterisk_test(1,2,3,4,5,6)

--> 1 (2,3,4,5,6)
    <class 'tuple'>
```
--> 별표는 여러 개의 변수를 담는 컨테이너로서 속성을 부여받았다

+ 별표의 언패킹 기능
> 별표는 컨테이너 역할 이외에 언패킹하는 기능도 가진다

```
def asterisk_test(a,args):
    print(a,*args)
    print(type(args))

asterisk_test(1,(2,3,4,5,6))

--> 1 2 3 4 5 6
    <class 'tuple>
```

## 선형대수학
+ 수학적 정의
<br>
벡터 : 크키과 방향을 모두 가지는 것 
<br>
스칼라 : 크기만 가지는 것
<br>
행렬 : 벡터 모임, 행 또는 열이 하나의 대상에 대한 정보를 표현한 것의 모음
<br>
* 컴퓨터 공학에서의 정의<br>
: 리스트와 여러 개의 데이터를 하나의 정보로 표현한다는 관점에서 비슷

#### 파이썬 스타일 코드로 표현한 벡터

```
vecter_a = [1,2,10] # 리스트
vecter_b = (1,2,10) # 튜플
vecter_c = {'x':1,'y':1,'z':10} # 딕셔너리
```

* 스칼라 - 벡터 연산
```
u = [1,2,3]
v = [4,4,4] # 벡터
alpha = 2 # 스칼라

result = [alpha * sum(t) for t in zip(u,v)]
result

--> [10,12,14]
```

* 파이썬 스타일 코드로 표현한 행렬
```
matrix_a = [[3,6],[4,5]] # 리스트
matrix_b = [(3,6),(4,5)] # 튜플
matrix_c = {(0,0):3, (0,1):6,(1,0):4, (1,1):5} # 딕셔너리
```

+ 행열의 동치
<br>
```
matrix_a = [[1,1],[1,1]]
matrix_b = [[1,1],[1,1]]
all([row[0] == value for t in zip(matrix_a, matrix_b) for row in zip(*t) for value in row])

--> True
```

++ all(), any() --> and, or과 비슷

+ 전치 행열
```
matrix_a = [[1,2,3],[4,5,6]]
result = [[element for element in t] for t in zip(*matrix_a)]
result

--> [[1,4],[2,5],[3,6]]
```
++ ``` for t in zip(*matrix_a)``` -> 별표가 리스트를 언패킹 해준다
