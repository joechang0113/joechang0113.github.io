---
title: Windows-FluentTerminal
---
macOS 和 Linux 在配置 shell 上都有很高的彈性也能打造出一個漂亮的效果，像是 macOS 的 iTerm2 & Oh-My-Zsh 搭配出來的效果，像是這樣

![Image](https://i.imgur.com/4BXtycS.png)

玩過 Cmder、Git bash、PowerShell 原生地 cmd 就不說了，無法滿足，於是找到了 [FluentTerminal](https://github.com/felixse/FluentTerminal)，這篇帶大家簡單安裝！
我們會完成的最終效果如下

![Image](https://i.imgur.com/4xq94rP.png)

## FluentTerminal 設定步驟

### Chocolatey 套件安裝

首先，在 windows 搜尋 powershell 並以系統管理員打開，接著輸入指令安裝 [Chocolatey](https://chocolatey.org/install)

![powerline](https://i.imgur.com/dXHF1ho.png)

``` bash
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1')); choco feature enable -n allowGlobalConfirmation
```

接著驗證版本已確認是否安裝完成

``` bash
choco -v
```

![Image](https://i.imgur.com/DaUN1TA.png)

利用 Chocolatey 安裝 FluentTerminal

``` bash
choco install fluent-terminal
```

如果出現如下圖中錯誤

![img](https://i.imgur.com/56IiBxb.png)

輸入以下指令，並輸入`A`執行

```bash
set-ExecutionPolicy RemoteSigned
```

### 安裝 oh-my-posh

上面我們安裝完 FluentTerminal，先將其打開之後操作都使用它完成，首先我們要安裝 oh-my-posh，不要懷疑，有 oh-my-zsh 當然有 oh-my-posh，他是一個強大的 powerline 主題，類似 Linux 下的 oh-my-zsh

相應的操作都在 oh-my-posh 的 [GitHub 官方文件](https://github.com/JanDeDobbeleer/oh-my-posh)，我直接貼出來，將其依序輸入進行安裝即可

``` bash
Install-Module posh-git -Scope CurrentUser
```

``` BASH
Install-Module oh-my-posh -Scope CurrentUser
```

安裝完畢後要進行相關配置，請依序輸入

``` bash
if (!(Test-Path -Path $PROFILE)) {New-Item -Type File -Path $PROFILE -Force}
```

```bash
code $PROFILE # 如果不是用 VSCode 請用自己的編輯器開（如 notepad)
```

打開後加入這四行

``` bash
Import-Module posh-git
Import-Module oh-my-posh
Set-Theme Paradox # 要用的 Theme
$DefaultUser = 'username' # your pc username，用來隱藏本機名
```
不知道 username 的朋友請按 `Win=R`，輸入`netplwiz`即可查看自己的 username

![Image](https://i.imgur.com/AVaHPuv.png)

貼上後如下圖

![Image](https://i.imgur.com/GsANGlQ.png)

## 設定字體與主題

### 字體安裝

跟 oh-my-zsh 一樣 oh-my-posh 也是利用依些特殊自行來美化這些 icon，所以我們要下載一些字體，這邊使用 Consolas NF，另外也有 [字體庫](https://github.com/powerline/fonts) 有興趣可以找找自己喜歡的

這邊我們直接到 [Consolas NF](https://github.com/whitecolor/my-nerd-fonts) 點選 Download ZIP 下載 zip 檔案到桌面

![Image](https://i.imgur.com/cs9by7e.png)

下載後，會是 my-nerd-fonts-master 資料夾，打開後接著點開 Consolas NF，會看到四個字形檔案

![Image](https://i.imgur.com/0vjqP6r.png)

接著到 `控制台、外觀及個人化、字型` 將這四個字形檔案丟進去

![fonts move demo](https://i.imgur.com/jst4kgp.gif)

### 主題安裝

首先到 [Argonaut](https://github.com/effkay/iTerm-argonaut/) 下載，一樣我們直接下載 zip 檔案到桌面

![Image](https://i.imgur.com/UhRvHgx.png)

解壓縮後，會看到 `iTerm-argonaut-master` 資料夾

### 設定 FluentTerminal

將剛剛下載的 Consolas NF 字形和 Argonaut 主題做配置

打開 FluentTerminal 點選左上角的選單，打開 Settings，選 Terminal，第一個選項 Font family 找到我們的 Consolas NF

![Image](https://i.imgur.com/7kwIMW6.png)

接著是主題配置，一樣 Settings 然後選擇 Themes，點選 import，到剛剛的路徑（桌面）將其導入

![Image](https://i.imgur.com/fdBHcDs.png)

然後記得勾選 argonaut 主題

![Image](https://i.imgur.com/p3gcL69.png)

順便將光標設定為下底線，才不會擋住自己打出來的命令，我們到 Settings 的 Terminal，將 Cursor style 選擇 Underline

![Image](https://i.imgur.com/nbIEFNd.png)

再重新啟動後就生效了！

## 關閉 powershell logo info

會發現打開的時候會跳出加載的時間和一些系統提示，這會拖慢開啟速度，也不美觀，我們做一些設定將其關閉，打開 FluentTerminal，到 `Settings` 點選 `Profiles` ，選擇 Powershell 並開啟右上角了 `Edit` ，在 Arguments 輸入 `-nologo`

![Image](https://i.imgur.com/weURH1m.png)

關閉 terminal 重新啟動 FluentTerminal，漂亮的 shell 搞定了！

![Image](https://i.imgur.com/7yiIiei.png)
