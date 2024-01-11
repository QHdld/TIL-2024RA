# 06 문자열 

## 문자열의 이해
> 문자열 : 리스트와 같이 데이터를 순차적으로 메모리에 저잘하는 형식의 데이터인 시퀀스 자료형이다.

#### 문자열과 메모리 공간
일반적으로 문자열을 저장하기 위해서는 영문자 한 글자당 1바이트의 메모리 공간을 사용
<br>
-> 이러한 문자를 처리하기 위해 이진수로 변환되는 표준규칙을 만듦 (<b>인코딩</b>)
<br>
➕ 대표적인 규칙 : ASCII, UTF-8 ... 

#### 문자열의 인덱싱
문자열은 글자 하나하나가 상대적인 주소를 가져 인덱싱을 사용할 수 있다. 

#### 문자열의 슬라이싱
슬라이싱 : 문자열의 주소값을 이용해 문자열의 부분값을 추출해내는 기법
```a[:]```, ```a[::2]```, ```a[::-1]```

#### 문자열의 연산 
* 덧셈으로 변수 연결 가능
* 곱하기고 반복 연산 가능
* ```A in a``` A가 a에 포함되었는지 확인

#### 문자열 함수
|함수명|기능|
|---|---|
|len()|문자열의 문자 개수를 반환|
|upper()|대문자로 편환|
|lower()|소문자로 변환|
|title()|각 단어의 앞글자만 대문자로 변환|
|capitalize()|첫 문자를 대문자로 변환|
|count('찾을 문자열')|'찾을 문자열'이 몇 개 들어있는지 개수 반환|
|find('찾을 문자열')|'찾을 문자열'이 왼쪽 끝부터 시작하여 몇번째에 있는지 반환|
|rfind('찾을 문자열')|'찾을 문자열'이 오른쪽 끝부터 시작하여 몇 번째에 있는지 반환|
|startswith('찾을 문자열')|'찾을 문자열'로 시작하는지 여부 반환|
|endswith('찾을 문자열')|'찾을 문자열'로 끝나는지 여부 반환|
|strip()|좌우 공백 삭제|
|rstrip()|오른쪽 공백 삭제|
|lstrip()|왼쪽 공백 삭제|
|split()|문자열을 공백이나 다른 문자로 나누어 리스트로 반환|
|isdigit()|문자열이 숫자인지 여부 반환|
|islower()|문자열이 소문자인지 여부 반환|
|isupper()|문자열이 대문자인지 여부 반환|

## 문자열 서식 지정
#### 1. % 서식
> %자료형 %값

```print("I eat %d apples."%3)```
|서식|설명|
|---|---|
|%s|문자열|
|%c|문자 1개|
|%d|정수|
|%f|실수|
|%o|8진수|
|%x|16진수|
|%%|문자 % 자체|

#### format() 함수
> "{자료형}".format(인수)

```print("I'm {0} years old.".format(20))```

#### 패딩
> 여유 공간을 지정하여 글자 배열을 맞추고 수소점 자릿수를 맞추는 기능

##### 1. % 서식의 패딩

``` print("%10d" %12)```(좌측 정렬시 - 붙이기)

➕소수점 자릿수 지정
```print("%10.3f" %5.94343)```->     5.943

##### 2. format() 함수의 패딩
```print("{0:>10s}".format("Apple"))```

➕소수점 자릿수 지정
```"{1:>10.5f}".format("Apple", 5.243)```->'   5.2400'

➕➕ 네이밍
``` 
print("Product: %(name)5s, Price per unit: %(price)5.5f."%{"name":"Apple", "price":5.243})
```