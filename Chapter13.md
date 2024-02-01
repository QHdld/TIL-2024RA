# 13 CSV와 로그 관리

## csv
> 콤마(,)를 기준으로 나누어진 값
> 흔히 테이블 데이터라고 하는 엑셀 형태의 데이터를 덱스트 형대로 다루는 형식

```
이름, 성별, 키
데이콘, 남자, 180
홍길동, 남자, 175
아이유, 여자, 163
```
-> 한 줄의 데이터는 하나의 객체를 가리킴

## csv 파일 만들기
01. 엑셀에서 파일 형식을 'CSV'로 선택한 후 저장
02. 메모장 같은 덱스트 에디터로 내용을 확인할 수 있음

## csv 파일 다루기
01. 파일 객체 사용하기
02. csv 객체 사용하기
03. PANDAS 객체 사용하기

### 1) 파일 객체를 사용하여 데이터 다루기

```python
line_counter = 0
data_header = []
customer_list = []

with open("customer.csv") as customer_data: # csv파일을 "customer_data" 객체에 저장
     
    while 1:
        data = customer_data.readline()
        if not data:break
        if line_counter == 0: # 첫 번쨰 데이터는 데이터의 필드
            data_header = data.split(",")

        else:
            customer_list.append(data.split(","))

        line_counter += 1
    
print("Header:", data_header)
for i in range(0,10):
    print("Data",i,":",customer_list[i])
print(len(customer_list))
```

### 2) csv 객체를 사용하여 데이터 다루기
-> import와 read()사용
```python
import csv
f = open("./test.csv","r")
reader = csv.reader(
    f,                      # 연결할 대상 파일 객체
    delimiter=',',          # 데이터를 분리하는 기준
    quotecher='"',          # 데이터를 묶을 때 사용하는 문자 
    quoting=csv.QUOTE_ALL)  # 데이터를 묶는 기준
```

+ quoting(데이터를 묶는 기준)
01. QUOTE_ALL : 모든 데이터를 자료형에 상관없이 묶는다. 모든 데이터를 문자열형으로 처리한다.
02. QUOTE_MINIMAL : 최소한의 데이터만 묶는다.
03. QUOTE_NONNUMERIC : 숫자 데이터가 아닌 경우에만 묶는다. 이 경우 데이터를 읽어올 때 묶이지 않은 데이터는 csv객체에 의해 실수형으로 읽어오게 된다.
04. QUOTE_NONE : 데이터 묶는 작업을 하지 않는다.

## 로그 관리
> 행동 정보를 저장 = 로그 정보를 저장
> 로깅 : 로그를 관리하는 기법 / 프로그램이 실행되는 동안 일어나는 정보(행동 정보, 예외, 함수 사옹 시간~)를 기록으로 남기는 일

### 기본 로그 관리 모듈 : logging

로깅 레벨

#### 1단계 : DEBUG
개발 시점에 프로그램이 문제없이 실행되는지 확인하기 위해 출력하는 결과

#### 2단계 : INFO
기본적으로 사용자에게 실행 결과를 알려주는 로그 정보

#### 3단계 : WARNING
문제가 될 수 있는 상황을 기록하는 것

#### 4,5 단계 : ERROR, CRITICAL
에러가 발생하거나, 프로그램이 더이상 수행하기 어려울 때 발생

-> 파이썬에서 로깅을 사용하기 위해서는 Logger 객체를 활용해야한다

```python
import logging

logger = logging.getLogger("main") # Logger 선언
stream_hander = logging.StreamHandler() # Logger의 출력 방법 선언
logger.addHandler(stream_hander) # Logger의 출력 등록

logger.setLevel(logging.DEBUG) # 어느 레벨을 사용해 출력할 것인가를 지정하는 코드
logger.debug("틀림")
logger.info("확인")
logger.warning("주의")
logger.error("에러")
logger.critical("망함")
```

## 설정 저장

### 01. configparser 모듈
> 프로그램의 실행 설정값을 어떤 특정 파일에 저장하여 사용하는 방식
> 딕셔더리와 비슷하게 설정 파일 안에 키와 값을 넣고 이를 호출하여 사용

```python
import configparser
config = configparser.ConfigParser()
config.section()

config.read('example.cfg') # 특정 파일 안에 있는 설정 정보 읽어오기
config.section() # 해당 파일의 section 정보 읽어오기
for key in config('SectionOne') # SectionOne에 있는 key 출력
```

### argparse 모듈
> configparser 모듈과 달리 저장된 파일을 사용하는 것이 아니라 프로그램을 콘솔 창에서 실행할 때 설정하는 방식

- 거의 모든 콘솔 프로그램은 실행 시점에서 설정할 수 있는 기능을 제공함
- 일반적으로 실행 시점의 설정 파일을 커맨드 - 라인 옵션이라고 함

```python
import argparse

parser = argparse.ArgumentParser(description='Sum two integers.') # 기본 설정 도움말

parser.add_argument('-a', "--a_value", dest="a", help="A integers", type = int) # 인수 추가

parser.add_argument('-b', "--b_value", dest="b", help="B integers", type = int)

args = parser.parse_args() # 입력된 커멘드-라인 인수 파싱

print(args) # >> Namespace(a=5,b=3) : 값이 저장된 형태는 "Namespace" 객체
print(args.a)
print(args.b)
print(args.a + args.b)
```