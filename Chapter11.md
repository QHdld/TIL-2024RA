# 11 모듈과 패키지

## 모듈과 패키지의 이해

> 모듈 : 이미 작성된 프로그램

> 패키지 : 이 프로그램의 묶음, 모듈의 묶음

### 모듈의 개념
+ 프로그래밍에서의 모듈<br>
: 작은 프로그램 조각 (레고 블록 하나하나)

-> 각 모듈은 저마다 역할이 있어서 서로 다른 모듈과 인터페이스만 연결되면 사용할 수 있다

+ 인터페이스<br>
: 함수에서 매개변수를 입력하는 약속<br>
해당 모듈을 사용하기 위해서는 모듈 간의 연결을 위한 약속이 필요한데 이것을 인터페이스라 한다.

+ 모듈을 호출하기 위한 코드<br>
```import 모듈```

### 패키지의 개념
: 하나의 패키지 안에 여러 개의 모듈이 있는데, 이 모듈들이 서로 포함 관계를 가지며 거대한 패키지를 만든다

+ 호출하기 위한 코드<br>
```from 패키지```

## 모듈 만들기

> .py 파일 자체가 모듈이다

### 모듈 만드는 방법
01. 코드를 작성하여 .py 파일로 저장<br>
02. 클라이언트 코드(해당 모듈을 사용하는 코드)에서 import해 사용
03. 함수를 가져다 사용하기 위해서는 ```fahrenheit = fah_converter.convert_c_to_f(celsius)``` 형식으로 작성

** 호출받는 모듈과 호출해서 사용하는 클라이언트 프로그램이 같은 디렉터리 안에 있어야한다.

### 네임스페이스

> 모듈 호출의 범위를 지정하는 것

> 클라이언트 프로그램의 함수 이름과 호출된 모듈의 함수 이름이 같은 경우 <br> ->모듈의 사용 범위를 명확히 지정해야한다 <br>-> 네임 스페이스 사용

01. 알리아스 생성<br>
 알리아스 : 일종의 별칭으로 모듈의 이름을 바꿔 부를 때 사용
 ```import fah_converter as fah```

02. from 구문을 사용해 특정 함수, 클래스만 호출하는 방법
 ```from fah_converter import covert_c_to_f```
 <br> from : 중첩 구조를 호출하는 역할

03. '*(별표)' 사용
 <br>'*(별표)' : 모든 것이라는 뜻
 <br>-> 해당 모듈 안에 있는 모든 사용 가능한 리소스를 호출한다는 뜻

### 내장 모듈의 사용

> 파이썬이 개발하기 위해 기본적으로 사용해야하는 모듈을 제공, 별다른 조치없이 import문으로 사용 가능

01. random 모듈 : 난수 생성 모듈
02. time 모듈 : 시간을 변경하거나 현재 시각을 알려준다
03. urlib 모듈 : 웹 주소의 정보를 불러온다 (request 모듈)

### 패키지 구성
> 패키지 : 대형 프로젝트를 수행하기 위한 모듈의 묶음

- 패키지는 파일이 포함된 디렉터리(폴더)로 구성된다.<br>
- 다른 사람이 만든 프로그램을 불러와 사용하는 것을 라이브러리라고 하는데, <b>파이썬에서는 패키지를 하나의 라이브러리로 이해</b>
- 패키지에는 예약어가 있다 (__init__.py)

### 패키지 만드는 방법
01. 디렉터리 구성하기<br>
 각 패키지 내에서 다시 세부 패키지에 맞춰 디렉터리 구성
 ```
 mkdir roboadvisor
 cd reboadvisor
 mkdir crawling
 mkdir database
 mkdir analysis
 ```

02. 디렉터리별로 필요한 모듈 만들기<br>
```__init__.py``` : 각 디렉터리가 패키지임을 나타내는 예약 파일 
-> 각각의 디렉터리를 하나의 패키지로 선언하기 위해서 만듦

03. 디렉터리 별로 ```__init__.py``` 파일 구성하기
 ```__init``` : 해당 디렉터리가 파이썬 패키지라고 선언하는 초기화 스크립트<br>
 이 파일 안에는 해당 패키지가 포함된 모듈에 관한 정보가 있다.<br>
 ** 디렉터리의 하위 패키지는 ```__all__, import```를 사용해 선언해야한다
 ```python
 import analysis
 import crawling
 import database

 __all__ = ['analysis', 'crawling', 'database']
 ```

04. '__main__.py'파일 만들기
> 패키지를 한 번에 사용하기 위해 만듦, 패키지 자체를 실행하기 위함

-> 기본적으로 호출해야 하는 여러 모듈을 from, import문으로 호출한 후, ```if __name == '__main__'```구문 아래 실행 코드를 작성

```python
from analysis.series import series_test

if __name__ == '__main__' :
    series_test()
```

05. 실행하기<br>
상위 디렉터리에서 'python 패키지명'를 입력

### 패키지 네임스페이스
01. 절대 참조 : 전체 패키지의 구조를 생각해 모듈의 경로를 모두 호출하는 것<br>
``` from roboadvisor.analysis import series```
02. 상대 참조 : 호출하는 디렉터리를 기준으로 호출하는 것<br>
```from .series import series_test```
<br> -> 현재 디렉터리에서 series모듈 안의 series_test 함수를 호출하라는 뜻
<br>(점 1개 : 현재 디렉터리 / 점 2개 : 부모 디렉터리)

## 가상환경 사용하기
> 각 프로젝트에 맞는 환경을 설정하여 진행하기 위한 개념

대표적인 가상환경 도구 : virtualenv , conda

### 가상환경 설정하기 

01. 가상환경 만들기
 ```conda create -n 가상환경 이름 python=버전```

02. 가상환경 실행하기
 ```activate 가상환경 이름```

03. 가상환경 패키지 설치하기
 ```conda install 패키지```
