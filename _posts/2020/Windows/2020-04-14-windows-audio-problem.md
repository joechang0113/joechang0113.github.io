---
title: 【Windows 筆記】W10 主機前面板的音源失效
tags:

    - Windows

---
重灌 win10 系統後，發現插在前面板音緣孔的耳機沒有辦法使用，後置面板的喇叭正常，有很多文章使用刪除 `Realtek` 驅動的相關方法，測試後時好時壞，W10 容易重新抓回驅動，這邊嘗試另一種方法。

## 解決辦法

打開 `控制台` ，點選 `硬體與音效`

![](https://i.imgur.com/IdZACaz.png)

開啟 `瑞昱高傳真音效管理`

![](https://i.imgur.com/oqcp83F.png)

點選右上角的齒輪來打開 `選擇`

![](https://i.imgur.com/Pfn6a4u.png)

將下方的 `錄音裝置` 選項，改為各自獨立

![](https://i.imgur.com/WUsMn4E.png)

這樣就能抓到前版耳機了
