---
title: 【VSCode 筆記】 建立 VSCode 環境
tags: VSCode
---
Visual Studio Code 由 2015 年微軟所開發的一個開源軟體，它同時支援 Windows、Linux 和 macOS 作業系統的開源文字編輯器。它支援偵錯，內建了 Git 版本控制功能，同時也具有開發環境功能，例如代碼補全、代碼片段、代碼重構等，心動的話趕快看下去。

## 下載與安裝

首先到 [官網](https://code.visualstudio.com/) 下載並安裝 VSCode。

## 套件安裝

大家都用：

* EditConfig
  + 團隊開發時自定義編輯環境格式
* ESLint
  + 自動檢查 coding style，需搭配 `.eslintrc` 檔
* GitLens
  + 版控紀錄，根據修改檔案的時間點做紀錄，方便追蹤
* Path Intellisense
  + 輸入 `/` 可以自動牽引該目錄底下的建議路徑
* Preview on Web Server
  + 前端開發可以即時預覽
* vscode-icons / Material Icon Theme
  + 幫 VSCode 檔案與資料夾的 icon 做美化，選自己喜歡的風格安裝即可
* Code Runner
  + 調用二進制系統文件快速運行程式碼
* Prettier
  + 語法正確的前提下，格式化漂亮的程式碼，支持 HTML，CSS，JSON，Markdown 等等文件
* Auto Close Tag
  + 自動填充對應的 Tag 標籤
* Settings Sync
  + 同步 VSCode 在不同裝置上的設定

## setting.json 設置

```json
{
  "explorer.confirmDelete": false, // 刪除檔案不重複確認
  "editor.fontSize": 14, // 字體大小
  "terminal.integrated.fontSize": 14,
  "editor.tabSize": 4, // 一個 tab 的空白間隔
  "files.autoSave": "afterDelay", // 自動儲存檔案
  "editor.formatOnSave": true, // 存檔時，自動格式化代碼
  "editor.formatOnPaste": true, // 貼上程式碼時會自動幫你排版
  "files.insertFinalNewline": true, // 在檔案最後自動加入斷行
  "editor.wordWrap": "on", // 隨編輯視窗大小調整程式碼長度
  "prettier.semi": false, // 語末不加分號
  "prettier.singleQuote": true, // 強制單引號
  "prettier.printWidth": 80, // 調整程式碼寬度上限
}
```

## Settings Sync 能做什麼

* 透過 GitHub 帳號和 Gist 來同步設定檔
* 快速上傳或下載設定檔
* 啟動 VSCode 就自動更新設定檔
* 透過 Gist 可以將設定檔分享他人

> 開始 Settings Sync 的前置作業

### 建立 GitHub access token

Settings Sync 需要使用你的 GitHub 以及 Gist，所以還沒有 GitHub 帳號的話，趕緊去 [這裡](https://github.com/) 申請一個帳號，再回來繼續操作。

接著到你的 GitHub 帳號後，從大頭貼鍵號找到 Settings > Develop Settings > Personal access token > Generate New Token

在 Note 打上自己清楚的描述名稱，我稱為 VSCode_SyncSetting，如圖。

![vscode_settingsync](/images\posts\post_syncsetting.png)

接著按下方的綠色 Generate token 按鈕建立，會跳出一串 token 不要急著關掉，這組要複製下來留好，離開畫面就找不到了

![token](/images\posts\post_token.png)

### 首次上傳設定檔

VSCode 安裝了 Settings Sync 這個套件後，只要記住兩個快速鍵

* 上傳：shift + option(Alt) + U
* 下載：shift + option(Alt) + D

> 這兩個快捷鍵，日後也可以設定為自動同步，後面會說明

有了 Token 就可以來進行設定檔同步作業，先按下 Shift + Alt + U，第一次操作時 VSCode 會詢問你的 Github access token。

![upload_token](/images\posts\post_upload_token.png)

輸入剛剛複製的 access token 後就設定完成，Settings Sync 也會開始將設定檔上傳至 Gist，完成後會出現上傳完成通知。

![gistID](/images\posts\post_gistID.png)

這個 Gist ID 請把它記下來，後續要讓另一台電腦下載設定檔就需要這個 Gist ID。

> 可以將 token 和 Gist ID 存放一起，Gist ID 弄丟沒關係，只要到你的 VSCode 的 `setting.json` ，就能看到剛剛 Settings Sync 所上傳過留下的 "sync.gist"，這個就是你的 Gist ID。

![setting.json](/images\posts\post_setting-json-gistID.png)

### 下載設定檔

> 下載的動作就簡單多了

換到另一台電腦，一樣在 VSCode 先安裝 Settings Sync 套件，然後按下 Shift + Alt + D，此時一會詢問你的 Github access token，接著再詢問你的 Gist ID，紛紛貼上後，等待下載安裝即可。

### 自動同步設定

打開 VSCode 設定檔，輸入

``` bash
"sync.autoDownload": true,
"sync.autoUpload": true,
```

這兩行的意思就是每次 VSCode 有更新的套件或是設定，settings sync 就會自動上傳，這邊要注意的是要同步更新的電腦也要加入這這兩行程式碼，當然如果你只想要以某 A 電腦的上傳為主，B 電腦就只要設定 `"sync.autoDownload": true` 即可。

![setting auto DU](/images\posts\post_sync-setting-auto-U-D.png)

> 這邊我使用 `false` 這是因為我想避免有些設定我只是暫時使用，並不需要同步到其他裝置。
