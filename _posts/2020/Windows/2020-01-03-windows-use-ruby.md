---
title: 【Windows 筆記】 Jekyll 本地預覽
tags:

    - Windows
    - Jekyll

---
blog 使用 Jekyll 建立，所以在 windows 上進行相關環境建置。紀錄一點心得和碰到的錯誤並分享解決的方法，使用 macOS 的朋友可以參考 [這裡](https://joechang0113.github.io/2020/01/03/macos-use-ruby.html)

## 安裝 Ruby

到 [下載地址](https://rubyinstaller.org/downloads/) 下載並安裝
選擇第一個 with devkit 的 64 位元版本（除非你電腦 32 位元）

![img](https://i.imgur.com/F9HTRoG.png)

添加環境路徑

![RUBY 安裝](https://i.imgur.com/6yUAb03.png)

安裝完成後出現 MSYS2 setup

![img](https://i.imgur.com/TMtd5Ot.png)

點選 finish，跳出 ruby installer for windows

![img](https://i.imgur.com/74ssNCv.png)

這邊直接按 enter 進入安裝，安裝完成後同樣的指令會再問你一次，直接按 Enter 自動跳離 terminal

## 安裝 Jekyll

> 安裝 Jekyll 之前請先將 VSCode 等等的編譯器或是 terminal 重新開啟在執行以下動作

輸入

``` bash
gem install jekyll
```

![img](https://i.imgur.com/jqpq4aU.png)

切換到 blog 目錄下，查看是否有 `Gemflie` 文件

![img](https://i.imgur.com/tsb6MmY.png)

且內容如下

``` bash
# frozen_string_literal: true
source "https://rubygems.org"
gem "github-pages", group: :jekyll_plugins
```

如果沒有以上文件，自行創建，並貼上內容程式碼
輸入

``` bash
gem install bundler
```

![img](https://i.imgur.com/UxYD798.png)

接著輸入

``` bash
bundler install
```

![img](https://i.imgur.com/lQ5p7mH.png)

接著輸入

``` bash
jekyll s
```

出現錯誤

![img](https://i.imgur.com/JElhvG5.png)

找了解決辦法，輸入

``` bash
bundle exec jekyll s
```

卻出現這錯誤

![img](https://i.imgur.com/YmvSq6A.png)

這是因為模板預設系統時間的問題，我們到 `Gemfile` ，加入這行指令

``` bash
gem 'tzinfo-data', platforms: [:x64_mingw,:mingw, :mswin]
```

像這樣

![img](https://i.imgur.com/qzqvv9J.png)

再次執行

``` bash
bundle exec jekyll s
```

可以運作了，但是可以看到圖中黃字訊息

![img](https://i.imgur.com/KEOBKZL.png)

查了一下，這是個警告不是 error 雖然可以運作，但是避免養虎為患，找了解決辦法
將下面指令加入 `_config.yml`

``` bash
github: [metadata]
```

> 要 Push 前記得 comment 掉

加入後如圖

![img](https://i.imgur.com/wST7JwB.png)

在執行一次

``` bash
bundle exec jekyll s
```

![img](https://i.imgur.com/02aTKj1.png)

搞定，完美執行，如果你跟我一樣用 VSCode， `Ctrl` 按住點 server address 連結 `http://xxx.xxx.xx` ，就能開啟 Blog 離線預覽
