---
title: 【Git 筆記】 如何使用 ssh 路徑
tags: Git
---
在管理Git專案上，很多時候都是直接使用https url克隆到本地，當然也有有些人使用SSH url克隆到本地。以下簡單介紹這兩種方式的主要區別

## 儲存庫路徑差異

`https` 和 `ssh` 兩個均是 Git 儲存庫的路徑，Github 官方推薦使用 `https` 但同時也提供 `ssh` 的連線方式，兩者差異點在於:

* `https` : 在上傳時需要輸入帳密，如果不需要，大多是帳密(Key Chain)已存在電腦內。
* `ssh` : 已先在電腦內設定好金鑰，上傳時不需要輸入額外帳密

## 如何設定 Github SSH 金鑰

輸入 `ssh-keygen` 產生金鑰，會出現下方訊息

``` bash
$ ssh-keygen                                   # 產生金鑰
Generating public/private rsa key pair.
Enter file in which to save the key (/home/xxx/.ssh/id_rsa):   # 金鑰存放路徑，直接按 Enter
Created directory '/home/xxx/.ssh'.
Enter passphrase (empty for no passphrase):    # 密碼，可設定可不設定，設定的話每次上傳會多需要輸入一次密碼
Enter same passphrase again:                   # 再輸入一次密碼
The key fingerprint is:                        # 之後會顯示你的 fingerprint，到這裡就完成 key 的產生了
```

## 將金鑰貼到GitHub

``` bash
cat /home/xxx/.ssh/id_rsa.pub           # 讀取檔案內容
ssh-rsa ~...一連串金鑰...~ xxx@xxx-PC           # 從 ssh-rsa 複製到 username@pc-name
```

開啟自己的 GitHub 網頁，點擊頭貼的 `setting` ，頁面右側的 SSH and GPG keys 打開，按下 New SSH key，將複製的內容貼到下欄 key 的位置，Title 可自行填寫方便辨認的名稱。
