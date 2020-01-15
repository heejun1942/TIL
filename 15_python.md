

# ???

>예외처리/ 내장함수/ 외장함수/ 정규식/ 크롤링



- 리스트 해당 인덱스가 없으면 오류. 인덱스를 지정해 줄 때 항상 조심 (IndexError)



### 예외처리

- **try- except**: 코드가 실행될 때 대략적으로 이런 오류가 발생할 것 같을 때

- 강제 종료되는 것을 방지

`try - except`: 오류마다 경고 메시지를 따로 줄 수 없음

`try - except 발생오류`: 오류마다 경고 메시지를 줄 수 있음



try 모두 실행함. 오류발생이면, expcet 아니면 else 실행.

try - except - finally: finally는 예외발생 여부에 상관없이 **항상 실행**. 접속 후 성공여부에 상관없이 close()를 해줘야하는 상황.

```python
try:
	file = open('test.txt', 'r')
    print('file open')
	text = file.read()
	print(text)
	text += 1 # TypeError 발생
except:
	print('예외발생')
finally:
	file.close() # 항상 실행
	print('file close')
```



- 의도적으로 오류 발생

라이브러리를 개발하는 사람은 오류를 떠넘김

사용자가 문제를 해결할 수 있도록



### 내장함수

abs(숫자): 절대값을 반환

all(리스트): 반복가능한 자료형의 모든 요소가 참일 때, True 반환.

any(리스트): all()과 반대. 하나라도 참이 있으면, True 반환

chr(아스키코드): 아스키코드를 문자로 돌려줌

ord(문자): 문자를 아스키코드로 돌려줌. chr()과 반대

dir(객체): 객체가 가지고 있는 변수, 함수를 볼 수 있음

divmod(숫자1, 숫자2): 나누기하여 (몫,나머지)를 튜플로 리턴 > 숫자1/숫자2

enumerate(리스트): 인덱스와 요소를 돌려줌. 

**eval(문자열)**: 문자열을 파이썬 **실행 코드**로 바꿔줌.

filter(조건함수, 리스트): 반복가능한 자료를 입력받은 후 참인 값만 돌려줌

	- filter는 list와 짝꿍일까? list(filter())

hex(10진수): 16진수로 돌려줌

id(객체): 주소값을 알려줌

input(): 사용자 입력을 받아 문자열로 반환

int( '숫자' ): 문자열을 숫자로 바꿔줌. 또한, 실수를 정수로 바꿀 수 있음. 10진수가 아닌 수를 10진수로 바꿀 수 있음

isinstance(요소,클래스): 해당 요소와 클래스가 같은 인스턴스인지 확인해 bool 반환. 

```python
class Car: pass
a = Car()
class Taxi(Car): pass
b = Taxi()

isinstance(a, Car)  #True
isinstance(b, Taxi)  #True
isinstance(b, Car)  #True
isinstance(10, int)  #True
isinstance(10.0, float)  #True
```



len(리스트): 요소의 개수를 돌려줌. 문자열도 가능

list(): 리스트로 만들어줌.

map(함수, 리스트): 반복 가능한 자료를 입력받아 함수 결과를 돌려줌

- 필터는 걸러줌. map은 적용시킴

max(): 요소중 최대값을 돌려줌. 문자열은 아스키코드로 비교

min()

sum()
oct(10진수): 8진수로 리턴

open()

pow(숫자x, 숫자y): x**y를 돌려줌 

range(): 해당 범위를 반복 가능한 객체로 만들어서 돌려줌.

- range(1, 10, 2): 1-9까지 2씩 건너뜀

sorted(): 반복 가능한 자료형을 정렬해 리턴 

- 만약, dictionary의 value를 기준으로 정렬하고 싶다면 operator를 import해 사용해야함

str(): 문자열로 바꿔서 리턴

- 주의: str(리스트)의 결과인 '[1,2,3]'는 다시 리스트로 돌릴 수 없음

tuple()

type(): 자료형을 알려줌

zip(): 동일한 인덱스끼리 묶어서 튜플로 반환. 인자의 길이가 동일해야함





### 외장함수

>내장함수와 다르게 모듈을 부르는 import과정을 거쳐야함
>
>

sys

pickle: 객체의 형태를 그대로 유지하면서 파일을 저장하고 불러올 수 있는 모듈

os: 

glob.glob()

time

time.sleep(): 코드를 일정시간 멈춰세움.

datatime보단 time을 더 많이 사용함

무슨 요일인지 알려주는 > calendar.weekday(년,월,일)

그 연도의 2월의 마지막날 > calendar.monthrange(년,월) 









