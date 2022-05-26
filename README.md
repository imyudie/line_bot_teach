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
  
到這就可以恭喜你，成功創建一個機器人的皮!
  
  
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














