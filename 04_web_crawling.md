# Python_웹 크롤링



### 1. 가상환경 만들기 

> - venv: 가상 환경을 만들고 관리하는데 사용되는 모듈
>
> - pip: 파이썬으로 설치한 패키지를 관리하는 시스템으로, 패키지를 설치, 업그레이드 및 제거할 수 있음

`python -m venv venv`: **venv** 가상환경 만들기 

`source venv/Scripts/activate`: 가상환경 활성화

`deactivate`: 가상환경 종료

`pip list`: 현재 추가된 가상환경 내에 라이브러리 목록을 보여줌



### 2. 패키지 설치

> - requests: Python에서 HTTP 요청을 보내는 라이브러리
>
> - BeautifulSoup: HTML 및 XML 파일에서 원하는 데이터를 손쉽게 Parsing 할 수 있는 라이브러리

`pip install requests`: requests 패키지 설치

```python
import requests
```

`pip install beautifulsoup4`: beautifulsoup4설치

```python
from bs4 import BeautifulSoup
```



### 3. 웹 크롤링

`request.get(url).text`: *url*주소의 html을 반환

`BeautifulSoup(request, 'html.parser')`: html을 파싱해줌 (xml 등 가능)

[예제1]

```python
import requests
from bs4 import BeautifulSoup

url = "https://finance.naver.com/sise/"

#페이지의 html태그를 가져옴
request = requests.get(url).text

#html을 파싱함
soup = BeautifulSoup(request, 'html.parser')

#해당 id의 html을 가져옴 > text만 출력
kospi = soup.select_one("#KOSPI_now")
print(kospi.text)	
```



[예제2]

```python
import requests
from bs4 import BeautifulSoup

url="https://finance.naver.com/marketindex/"

req = requests.get(url).text
soup= BeautifulSoup(req, 'html.parser')

#class를 가져올 때 상위의 id를 선택해주자
ex=soup.select_one("#exchangeList .value")
print(ex.text)
```



[예제3] 네이버 검색어 가져오기 

```python
import requests
from bs4 import BeautifulSoup

url="https://www.naver.com"

req = requests.get(url).text
soup= BeautifulSoup(req, 'html.parser')

# soup.select(): 모든 요소를 리스트로 반환
search=soup.select("#PM_ID_ct > div.header > div.section_navbar > div.area_hotkeyword.PM_CL_realtimeKeyword_base > div.ah_roll.PM_CL_realtimeKeyword_rolling_base > div > ul > li > a > span.ah_k")

for item in search:
    print(item.text)
```




