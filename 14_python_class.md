# 파이썬 클래스



- 서랍장에 들어갈 수 있는 것: 전역변수와 함수

- 캡슐화: 변수는 숨겨주고, 함수제공  > 데이터 보호

- **self**: (함수 내 지역변수가 아닌) 클래스의 변수를 활용하려면 self 선언 필요.

  ```python
  # self가 있을 때
  class 클래스:
      def 함수(self):
          print('실행')
  객체 = 클래스()
  객체.함수()
  
  #self가 없을 때
  
  ```

- 클래스=, 인스턴스-= 

- 함수안에서 `self.var1`  > 전역변수 var1이 생성

  

- 참조자료형(list, dictionary, set)은 전역변수로 선언시 모두가 공유하므로, self를 이용하여 생성해야함.

```python
class Car:
# self를 쓰지않고 전역변수를 생성하면 주소를 공유함
# 리스트는 참조자료형이라서
#   car=[]  
    def __init__(self):
        self.car=[]  # 전역변수 생성
        
    def add_option(self, option):
         self.car.append(option)
        
    def show_option(self):
        return self.car

car1 = Car()
car2 = Car()
car1.add_option('전동 트렁크')
car1.add_option('통풍 시트')
car2.add_option('뒷자리 에어백')
car2.add_option('하이패스')
print(car1.show_option())
print(car2.show_option())
```



- 상속: `class [자식클래스명] ([부모클래스명])`
  - 기능이 아닌 개념을 받는(추상화)
  - 표준이나 규격을 함수로 만들어 놓음 > 상속받은 클래스는 동일한 규격을 가짐(다형성)
- **오버라이딩**: 부모가 물려준 함수를 수정함



```python
import random

class SelectMenu: 
    # 생성자를 통해 인자를 넘겨주므로, init에 parameter 생성.
    def __init__(self,menu):
        self.menuList=menu
        
    def get_menu(self):
        ran=random.randint(0,len(self.menuList)-1)
        choice = self.menuList[ran]
        return choice
    
    
menu = SelectMenu(['짬뽕', '초밥', '쌀국수', '주꾸미'])
print(menu.get_menu())
```



### 모듈

- 다른 사람이 만든 파일. 클래스가 아닐 수 있음.

- `import [파일명] `: 함수사용시 [파일명].[함수명1]

  `import [파일명] as [별명]` : 파일명이 너무 길 경우

  `from [파일명] import [함수명1],[함수명2]`: 특정 함수만 가져가기. 함수명만으로 실행 가능. (함수명이 겹치면 충돌발생 위험이 있음)

- `if __name__ == '__main__'`

  - 만든사람이 모듈을 테스트하기 위해.

  - 본 파일을 실행할 때만 실행됨. `__name__`이 `__main__`이 됨.

  - import했을 때는 `__name__`은 파일명(mymod)이므로 실행안됨.

  - 이것을 실행하기위해 다른 파일을 만드는 것이 비효율적임  >  이 파일에서 실행되게 하자.

```python
# mymod.py 
def myfunc(num1, num2):
    return num1+num2

if __name__ == '__main__':
    myfunc(3,5)
```





### 패키지

>모듈을 계층구조(디렉토리)로 관리하는 것

- driver/sound/mp3.py를 import 하기

  `import driver.sound.mp3`

- 패키지 안에 모든 파일을 가져오고 싶을 때 (import), `__init__.py`파일을 패키지 안에 만들어줌.

  ```python
  # __init.py__
  
  __all__=['mp3', 'wav']    # 패키지 내에 mp3.py, wav.py존재
  ```

  

  