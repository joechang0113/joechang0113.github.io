---
title: 【Android 筆記】 託管於 GitHub
tags: [Android, GitHub]
---
本篇紀錄一下，如何在 Android Studio 中使用 git 相關指令將程式碼上傳 GitHub 託管

## GitHub 遠程庫創建

新建 repo

![img](https://i.imgur.com/2TbAS3L.png)

取一個名字

![img](https://i.imgur.com/1nVAxLd.png)

## Android Studio 設定

到 android studio 專案中 打開 terminal，輸入

``` bash
git init
```

這個動作表示初始化一個本地儲存庫
![img](https://i.imgur.com/wxSf4GJ.png)

想當然我們要上傳到遠端儲存庫當然要把遠端地址給他，回到如下 github 頁面

![img](https://i.imgur.com/bP5dKmM.png)

先複製第一行程式碼貼到 androidstudio 的 terminal 內

``` bash
git remote add origin git@github.com:'your-git-name'/'your-repo-name'.git
```

執行後根據每個人使用 terminal 有些不同，但是基本如下沒有出現錯誤就是正確
![img](https://i.imgur.com/LbB27bS.png)
接著輸入

``` bash
git add --all
```

![img](https://i.imgur.com/COuSSKn.png)

接著查看 git 狀態，輸入

``` bash
git status
```

部分情形如下，意思是將這些新檔案加入到 Git 版控系統裡 gz[](https://i.imgur.com/YWIF37f.png)

接著為這些新檔案寫一些註解，以利自己或他人清楚此次提交所做的事情

``` bash
git commit -m "your comment"
```

![img](https://i.imgur.com/57PI34F.png)
接著將這些檔案 push 到遠端儲存庫

``` bash
git push -u origin master
```

![img](https://i.imgur.com/0d1S0d8.png)
沒有出現錯誤就是上傳成功，我們到 GitHub 頁面重新整理看看
![ig](https://i.imgur.com/U2ewmxn.png)
以上就是我們 androidstudio 的內容了！

## 製作 README.md

點擊右下角的 Add a README.md 製作一個簡單的介紹頁面，說明此專案的內容以及呈現

![img](https://i.imgur.com/wULXZew.png)

`README.md` 編輯完之後，捲動到最下方，comment 的地方可自行填寫，這邊我不更改只使用預設，最後點擊下方 commit new file
![img](https://i.imgur.com/zHKca4O.png)
接著回到我們的 android repo 如下畫面可以看到我們的首頁能呈現我們剛剛新增的 `README.md` 內容
