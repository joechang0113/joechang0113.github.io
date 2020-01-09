---
title: 【Android 筆記】 git push 專案到 GitHub
tags:

    - Android
    - Git

---
Android Studio 在 Git/GitHub 使用上其實很方便， 往下看 Android Studio 中如何使用 git 相關指令將程式碼上傳 GitHub 託管

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

## clone 專案

首先，我們打開 Android Studio 視窗，右下角有一個 `Configure` 的選單，打開並點擊 `Settings` ，Android Studio 已經有專案進行的朋友直接跳到 [專案內 clone 新 project](#%e5%b0%88%e6%a1%88%e5%85%a7-clone-new-project)

![Image](https://i.imgur.com/ShMoADm.png)

然後到 `Version Control` 打開 GitHub，沒有登入過的朋友會是一個 `add` 的 link，請先登入

![Image](https://i.imgur.com/erX2uzp.png)

接著回到起始頁面，點擊 `check out project from Version Control` ，選擇 `Git` 跳出如下

![Image](https://i.imgur.com/jdxTmjI.png)

在跳出的視窗中，貼上你要 clone 的 GitHub 地址

![Image](https://i.imgur.com/6V4547H.png)

接著等待開啟即可！

## 專案內 clone new project

Android Stuido 預設開啟會是上一次作業的 project 而不是起始視窗，所以如果 project 進行到一半才來到這裡的朋友請這樣做

到 File - New - Project from Version Control - Git

![Image](https://i.imgur.com/D8bNAC1.png)

打開後貼上要 clone 的 GitHub 地址

![Image](https://i.imgur.com/gOy3RaB.png)
