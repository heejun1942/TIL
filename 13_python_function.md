# 파이썬 함수 & 입출력

parameter가 몇개가 들어오는지 알 수 없을 때 \*를 붙여줌: `*args`

인자를 key=value 형태로 넘겨줄 때, `**kwargs`

여러개의 값을 한번에 return 할 수 있음 > tuple로 나옴.

```python
def funcB():
	return 'a', 'b'    #('a','b')
	
#리턴이 두개일 때, 각 변수에 따로 저장
retB1, retB2 = funcB()
```



return을 활용하여 강제 종료시킬 수 있음

boolean은 매개변수의 마지막에 위치해야함

지역변수, 전역변수는 **들여쓰기**로 구분함



- lambda: 함수를 간결하게 만들 때

  `[함수명] = lambda [parameter] : [return 값]`
  
  ```python
  plus = lambda a,b: a+b
  result = plus(10,20)
print(result)
  ```

  
  
  

## 입출력

>print(): 출력 / input(): 입력 
>
>open(): 파일을 다룰 때
>

- 여러개를 출력하는 방법: 띄어쓰기, +, 콤마(,)  >  자료형이 다를 때는 콤마를 써야함
- `print('Life', end=' ')`: 줄바꿈 안하고 싶을 때 `end`를 사용

- `open('파일명', '모드')`: 파일 생성/열기

  모드: r(읽기), w,x(쓰기), a(추가), t(텍스트), b(바이너리)
  
  - r, x는 파일이 없으면 오류가 뜸. (x: 쓰기모드)
  - w, a는 파일이 없는 경우 새 파일 생성. but, w는 파일이 있는 경우 덮어씀.
  - 두번째 인자를 안쓰면 'rt'로 인식

  - 인코딩 문제시 인자로 `encoding='UTF-8'`을 추가해주자.
  
  ```python
#open의 인자로 encoding을 지정해주자
  
  f=open('c:/dev/text.txt', 'rt',encoding='UTF-8')
  print(f.read())
  f.close()  #모든 작업 후 닫아줘야함. 메모리에 올려놓음
  ```

- 바이너리 모드(b)를 해야하는 경우: **List, Tuple, Dictionary, Set**  >  확장자 `.bin`

  - text 모드는 모든 것을 문자열로 만듬.
  - 리스트 안에 숫자만 가능. 문자열 X  >   라이브러리 **pickle**을 쓰자.
  
  ```python
  # pickle을 이용하여 리스트 파일에 저장하기.
    
  import pickle
    
  file = open('c:/dev/list.bin', 'wb')
  list1=['a',1,2,3,4,5]
    
  #file.write(bytes(list1)) 대신 아래와 같이 씀.
  pickle.dump(list1, file)
    
  file.close()
  ```
  
  ```python
  #pickle.load()로 읽기
  file=open('c:/dev/list.bin', 'rb')
  result=pickle.load(file)	
  print(result)
  file.close()
  ```



- read(): 모두읽음, 

  readline(): 한줄만 읽음, 

  readlines(): 줄바꿈 기준으로 한줄씩 리스트에 넣음.

- close()대신 **with**을 쓸 수 있음 (권장됨)

  ```python
  f=open('c:/dev/text.txt', 'rt')
  with file:
  	print(f.read())
  # f.close()  
  ```

- with은 __enter__와 __

