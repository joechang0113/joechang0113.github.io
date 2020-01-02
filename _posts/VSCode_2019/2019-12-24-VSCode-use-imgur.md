---
title: 【VSCode 筆記】 使用 MarkDown 套件
tags: VSCode
---

## 前言

有用過 HackMD 的玩家應該對於圖片可以自動上傳到 imgur 很心動，但是又比較習慣 VSCode 多套件支援的情況下，如果可以在 VSCode 使用 Imgur 的自動上傳功能，像下面的操作一般會省下很多附加圖片的時間

![img](https://i.imgur.com/jPm7V6t.gif)

## Imgur 帳號申請

沒有帳號的朋友先到 [Imgur 官網](https://imgur.com/) 申請一個

![Image](https://i.imgur.com/MvCSia8.png)

### 取得 API

到 [這裡](https://api.imgur.com/oauth2/addclient) 申請 API，接著填寫一些必要訊息

* Application name：隨便想，最好自己可以認得
* Authorization type：OAuth 2 authorization without a callback URL

參考如下

![Image](https://i.imgur.com/JoNS3ZD.png)

submit 之後會取得兩樣東西，這時請務必要複製下來保存好

* Client ID
* Client secret

![Image](https://i.imgur.com/sYK5Y32.png)

ClientID 遺失可以到下圖的地方找，但是 Client secret 就必須要重新生成了

![Image](https://i.imgur.com/hFb0xxU.png)

> 到這邊 Imgur 的網頁先不要關掉，等一下還會需要，我們先到 VSCode 做相關設定

## VSCode

首先，到 EXTENSIONS（市集）輸入 `vscode-imgur` 並安裝

![Image](https://i.imgur.com/K3MY9nS.png)

接著到 VSCode 設定檔，打開 `setting.json`

![Image](https://i.imgur.com/Rw5zllj.png)

打開後複製下面程式碼貼到 `setting.json`

``` bash
"vscode-imgur.client_id":  # 剛剛 imgur 的 client_id"
"vscode-imgur.client_secret":  # 剛剛 imgur 的 client_secret
"vscode-imgur.preferUserUpload": true,
```

接下來去隨便找一個圖片點右鍵拷貝影像（複製圖片）

![Image](https://i.imgur.com/VfPsNQC.png)

然後在 VSCode 的任一 `.md` 檔案中按下 option + comman + v(CTRL + ALT + V)，接下來會跳出這個視窗

![Image](https://i.imgur.com/00yEWLA.png)

這時候切回去 Imgur 畫面，如下圖，會詢問是否允許 vscode 使用 Imgur 來上傳圖片，*當然要啊！不然都看到這邊要放棄嗎*。

![Image](https://i.imgur.com/mNgYVSW.png)

接下來複製畫面出現的一組 PIN

![Image](https://i.imgur.com/Q0WI9Fc.png)

將這組 PIN 貼到這裡

![Image](https://i.imgur.com/8P4lzoz.png)

到這邊只要*複製圖片*，使用 option + comman + v(CTRL + ALT + V) 貼上圖片，這樣就可以自動上傳 imgur 並加入到你的 `.md` 檔案裡面

## 相簿分類

如果本來就有再用 Imgur 的玩家，這樣上傳的方式一定會增加 Imgur 整理的困難，所以我們可以將上傳的照片另外用一個相簿整理起來，請先進入 Imgur ，點選右上角頭貼，打開 images

![Image](https://i.imgur.com/YSmMznP.png)

到 All Images 的下拉選單點選 New Album

![Image](https://i.imgur.com/xZfz4vB.png)

接著輸入你想要的命名以及這個相簿的相關描述

![Image](https://i.imgur.com/QYnSFop.png)

建立相簿完成後，點選頭貼的 gallery profile

![Image](https://i.imgur.com/DmrwItv.png)

點選你剛剛建立的相簿，我的是 Blog Posts

![Image](https://i.imgur.com/HZG8B6z.png)

點進去後看一下自己的網址應該會是這樣

`https://imgur.com/a/xxxxxx`

記住後面的 `xxxxxx` 然後回到 vscode，將下方代碼放進 `setting.json`

``` json
"vscode-imgur.album_id": "相簿代碼",  // 相簿代碼就是上面的 xxxxxx
```

以上相關設定做個紀錄有興趣的朋友也可以試試看！！
