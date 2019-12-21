# 챗봇 만들기

**Telegram**으로 나만의 챗봇 만들기



### 1. 챗봇 생성

1.  Telegram 설치 후 검색창에 BotFather 검색
2. BotFather에 들어가 ` /newbot`입력 > 내 bot 이름 설정 후 token을 받을 수 있음
3. 검색창에 내 bot이름을 검색하여 찾을 수 있음. 
4. 챗봇과 정보를 주고받을 `app.py` **flask**파일을 만들자

```python
# Flask 기본설정

from flask import Flask

app = Flask(__name__)


if __name__ == ("__main__"):
    app.run(debug=True)
```



### 2. Telegram 메소드 이용방법

(설명서: https://core.telegram.org/bots/api) 

- .메소드 형식

  ```
   https://api.telegram.org/bot<token>/METHOD_NAME 
  ```



1. method > getMe: 제대로 bot이 생성되었는지 확인

2. `/start`입력한 후, getUpdates 메소드를 통해 chat_id확인 가능 (chat에 있는 id임)

   ```
   https://api.telegram.org/bot<token>/getUpdates
   ```

3. sendMessage 메소드로 메시지 보내보기. *chat_id*와 *text*정보가 필요함

   - 정보 보내는 법: ?[변수1]=[값1]&[변수2]=[값2]

   ```
   /sendMessage?chat_id=[내 id]&text=[메시지]
   ```

4. `pip install python-decouple`: python-decouple 라이브러리 설치

   > python-decouple:  python으로 ini 파일이나 env 설정 파일을 파싱할 수 있는 패키지

   - 안전을 위해 `.env`파일에 chat_id와 token을 넣어놓자.

   ```
   #.env
   
   CHAT_ID="[chat_id]"
   TELEGRAM_BOT_TOKEN="[chat_tocken]"
   ```

   ```python
   #app.py
   
   from decouple import config
   
   token=config("TELEGRAM_BOT_TOKEN")
   chat_id=config('CHAT_ID')
   ```



### 3. Git으로 관리하기

1. id와 token 보호를 위해`.gitignore`파일 생성

   ( http://gitignore.io/ 에서 'window', 'flask', 'python', 'venv', 'visual studio code' 입력 후 코드 복붙)

   - `commit` 후 `push`하면 `.env`는 올라가지 않음



### 4. WebHook: ngrok사용

>  WebHook을 통해 Telegram서버와 Flask서버를 연결하기 

<img src="https://www.ntaso.com/wp-content/uploads/2016/04/telegram-bot.png" style="zoom: 50%;" />

1. ngrok 다운로드

   > ngrok이란 방화벽 뒤에 있는 `로컬 서버`를 안전한 터널을 통해 공개 인터넷에 노출시켜 주는 도구. 
   >
   > 즉, 포트 포워딩과 같은 네트워크 환경 설정 변경없이 로컬에 실행중인 서버를 안전하게 외부에서 접근 할 수 있게 해줌.

   https://ngrok.com/ > download > **ngrok**다운

   cmd에서 `ngrok http 5000`입력하여 주소를 받을 수 있음 (※주의: 실행시킬 때마다 주소가 변경됨)

   ![](https://user-images.githubusercontent.com/58925328/71307355-806eda00-2430-11ea-98ca-c84c07236d4c.PNG)

   

2. `webhook.py`파일 생성

   ```python
   from decouple import config 
   import requests
   
   token = config("TELEGRAM_BOT_TOKEN")
   url = "https://api.telegram.org/bot"
   ngrok_url = "https://2ccfe768.ngrok.io"
   
   #setwebhook을 설정
   data = requests.get(f'{url}{token}/setwebhook?url={ngrok_url}/{token}')
   print(data.text)
   ```

3. Telegram과 데이터 주고받기

   ```python
   @app.route(f'/{token}', methods=["POST"])
   def telegram():
       # 챗봇에서 내가쓴 데이터 읽어오기(json형태)
       re_data=request.get_json()
   
       # json데이터에서 원하는 정보뽑기
       re_id= re_data['message']['chat']['id']
       text=re_data['message']['text']
   
       # 챗봇에게 다시보내기
       requests.get(f'{url}{token}/sendmessage?chat_id={re_id}&text={text}')
       
       #200은 접속성공을 의미하는 숫자임!
       return "ok", 200   
   ```



python anywhere https://www.pythonanywhere.com/