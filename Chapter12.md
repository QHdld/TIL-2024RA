# 12 예외 처리와 파일 다루기

## 예외의 개념과 사례
예외 : 프로그램을 실제로 작성하고 실행하다 예상하지 못한 일이 발생하는 것

+ 예측 가능한 예외
> 개발자가 발생여부를 사전에 인지할 수 있는 예외, 쉽게 대응 가능

+ 예측 불가능한 예외
> ex) 매우 많은 파일을 처리할 때 빈 파일이 있는 경우

### 예외 처리 구문
> 예외 처리 : 프로그램의 완성도를 높이는 차원에서 중요

01. try - except문
```python
try:
    예외 발생 가능 코드
except 예외 타입:
    예외 발생 시 실행되는 코드
```

02. try - except - else문
<br>해당 예외가 발생하지 않는 경우 수행할 코드를 else에 작성
```python
try:
    예외 발생 가능 코드
except 예외 타입:
    예외 발생 시 실행되는 코드
else:
    예외가 발생하지 않을 때 실행되는 코드
```

03. try - except - finally문
<br> finally문은 수행 코드가 아무런 문제가 없이 종료되었을 경우 최종으로 호출하는 코드

```python
try:
    예외 발생 가능 코드
except 예외 타입:
    예외 발생 시 실행되는 코드
finally:
    예외 발생 여부와 상관없이 실행되는 코드
```

04. raise문
<br>필요할 때 예외를 발생시키는 코드<br>
```raise 예외 타입(예외 정보)```

```python
for digit in value:
    if digit not in "309228":
        raise ValueError("숫자값을 입력하지 않았습니다.")
```

05. assert문
<br>미리 알아야 할 예외 정보가 조건을 만족하지 않을 경우 예외를 발생시킴
<br>True 또는 False의 반환이 가능한 함수를 사용
<br>```assert 예외 조건```
```python
def get_binary_number(decimal_number):
    assert isinstance(decimal_number, int) # -> False 반환
    return bin(decimal_number)
print(get_binary_number(10))
print(get_binary_number("10))
```

## 파일 다루기
### 파일과 디렉터리
> 파일 : 컴퓨터에서 논리적으로 정보를 저장하는 가장 작은 단위<br>
디렉터리 : 파일을 담는 또 하나의 파일, 여러 파일을 포함할 수 있는 그릇

### 파일의 종류
+ 바이너리 파일 : 컴퓨터만 이해할 수 있는 이진 정보로 저장된 파일(ex 엑셀, 워드)

+ 텍스트 파일 : 사람이 이해할 수 있는 문자열로 저장된 파일 -> 메모장으로 내용 확인 가능
<br>** 텍스트 파일도 사실 컴퓨터가 이해할 수 있는 형태로 변경하여 저장된다.
--> 변경하는 기준을 보통 아스키코드, 유니코드로 하고 변환한다.

### 파일 읽기
텍스트 파일을 다루기 위해 ```open()```함수를 사용
```python
f = open("파일명","파일 열기 모드")
f.close()
```

+ 파일 열기 모드<br>

|종류|설명|
|---|-----|
|  r  |읽기 모드: 파일을 읽기만 할 때 사용|
|  w  |쓰기 모드: 파일에 내용을 쓸 때 사용|
|  a  |추가 모드: 파일의 마지막에 새로운 내용을 추가할 때 사용|

+ 파일 읽기<br>
with문과 함께 open() 함수를 사용할 수 있다
<br>- <b>with문</b>은 들여쓰기를 하는 동안에는 open()함수가 유지되고, 들여쓰기가 끝나면 open() 함수도 종료되는 방식이다.
➕ 자원을 획득하고, 사용하고, 반납할때 주로 사용한다.
예를들어 파일을 여는 경우, 다른 프로세스를 위해 사용한 뒤에 닫아주어야 한다. 
또는 DB 세션을 사용하는 경우, 다른 프로세스를 위해 반납해야 한다.<br>
-as문을 사용하여 변수명에 할당한다. (with as는 세트)

```python
with open("dream.txt","r") as my_file:
    contents = my_file.read()
    print(type(contents),contents)
```

### 한 줄씩 읽어 리스트형으로 반환하기
```readlines()```함수 사용<br>
```python
with open("dream.txt","r") as my_file:
    content_list = my_file.readlines()
```

### 파일 쓰기
> 파일에 무엇인가를 쓰기 위해서는 파일 열기 모드를 'w'로 설정하는 것과 함께 인코딩이라는 개념을 알아야함

> 인코딩 : 텍스트 파일을 저장하기 위해서는 저잘할 때 사용하는 표준을 지정해야함 (ex: uf8, cp949)

```f = open("count_log.txt", "w", encoding = "utf8")```

### 파일 열기 모드 a로 새로운 글 추가하기
> 쓰기 모드 w는 늘 새로운 파일을 생성한다. -> a모드로 파일을 열면 해당 파일에 계속 추가된다.

```python
with open("count_log.txt", 'a', encoding = "utf8") as f :
    for i in range(1,11):
        data = "%d번째 줄이다.\n"%i
        f.write(data)
```

### 디렉터리 만들기
os 모듈 사용하기

-디렉터리 생성 코드 
```python
import os
os.mkdir("log")
```

-디렉터리 유무 확인 코드
```python
import os
os.mkdir("log")

if not os.path.isdir("log"):
    os.mkdir("log")
```

### 로그 파일
<b>로그 파일 : 여러 가지 중간 기록을 저장하는 역할을 하는 파일</b> <br>
프로그램내에서 발생하는 이벤트나, 처리내용, 소프트웨어간 통신 메세지, 에러내용 등을 기록해 두었다가 확인 하는 용도

### pickle 모듈
파이썬 프로그램을 실행할 때 생성되는 여러 변수와 객체는 순간적으로 메모리에 로딩되었다가 프로그램이 종료되면 사라진다. <br>-> 사용되는 객체를 저장시켜 놓고 필요할 때 다시 불러야 하는 경우 (영속화)
<br>
> --> pickle모듈은 메모리에 로딩된 객체를 영속화 할 수 있도록 지원한다.

```python
import pickle

f = open("list.pickle", "wb")
test = [1,2,3,4,5]
pickle.dump(test,f)
f.close()
```

 01. 파일을 생성할 때에는 'w'가 아닌 'wb'(b: 바이너리)로 열어야한다 -> 텍스트 파일이 아닌 바이너리 파일로 저장한다는 의미
 02. dump() 함수에서는 저장할 객체, 저장될 파일 객체를 차례대로 인수로 넣으면 객체가 해당 파일에 저장된다.
 03. 저장된 pickle파일을 불러오는 프로세스도 저장 프로세스와 같다.
 -> list.pickle 파일을 'rb'모드로 읽어온 후 'load' 함수로 불러오면 된다.