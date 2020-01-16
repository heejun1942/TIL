# 파이썬 크롤링



자동화된 방법으로 데이터를 가져와 저장하는 것

URL에 요청을 보내고 결과를 받음. 받은 결과물을 파싱하여 필요한 정보만 추출한다. 

라이브러리

- URL에 요청을 보내고 결과를 받음. > **requests**, urllib, urllib2
- 받은 결과물을 파싱 > bs4(BeautifulSoup) 



parameter

header ??

함수로 만들어 사용 get_html



beautifulsoup4 라이브러리 설치

conda install beautifulsoup4



```python
# 속성값 가져오기
imgs = soup.select('.number img')

for img in imgs:
    print(img['alt'])  #태그의 alt 속성값을 가져옴
```



select는 해당하는 모두를 가져옴 > select_one으로 해야 한개

find는 해당하는 첫번째 하나를 가져옴 > find_all로 해야 모두





#### Selenium

자바스크립트를 통해 생성되는 사이트일 때

브라우저를 통해서만 접속 허용하는 사이트일 때

설치

1. 파이썬 라이브러리 셀레니움

2. 사용할 브라우저의 드라이버

3. phantomjs (크롬대신)

   

대기: 브라우저에 HTML 요소가 보여진 후 코드 실행







※ 참고

주피터노트북 cmd에 커서가 있으면 멈춤

자바스크립트로 만들어진 태그는 크롤링이 X