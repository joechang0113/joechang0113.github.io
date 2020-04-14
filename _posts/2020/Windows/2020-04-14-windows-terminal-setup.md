---
title: 【Windows 筆記】Windows Terminal 使用與美化
tags:

    - Windows

---
之前有介紹過好用的 [Fluent Terminal](https://joechang0113.github.io/2020/03/23/windows-fluent-terminal.html)，這次介紹微軟自己的 `Windows Terminal` ，多了很多好玩的功能，透過 `.json` 的設定，可以自由的客製化，個人覺得可玩度比 `Fluent Terminal` 高！

## 官方宣傳影片

雖然現在還只是 `Preview` 版本，不過相信隨著更新會越來越好的，來看看官方的宣傳片

{% include youtube.html id="8gw0rXPMMPE" %}

安裝的環境有些限制，目前僅有 `W10 version 1903` 之後的版本可以相容各項功能，不確定自己版本，可以按下 `Win+R` 打開執行命令，輸入 `winver` 就有自己的 windows 版本號了，準備就緒後，我們就開始！

## 介紹

我們原本的 powershell 會長這樣

![Image](https://i.imgur.com/1IIAxZP.png)

我們要改造成這樣

![Image](https://i.imgur.com/YFvx4X5.png)

## oh-my-posh 安裝

打開 `PowerShell` 依序輸入兩行指令

``` bash
Install-Module posh-git -Scope CurrentUser

Install-Module oh-my-posh -Scope CurrentUser
```

> 問題全部都選 `是`

接著設定自動套用，在 `PowerShell` 上輸入 `$PROFILE` ，依序輸入下列兩行指令

``` bash
if (!(Test-Path -Path $PROFILE )) { New-Item -Type File -Path $PROFILE -Force }

code $PROFILE
```

> 第一行是有檔案的話就開啟，沒有自動新增

第二行是以 `VSCode` 打開

也可以直接到以下路徑新增檔案

```
C:\Users\[hostname]\Documents\WindowsPowerShell\
```

打開後，貼上下面程式

``` ps1
Import-Module posh-git
Import-Module oh-my-posh
Set-Theme Paradox
$DefaultUser = 'hostname' # your pc username，用來隱藏本機名
$ProgressPreference = 'SilentlyContinue' # 關閉 powershell 下載進度條
```

如果不斷出現如下圖錯誤

![Image](https://i.imgur.com/lKNpZjn.png)

請執行此命令

``` bash
Set-ExecutionPolicy RemoteSigned
```

## Windows Terminal 安裝

打開 Microsoft store

![Image](https://i.imgur.com/oXtQGGl.png)

搜尋 `terminal`

![Image](https://i.imgur.com/hFzHgQ8.jpg)

啟動後如下

![Image](https://i.imgur.com/3mPLkYG.png)

> 有些亂碼是正常的，因為字形還沒設定

## Powerline 字形安裝

到 powerline fonts 的 [github page](https://github.com/powerline/fonts) 下載字形包，建議直接下載 `zip`

![Image](https://i.imgur.com/jJHYXA7.png)

接著解壓縮並打開字形包，選擇自己要的字形（我用 `Source Code Pro for Powerline` 他放在 `SourceCodePro` 資料夾），將要得 `.otf` 檔案拖移到字形資料夾進行安裝

![Image](https://i.imgur.com/mGeKeU8.png)

最後，待一段時間，重啟 `windows terminal` 就完成了。

> 下面的設定，看個人需求進行

## 使用系統管理員開啟 Windows Terminal 分頁（選）

### 安裝 gsudo

輸入指令

``` bash
PowerShell -Command "Set-ExecutionPolicy RemoteSigned -scope Process; iwr -useb https://raw.githubusercontent.com/gerardog/gsudo/master/installgsudo.ps1 | iex"
```

過程中會詢問是否利用 `sudo` 取代 `gsudo` ，看個人，不影響最後使用

![Image](https://i.imgur.com/91Sy1nm.png)

接著，打開 windows terminal 的 setting，在 `list` 陣列中，貼上如下程式碼

``` js
{
  "guid": "{41dd7a51-f0e1-4420-a2ec-1a7130b7e950}",
  "name": "Windows PowerShell Elevated",
  "commandline": "gsudo.exe powershell.exe",
  "hidden": false,
  "colorScheme": "Solarized Dark",
  "icon": "https://i.imgur.com/Giuj3FT.png"
},
```

![Image](https://i.imgur.com/RWt3pgn.png)

## 加入右鍵選單（選）

我們希望在右鍵選單，可以快速開啟，如下圖

![Image](https://i.imgur.com/YleapRx.png)

首先，開啟 `cmd` 輸入以下兩個指令 ( `gitbash` 無效）

``` bash
echo %USERPROFILE%

echo %LOCALAPPDATA%
```

分別出現如下回應

![Image](https://i.imgur.com/Y0cglWM.png)

輸出有如上圖，就表示 `%USERPROFILE%` 有正確指向你的電腦目錄

> 如果輸出還是 `%USERPROFILE%` 以下操作請自行更改為您的絕對路徑

接著，需要建立一個 `Terminal` 資料夾，輸入

``` bash
mkdir "%USERPROFILE%\AppData\Local\Terminal"
```

> `%USERPROFILE%` 沒有正確指向的可以直接到該路徑新增，此路徑在隱藏目錄中，記得打開顯示

![Image](https://i.imgur.com/y1CjBjJ.png)

複製路徑 `%USERPROFILE%\AppData\Local\Terminal` ，然後下載 [icon](https://raw.githubusercontent.com/microsoft/terminal/master/res/terminal.ico) 到剛剛的 `Terminal` 資料夾（在資料夾路徑搜尋直接貼上複製的路徑）

![Image](https://i.imgur.com/1ub33TM.png)

在桌面新增一個 `txt` ，貼上以下內容，另存為名為 `addwt` 的 `reg` 檔

```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\Background\shell\wt]
@="Windows Terminal here"
"Icon"="%USERPROFILE%\\AppData\\Local\\Terminal\\terminal.ico"

[HKEY_CLASSES_ROOT\Directory\Background\shell\wt\command]
@="C:\\Users\\[yourhostname]\\AppData\\Local\\Microsoft\\WindowsApps\\wt.exe"
```

![Image](https://i.imgur.com/eJUGPbr.png)

直接執行該檔案，完成後，打開 `windows termianl` 的 setting，加入以下命令

``` js
"startingDirectory": null
```

![Image](https://i.imgur.com/rswI2G9.png)

完成

## 後記

如果不喜歡每次開啟 `Terminal` 都有 copyright 的介紹，可以在 `profile.json` 中，為每個 `cmd` 加入 `-nologo` 的指令，如下圖

![Image](https://i.imgur.com/i3hpQUv.png)

這樣開啟時，就不會有一堆無關訊息了！

![Image](https://i.imgur.com/BsO2Lgf.png)
