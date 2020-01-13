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

  ```python
  plus = lambda a,b: a+b
  result = plus(10,20)
  print(result)
  ```

  

  



## 입출력

- print()

`print('Life', end=' ')`: 줄바꿈 안하고 싶을 때 `end`를 사용

- input()

- open('파일명', '모드'): 파일 생성/열기

  ```python
  file= open('c:/test.txt', 'r')
  print(file.read())
  file.close() #모든 작업 후 닫아줘야함. 메모리에 올려놓음
  ```

  - r, x는 파일이 없으면 오류가 뜸. (x: 쓰기모드)
  - w, a는 파일이 없는 경우 새 파일 생성. but, w는 파일이 있는 경우 덮어씀.
  - 두번째 인자를 안쓰면 'rt'로 인식

  - 인코딩 문제시

  ```python
  #open의 인자로 encoding을 지정해주자
  
  f=open('c:/dev/text.txt', 'rt',encoding='UTF-8')
  print(f.read())
  f.close()
  ```

  