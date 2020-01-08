---
title: 【macOS 筆記】Jekyll 本地預覽
tags:

    - macOS
    - Jekyll

---
先前介紹過 [windows 設定](https://joechang0113.github.io/2020/01/03/windows-use-ruby.html)，在 macOS 上進行相關環境建置有些許不同，做個紀錄

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
