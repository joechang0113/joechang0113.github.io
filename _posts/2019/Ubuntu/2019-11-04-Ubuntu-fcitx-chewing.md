---
title: 【Ubuntu 筆記】使用 fcitx chewing 新酷音輸入法
tags: Ubuntu
---
Ubuntu 下 fcitx 輸入法架構比預設的 ibus 穩定許多，這邊分享如何安裝與設定

## 安裝 fcitx 語系

安裝 fcitx （框架） 以及 fcitx-chewing （框架下的新酷音輸入法）：

``` bash
 sudo apt-get install fcitx fcitx-chewing
```

按照步驟設定：

1. 設為預設輸入法架構： System Settings > Language Support > Language Tab > Keyboard input method system: set to fcitx

2. 讓每個程式獨立維持輸入法狀態： System Settings > Keyboard > Typing Tab > Click on Text Entry > Select Allow different sources for each application

3. citx 設定沒事別跳出選字框： 右上角工具列 fcitx 鍵盤圖示 > Configure > Global Config > Click Show Advance Option > Appearance > Do not show input window if there is only preedit string

4. 下載 Gist 圖示，取代原本新酷音古板圖示，符合 Ubuntu Ambiance 主題風格：

Gist-icon:

> 右鍵另存圖檔

![fcitx-chewing.png](/assets\images\posts\fcitx-chewing.png)

> 注意記住自己下載檔案的位置在哪裡，這邊我下載到 Download 資料夾內

到自己下載的路徑

``` bash
cd Download/
```

輸入以下指令將 icon 複製到以下路徑（手動複製也可以）

``` bash
sudo cp fcitx-chewing.png /usr/share/icons/hicolor/48x48/apps/fcitx-chewing.png
```
