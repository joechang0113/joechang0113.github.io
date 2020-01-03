---
title: 【Ubuntu 筆記】 安裝 Oh-My-Zsh
tags: [Ubuntu, Zsh]
---
一直以來看到很多人推薦用 zsh (z shell)，有興趣了解原因，可以看看其他文章。今天將剛灌完的 ubuntu 系統把 shell 從 bash 轉移到 zsh，順便紀錄給有興趣裝 zsh 的人。

## 相關更新

首先，如果 ubuntu 系統是剛灌完，建議利用下面兩步驟先更新一下，如果是舊玩家直接跳過這一步驟進入 zsh 基本安裝即可

``` bash
sudo apt-get update
sudo apt-get upgrade
```

## zsh 基本安裝

打開終端機 （Ctrl+Alt+t）預設啟用的是我們常見的 Bash Shell

``` bash
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

接著需要安裝 zsh

``` bash
sudo apt-get install zsh
```

> oh-my-zsh 就是基於此 shell 之上運作的，需要安裝 zsh 也合情合理

安裝完後，輸入指令查看成功與否

``` bash
$cat /etc/shells
```

![cat_shell](https://i.imgur.com/3p8xsuS.png)

> 列出來的內容有看到最下方兩個 zsh 相關路徑表示安裝成功

接著安裝 oh-my-zsh，可以用 curl 或 wget 兩種方式安裝（本文以 wget 安裝），輸入

``` bash
$sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

安裝完成後會直接進入 oh-my-zsh 的歡迎畫面

![welcome_ohmyzsh](https://i.imgur.com/8Om3CM3.jpg)

到這邊基本上已經安裝完成了，接著我們修改一下配置使它更加方便

## oh-my-zsh 配置修改

如果到上面你不小心關掉畫面，再次打開可能會發現 shell 依然還是原本的 Bash Shell，可以選擇每次進入時輸入 `zsh` 指令來進入 oh-my-zsh 但是這樣過於麻煩，所以我們使用以下指令將其預設 shell 改為 zsh

``` bash
chsh -s /bin/zsh
```

然後把電腦登出再登入或是重開機，再次開啟 Terminal 就可以看到自動進入 oh-my-zsh 了，此時開啟會如下圖

![zsh original](https://i.imgur.com/bOvJfdz.png)

## 主題修改

接著我們要設定自己喜歡的主題，可以從 [官方提供的主題](https://github.com/ohmyzsh/ohmyzsh/wiki/External-themes) 中挑選喜歡的主題使用

我選的是 bullet-train 這個主題，效果如下

![bullet-train.gif](https://i.imgur.com/AIu2gWu.gif)

> 選好主題後，點選主題下方的 See [Repo](https://github.com/caiogondim/bullet-train.zsh) for source 的連結，進入該主題的 github 專案，複製其 `clone or download` 連結

接著打開 terminal，輸入 `git clone (your link)` ，如下

``` bash
git clone https://github.com/caiogondim/bullet-train.zsh.git
```

> 如果你也想要用 bullet-train 這個主題，可以直接複製上方命令即可，如果是自己挑選得主題，記得換掉 `https://github.com/caiogondim/bullet-train.zsh.git`

clone 完畢後，如下圖

![bullet_train_folder](https://i.imgur.com/0iS9eP2.png)

打開資料夾可以看到內容有

![folder_in](https://i.imgur.com/dPL4XLX.png)

先將 `bullet-train.zsh-theme` 這個檔案複製

![bullet-train.zsh-theme](https://i.imgur.com/162PxEY.png)

然後打開一個新 terminal，輸入

``` bash
nautilus ~/.oh-my-zsh/themes
```

> nautilus 是打開資料夾的指令，themes 是存放 oh-my-zsh 主題的資料夾，接著應該知道剛剛複製的檔案要乾麻了，沒錯！直接貼到資料夾裡面

![bullet_train in folder](https://i.imgur.com/Kq9nGoe.png)

> 上圖最下方可以看到 bullet-train.zsh-theme，資料夾中有眾多主題，使用列表呈現可以查看並確定是否有你的主題

確定主題成功貼入後，開啟 `.zshrc` 檔案，來做主題修改的動作

* VSCode 請輸入

``` bash
code ~/.zshrc
```

* nano 請輸入

``` bash
sudo nano .zshrc
```

> 其他編譯器可自行尋找相關開啟指令，以下用 VSCode 示範

開啟後如下圖最下方，修改 `ZSH_THEME="robbyrussell"` 為 `ZSH_THEME="bullet-train"`

![vscode change bullet train](https://i.imgur.com/elbR28Z.png)

接著另外新開一個 terminal 可以看到如下圖

![bullet train without powershell](https://i.imgur.com/1C1XlJf.png)

> 此時會發現看起來很像亂碼，那是因為這些主題是用特別的字形去做類圖樣的覆蓋，我們只需要使用相對應字形就可以解決這個問題

## 嵌入字形

依序輸入

``` bash
sudo apt-get install powerline
sudo apt-get install fonts-powerline
```

最後重新開啟 terminal 可以看到如下圖效果，表示成功安裝完成了

![terminal with bullet train](https://i.imgur.com/Sl2jnhc.png)

## VSCode 亂碼

Terminal 解決了亂碼問題 VSCode 也需要校正，另開 terminal，輸入

``` BASH
cd /usr/share/fonts/truetype/
sudo git clone https://github.com/abertsch/Menlo-for-Powerline.git
sudo fc-cache -f -v
```

打開 `setting.json` 加入下方 code

``` js
// The path of the shell that the terminal uses on Linux.
"terminal.integrated.shell.linux": "/bin/zsh",
"terminal.integrated.fontFamily": "Menlo for Powerline",
```
