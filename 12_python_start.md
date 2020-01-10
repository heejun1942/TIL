# 파이썬

'주피터 노트북' 라이브러리가 python 3.8에서 잘 동작하지 않음

파이썬은 버전에 따라 라이브러리가 동작하지 않는 경우가 많음. 



파이썬 3.8 에서 '주피터 노트북' 사용법

```
ㅇ visual c++ 2005 설치


ㅇ Lib/asyncio/__init__.py
import asyncio
if sys.platform == 'win32':  # pragma: no cover
    from .windows_events import *
    asyncio.set_event_loop_policy(asyncio.WindowsSelectorEventLoopPolicy())
    __all__ += windows_events.__all__
else:
    from .unix_events import *  # pragma: no cover
    __all__ += unix_events.__all__
```



## 1. 환경설정



### 1) Miniconda 설치

> Anaconda: 가상환경을 통해 파이썬 버전을 설정할 수 있음. python 언어를 관리해주는 것.
>
> Miniconda: 용량을 줄인 아나콘다

1. miniconda 사이트에서 Python 3.7 설치

설치시 add path 체크해주기.



2. 주피터 노트북 설치

> 주피터 노트북: 코드가 라인별로 실행되기 때문에 오류발생시 처음부터 다시 실행하지 않아도됨. [개발툴]

주피터 노트북에서는 변수만 쳐도 print됨.

두가지 모드가 있음: 입력모드, 명령모드

꼭 위에서 아래로 실행되는 것이아님.



3. 가상환경 생성

`conda create --name myenv`: 아나콘다를 이용하여 가상환경 생성

`activate [가상환경이름]`: 실행

`conda deactivate`: 가상환경 종료

`conda install matplotlib`: matplotlib 설치하기

가상환경 제거: 해당 폴더 삭제

pip로 패키지 관리할 수 있지만 아나콘다로 관리할 수 있음

가상환경은 어느 위치에서든 실행할 수 있지만, 그 위치의 폴더를 사용하는 것임.



### 자료형

리스트 안의 자료형은 달라도 가능

tuple은 리스트와 비슷. but, 변경불가. 추가는 가능.

Dictionary는 자바의 map임. (다른곳에서는 table로도 불림)

Bool은 True, False의 첫글자가 대문자!



더하기는 자료형 일치가 되야함.

(문자열은 문자열끼리만 더하기 가능.)



※참고: 주피터 노트북 단축키

`h`: 단축키보기

`dd`: 삭제

`a`:앞에 추가

`b`:뒤에추가

`ctrl+enter`: 실행

`shift+enter`:실행하면서 아래로 선택이 내려감



문자열Formatting - (두가지방법 존재)

1. %를 사용해서 문자열에 값 삽입하기

2. {}를 사용. **문자열과 숫자를 구분하지않아** 편리함. 또는 {}안에 값이름을 지정해줄 수 있음



- count(): 자바에는 없는 기능. 자바는 반복문사용.

- 문자열 위치 찾는 함수: find(), index() >> 차이점: 해당 문자가 없는경우 find()는 -1을 반환하지만 index()는 에러발생.

- join은 리스트를 문자열로 합쳐줌.

  split(): 문자열을 리스트로 만듬

- 공백제거 strip(),rstrip(),lstrip()

- list에 요소넣기: **append()**, extend(), insert(), 더하기연산자(+)

- set은 순서가 없으므로 **특정 값만** 선택하여 조회하거나 수정 불가 (추가/삭제는 가능)

- Boolean False일 때  > 0, '', []



#### 변수

변수는 **값**을 담거나, **주소**를 담음. > 참조 자료형(주소), 기본 자료형(값)

파이썬은 변수선언에 자료형이 없음

튜플을 이용하여 한번에 여러 변수 선언 가능

​	 a, b = ('python', 'variable')   //a='python', b='variable'









#### mutable vs inmutable (43p 참고)

list는 muatable, tuple은 inmutable이다

참조 자료형(주소), 기본 자료형(값)

​	참조자료형: list, dictionary, set

​	따라서 list의 값을 **복사한 변수**를 가지고 싶다면, 

​		list2=list1  (X) 

​		**list2 = list[:]**  (O)





#### 제어문

- {}를 쓰지않고 **들여쓰기**(Tab, 4칸)로 인식하므로 주의하자.





파이썬의 for문은 for-each 방식임.





