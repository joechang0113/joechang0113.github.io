---
title: 【Windows 筆記】印表機多工緩衝問題 - 提示"需要注意"
tags:

    - Windows

---
印表機影印常常會使用多工緩衝處理，來加快影印的速度，有時候資料送出的時間差會造成緩衝資料的衝突導致印表機影印異常，顯示 `需要注意` 的狀態

## 解決方式

按下 `Win + R` 打開執行命令欄，輸入 `services.msc`

![Image](https://i.imgur.com/wKnmKgk.png)

此命令會打開電腦中正在執行的服務，在眾多服務中找到名為 `Print Spooler` 的服務，然後 `右鍵` 選擇停止

![Image](https://i.imgur.com/MAu4gSD.png)

停止後，在將其重新啟動

![Image](https://i.imgur.com/zkrITab.png)
