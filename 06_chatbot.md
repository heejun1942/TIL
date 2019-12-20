# 챗봇 만들기

telegram > BotFather



### 1. 챗봇 생성

1. ` /newbot`입력 후 이름 설정 > token을 받음
2. 검색창에서 나의 bot이름을 입력하여 들어감.
3. `app.py` **flask**파일 생성

```python
#플라스크 기본설정

from flask import Flask

app = Flask(__name__)


if __name__ == ("__main__"):
    app.run(debug=True)
```



### 2. 기본설정

(설명서: https://core.telegram.org/bots/api) 

- 메소드 형식: https://api.telegram.org/bot<token>/METHOD_NAME 



1. method > getMe :  내 정보 확인

2. 챗봇에 `/start`입력

3. method > getUpates : 계정아이디 복사

4. method > sendMessage: *chat_id*와 *text*정보가 필요함

   - 정보 보내는 법: ?[변수1]=[값1]&[변수2]=[값2]

     /sendMessage?chat_id=<내 id>&text=<안녕하세요>

5. `pip install python-decouple`

   - 안전을 위해 `.env`파일에 쳇봇 id와 token을 넣어놓자.

   ```
   #.evn
   
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

   - `commit` 후 `push`하면 `.evn`는 올라가지 않음



### 4. WebHook

telegram서버와 내 서버를 연결.? 

(참고: setWebHook)

1. ngrok 다운

   - ngrok: 

   https://ngrok.com/ > download > **ngrok**다운

   cmd에서 -------------

   'https:// ~~' 주소가 내 flask 주소

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