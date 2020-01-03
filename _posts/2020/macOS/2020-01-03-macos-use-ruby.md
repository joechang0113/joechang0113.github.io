---
title: 【macOS 筆記】macOS 下安裝 Jekyll
tags: [macOS, Jekyll]
---
目前使用的個人電腦是 macOS (macOS Catalina 版本 10.15.2)，因此在 macOS 上安裝 Jekyll 進行相關環境建置。在這邊紀錄一點心得和碰到的錯誤並分享解決的方法

## 安裝 Ruby

輸入

``` bash
brew install ruby
```

![install ruby](https://i.imgur.com/srT8wtW.png)

輸入

``` bash
bundle install
```

![bundle install](https://i.imgur.com/sUG6bPb.png)

## 安裝 Jekyll

``` bash
gem install jekyll bundler
```

![gem install](https://i.imgur.com/eIJrSzW.png)

輸入

``` bash
bundle exec jekyll s
```

如下，成功執行

![run jekyll s](https://i.imgur.com/bH3vo3Z.png)

按住 command 鍵，點擊連結開始預覽
