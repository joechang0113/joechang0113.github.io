---
title: 【Windows 筆記】Windows 工具列時間加入秒數顯示
tags:
    - Windows
---
希望效果如下圖

![](https://i.imgur.com/j5jlPyV.png)

## 設定方法

打開`CMD`複製並貼上以下命令

```
reg add HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced /v "ShowSecondsInSystemClock" /t reg_dword /d 1 /f >nul 2>nul1
```

此時的時間為12小時制，如果想要24小時制，可以在時間點右鍵開啟`調整日期/時間`
![](https://i.imgur.com/ZP67dHu.png)

接著依序下圖點開設定

![](https://i.imgur.com/YpVdk6S.png)

![](https://i.imgur.com/h4dlcNy.png)

選取想要的格式即可
![](https://i.imgur.com/h5wqbOJ.png)
