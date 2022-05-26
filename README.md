## line機器人基本架設教學

### 基本介紹
本篇教學是建立在**已接觸過Python基本語法**的人，因此中間會跳過些許介紹，在部屬至heroku部分很容易出現些問題，若是有問題可以直接私訊我。

### 所需工具

1. [python語言](https://www.python.org/downloads/)
2. [git](https://git-scm.com/downloads)
3. [heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)([下載](https://cli-assets.heroku.com/heroku-x64.exe))
4. [VScode](https://code.visualstudio.com/download)
5. [line developers](https://developers.line.biz/console/)

### 前置準備(已有可跳過)

#### 一. 下載python環境
  
因為此機器人需使用python中的flask模組，所以要先建設python的環境至電腦中。進入到[下載介面](https://www.python.org/downloads/)可看到下圖，點擊Downloads便可下載，直接一路安裝到底便可。
  
![image](https://user-images.githubusercontent.com/102812213/170426852-b040a03c-f1eb-4b1c-b630-3925bca32f44.png)

  
記得，一定要勾選**Add python xx.xx.xx to PATH** 來加入環境變數
  
![image](https://user-images.githubusercontent.com/102812213/170429765-2a859727-b470-4b26-9aaa-9fc5a9cd4abe.png)
  
接下來一路下一步就可。

#### 二. 下載git

不管是要push至github還是部署heroku網頁，甚至以後要開發專案都需使用的分散式版本控制軟體，現在大多linux系統都自帶，但是windows卻須自行下載。
  
進入[下載介面](https://git-scm.com/downloads)下載符合系統的git，例如我是使用windwos，便是點擊Download for Windows，下載後一樣一路按next就好。
  
![image](https://user-images.githubusercontent.com/102812213/170431758-2c98fc6c-0e65-4edd-92e3-0a8d1b4f8dcb.png)
  
#### 三. 安裝heroku CLI

CLI 是命令列介面 (Command-Line Interface)，是與電腦互動的指令。因此我們要下載heroku CLI來與heroku溝通。
  
進入至[下載介面](https://devcenter.heroku.com/articles/heroku-cli)後，點選符合系統的按鈕，我還是一樣選擇windows x64。若系統是mac就必須使用終端機，輸入`brew tap heroku/brew && brew install heroku`。下載後一樣一路按next就好。
  
![image](https://user-images.githubusercontent.com/102812213/170433444-bcb5dc52-6185-45b3-9c6c-67bb9400c467.png)

#### 四. 安裝VScode

VScode是一個許多開發人員愛使用的文本編輯器，並且有許多模組可幫助快速開發，但這並不是此篇重點。  
一樣進入[下載介面](https://code.visualstudio.com/download)，點選符合系統的按鈕。下載後一樣一路按next就好。
  
![image](https://user-images.githubusercontent.com/102812213/170435487-f33bf9c8-c102-4015-818a-9b4594d2c280.png)
  
---
  
### 基本帳號設定

#### 一. Line developers 建立機器人

line機器人最主要還是基於line釋出的API上，只要有line的帳號便可聲請機器人，當然，我們使用的是免費版，所以還是有**每月只有500則push message的推播數量**的限制。
  
最先便是[到這裡](https://developers.line.biz/console/)登入自己的line，可看見以下畫面 :
  
![image](https://user-images.githubusercontent.com/102812213/170441266-6fad8d25-49e9-48fb-bee7-3d274e1e7685.png)
  
登陸後進入Channels，點選Create a new channel :
  
![image](https://user-images.githubusercontent.com/102812213/170441663-6574a777-8349-4750-8f86-f54ca092d886.png)
  
點選Messaging API :
  
![image](https://user-images.githubusercontent.com/102812213/170442290-6cbc49f7-2360-4fda-8073-c2a540d7b348.png)
  
接下來進入下圖介面，Channel type上一部已經選好了，Provider便是提供者，因為是測試所以我都隨便輸，Company or owner's country or region 選擇自己的國家，Channel icon想放甚麼就放甚麼，但一定要是圖檔 :
  
![image](https://user-images.githubusercontent.com/102812213/170442818-9f391bee-462b-4d60-b883-4f43454784fc.png)
  
往下滾後可看見下圖，Channel name填你想要的名字，Channel description便是機器人說明，Category和Subcategory我一律選其他媒體 :
  
![image](https://user-images.githubusercontent.com/102812213/170443649-f77f5efb-7473-4af9-b171-c3b64d57cc81.png)
  
最後填上e-mail就好，並將下面兩個框打勾，點選create便可 :
  
![image](https://user-images.githubusercontent.com/102812213/170444429-d4e1a2ca-5186-42d5-b34d-a92180718593.png)
  
到這就可以恭喜你，成功創建一個機器人的皮!但是!!我們還有一些前置設定要先設好。
  
先到Messaging API中 :
  
![image](https://user-images.githubusercontent.com/102812213/170460281-c7beadd4-1c55-42d4-8f09-ecb7339b6807.png)
  
往下滑到這 :
  
![image](https://user-images.githubusercontent.com/102812213/170460491-b47138b2-d78a-4235-a7fc-7bb3d47996a0.png)

  
我們要把它預設的自動回復關掉，點選Auto-reply messages的Edit，設定成下圖 :
  
![image](https://user-images.githubusercontent.com/102812213/170460859-1acaa538-3226-4439-96f9-6b62a267ef3e.png)
  
結束後回到上一頁，往下滑到Channel access token (long-lived)，點下面的Issue
  
![image](https://user-images.githubusercontent.com/102812213/170461217-bca684f6-3db9-437a-a354-3417d740d694.png)
  
便會產生一長串的Channel access token，這樣line端的前置作業便解決了!!!!(下圖我密碼處理過~)
  
![image](https://user-images.githubusercontent.com/102812213/170461825-0ce1196b-9b0a-4bdf-ad36-b556db252f12.png)
  


#### 二. heroku帳號申請(有了就直接跳過)

[點我到heroku申請帳號](https://signup.heroku.com/login?redirect-url=https%3A%2F%2Fid.heroku.com%2Foauth%2Fauthorize%3Fclient_id%3Dd2ef2b24-e72c-4adf-8506-28db2218547d%26response_type%3Dcode%26scope%3Dglobal%252Cplatform%26state%3DSFMyNTY.g2gDbQAAAHhodHRwczovL2Rhc2hib2FyZC5oZXJva3UuY29tL2F1dGgvaGVyb2t1L2NhbGxiYWNrP3N0YXRlPTRjMGJmMDRkODBkYTg2MzI0ZTc3NzNhMjgzNDllYmY4ZWU0MzM3NjFjM2JjNzQ5MTg1MWUyYzdlZWQzNjBmZjNuBgAgSmn_gAFiAAFRgA.oFNaB9jRwVj9LovZDBxfNxMoaqFckVh5avXhB4ddwo8)
  
進入heroku註冊頁面(下圖)註冊一個帳號，這....應該不用我教吧?
  
![image](https://user-images.githubusercontent.com/102812213/170447004-929601cf-1e00-45e2-82d0-312bd4beb05d.png)
  
#### 三. heroku建立app

進入後會看見這樣的介面 :
  
![image](https://user-images.githubusercontent.com/102812213/170447744-8bb51b64-18aa-42ef-83e6-b44eabe99953.png)
  
點右上的new，選擇create new app :
  
![image](https://user-images.githubusercontent.com/102812213/170447959-2b888e41-4837-4fbb-a356-770ebf14cdeb.png)
  
填上你要的名字，完成後點Create app
  
![image](https://user-images.githubusercontent.com/102812213/170449129-bfec8f8e-e5da-4fbd-bf88-2c73571d03ab.png)
  
到這恭喜你，完成60%了，剩下程式和上傳部分!!

---
  
### 機器人程式

早先說過，這次機器人主要以python為主，而這些程式就需要使用編輯器來編輯，本篇便是使用VScode，當然，使用spyder和python原廠IDE也可，但這些還要另開終端機，在部屬時還要切到CMD中，而VScode本身便自帶CMD，還有須多輔助模組，最主要還是**我用的習慣**!  
  
再來在任何你喜歡的地方新建資料夾，再到VScode中開啟資料夾:
  
![image](https://user-images.githubusercontent.com/102812213/170469097-a51f57bc-b0f5-431a-be87-e7dcaef08a85.png)
  
並且新增三個檔案，"app.py"、"Procfile"(沒副檔名)、"requirements.txt"，或是直接下載我的範例，完成後目錄長這樣 :
  
![image](https://user-images.githubusercontent.com/102812213/170469768-c37e9db9-dedf-48b2-805a-47f28e54aa10.png)
  


我在這貼上官方所給的範例程式，把這直接貼入app.py中，裡面些細小的原理我便不闡述。  

```python
"""
這是官方的範例

"""

from flask import Flask, request, abort

from linebot import (
    LineBotApi, WebhookHandler
)
from linebot.exceptions import (
    InvalidSignatureError
)
from linebot.models import (
    MessageEvent, TextMessage, TextSendMessage,
)

app = Flask(__name__)

line_bot_api = LineBotApi('YOUR_CHANNEL_ACCESS_TOKEN')
handler = WebhookHandler('YOUR_CHANNEL_SECRET')


@app.route("/callback", methods=['POST'])
def callback():
    # get X-Line-Signature header value
    signature = request.headers['X-Line-Signature']

    # get request body as text
    body = request.get_data(as_text=True)
    app.logger.info("Request body: " + body)

    # handle webhook body
    try:
        handler.handle(body, signature)
    except InvalidSignatureError:
        print("Invalid signature. Please check your channel access token/channel secret.")
        abort(400)

    return 'OK'


@handler.add(MessageEvent, message=TextMessage)
def handle_message(event):
    line_bot_api.reply_message(
        event.reply_token,
        TextSendMessage(text=event.message.text))


import os
if __name__ == "__main__":
    port = int(os.environ.get('PORT', 5000))
    app.run(host='0.0.0.0', port=port)
```
  
主要讓機器人回應使用者的程式便是
```python
@handler.add(MessageEvent, message=TextMessage)
def handle_message(event):
    line_bot_api.reply_message(
        event.reply_token,
        TextSendMessage(text=event.message.text))
```
  
接下來就要將程式中的這兩行改為屬於你機器人的程式  
```python
line_bot_api = LineBotApi('YOUR_CHANNEL_ACCESS_TOKEN')
handler = WebhookHandler('YOUR_CHANNEL_SECRET')
```
  
到line developers中的Basic settings，向下滑可看到Channel secret(下圖)，把app.py中的`handler = WebhookHandler('YOUR_CHANNEL_SECRET')`中的`YOUR_CHANNEL_SECRET`改成你複製的Channel secret。
  
![image](https://user-images.githubusercontent.com/102812213/170467202-fb545fb0-c899-4c8d-94c5-505993cdcbae.png)
  
再到Messaging API中複製你的Channel access token(下圖)，把app.py中的`line_bot_api = LineBotApi('YOUR_CHANNEL_ACCESS_TOKEN')`中的`YOUR_CHANNEL_ACCESS_TOKEN`改成你複製的Channel access token。
![image](https://user-images.githubusercontent.com/102812213/170467378-fd962f06-5e29-40b8-84af-eed8e978e18c.png)
最後會變成像下面一樣
![image](https://user-images.githubusercontent.com/102812213/170468028-b9678040-230a-417c-9a7f-69726fd61a2c.png)
  
再來切到Procfile中，輸入
```
web: python app.py
```
再切到requirements.txt中輸入
```
line-bot-sdk
flask
```

好!到這裡完成80%，剩下將程式push到heroku便可!!
  
---
### PUSH至Heroku並和line連接

#### PUSH至Heroku

當我們程式碼寫完，當然要部署至Heroku中才能執行，而push就必須使用git，把鼠標移至上面的工具列，點終端機，新增終端機。
  
![image](https://user-images.githubusercontent.com/102812213/170471999-5d9d1c4d-0886-4ede-9a90-40bb91aeca2a.png)
  
它會跳出這樣的介面:
  
![image](https://user-images.githubusercontent.com/102812213/170472161-5fc65f5c-f4ae-4a65-9511-3b8f14fe2545.png)
  
這個功能跟CMD差不多，只是它已經幫你CD至程式的跟目錄，接下來的步驟最容易出錯，要仔細的看!!  
以下操作皆在終端機中輸入
1. 輸入` heroku login`
  
會跳出這個畫面
  
![image](https://user-images.githubusercontent.com/102812213/170472727-39622ccf-8870-491c-bdaf-92d5c7558b46.png)
  
按移下Enter就會進入瀏覽器中登錄
  
![image](https://user-images.githubusercontent.com/102812213/170473122-ea3d7342-4050-4d14-a540-254454d4dd24.png)
  
點login後就可切回VScode中

2. 輸入`git init`
3. 輸入`heroku git:remote -a {你 HEROKU APP 名字}`，顯示`set git remote heroku to https://git.heroku.com/xxx.git`便是成功
4. 輸入`git add .`
5. 輸入`git commit -m "first commit"`，註解此次動作為first commit，當然，也可以自己隨意取
6. 輸入`git push -f heroku master`，跑出下圖就是成功!!
  
![image](https://user-images.githubusercontent.com/102812213/170475225-4428ec3b-eeb3-4400-810c-39f362023f4b.png)
  
#### 和line連接

終於感人的時刻到來，要成功了!!
1. 進入Heroku網站中，點擊剛剛創建的APP，點擊右上的 open app ，複製跳出來網站的網址
  
![image](https://user-images.githubusercontent.com/102812213/170476714-19e2795d-6a21-47f4-b21d-c79efbf7bbbd.png)
  
2. 到line developers中的messaging，在Webhook URL貼上剛剛複製的網址，並在後面加上`/callback`，按下update就完成了!!!!!!
  
![image](https://user-images.githubusercontent.com/102812213/170477006-24dfd8c0-8c83-4183-b4b8-06283f8952c1.png)

---

###總結
這是我第一次使用.md編寫教學，希望排版不會太亂哈哈，若是有甚麼bug直接來問我沒關係，我也經歷了許多bug才熟練起來的!



