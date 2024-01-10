# 05 함수

## 함수 기초
함수 : 어떤 일을 수행하는 코드의 덩어리

#### 장점 

     1. 필요할 때 마다 호출 가능
     2. 논리적인 단위로 분할 가능
     3. 코드의 캡슐화

#### 함수 선언 방법

     1. def - 함수의 정의를 시작한다는 의미
     2. 함수 이름 - 소문자, 띄어쓰기 대신 _, 동사와 명사 사용, 짧고 명료한 이름이 일반적
     3. 매개변수 - 입력값으로 사용하는 변수
     4. 명령문 - 일반적인 코드, 들여쓰기 필요

#### ➕매개변수와 인수 
``` 
def f(x):
return 2*x+7

print(f(2))
```
-> f(x)에서 x가 매개변수
<br>
-> f(2)에서 2가 인수

#### 함수의 형태
```
def a_rectangle_area(): # 매개변수 x, 반환값 o
     print(5 * 7)
def b_rectangle_area(x,y): # 매개변수 o, 반환값 x
     print(x * y)
def c_rectangle_area(): # 매개변수 x, 반환값 o
     return(5*7)
def d_rectangle_area(x,y): # 매개변수 o, 반환값 x
     return(x * y)

a_rectangle_area()
b_rectangle_area()
print(c_rectangle_area())
print(d_rectangle_area())
```

## 함수 심화
#### 함수의 호출 방식
``` 
def spam(eggs):
     eggs.append(1) # 기존 객체의 주소값에 [1]추가
     eggs = [2,3] # 새로운 객체 생성

ham = [0] 
spam(ham)
print(ham)

-> [0,1]
```

#### 변수의 사용 범위
* 지역 변수 : 함수 내부에서만 사용
* 전역 변수 : 프로그램 전체에서 사용

```
def f():
     s = " I love London!"
     print(s)

s = " I love Paris!"
f()
print(s)

-> I love London!
-> I love Paris!
```
```
def f(): 
     global s
     s = " I love London!"
     print(s)

s = " I love Paris!"
f()
print(s)

-> I love London!
-> I love London!
```

## 함수의 인수
#### 1. 키워드 인수 
> 함수에 입력되는 매개변수의 변수명을 사용하여 함수의 인수를 지정하는 방법

#### 2. 디폴트 인수 
> 매개변수에 기본값을 지정하여 사용하고, 아무런 값도 인수로 넘어가지 않을 때 지정된 기본값을 사용하는 방식
```
def print_something_2(my_name, your_name = "TEAMLAB"):
     print("Hello {0} + My name is {1}.format(your_name, my_name))

print_something_2("Choi", "Teamlab")
print_something_2("Choi")

-> Hello Teamlab, My name is Choi
-> Hello Teamlab, My name is Choi
```
#### 3. 가변 인수
> *로 표현 가능
-> *는 일반적인 키워드 인수에 대한 선언이 모두 끝난 후 마지막에 선언되어야 한다. 또한 리스트와 비슷한 튜플 형태의 함수 안에서 사용되어지므로 인덱스를 사용

+ 튜플: ()로 묶여 출력되는 자료형
```
def asterisk_test_2(*args):
     x,y,*z = args
     return x,y,z

print(asterisk_test_2(3,4,5))

-> (3,4,[5])
```
#### 4. 키워드 가변 인수
> 변수의 이름을 저장할 수 없다는 가변 인수의 단점을 보안한 것


-> **로 표현
<br>
-> 딕셔너리 자료형과 비슷 
<br>
-> 반드시 모든 매개변수(가변 인수) 다음에 선언되어야 함

## 좋은 코드를 작성하는 방법
#### 코딩 규칙 
1. 들여스기는 4 스페이스
2. 한 줄은 최대 79자까지
3. 불필요한 공백은 없애기

➕ 규칙
1. = 연산자는 1칸 이상 띄우지 않는다
2. 주석은 항상 갱신하고 불필요한 주석은 삭제한다
3. 소문자 l, 대문자 O, 대문자 I는 사용을 금한다.

➕ 함수 개발 가이드라인
1. 함수 내용은 가능하면 짧게, 역할과 의도를 명확히 드러낼 것
2. 함수의 역할은 한 가지 역할을 명확히 해야한다
3. 함수를 만들어야 하는 경우 : 공통으로 사용되는 코드를 함수로 변환, 복잡한 로직이 사용되었을 떄 식별 가능한 이름의 함수로 변환