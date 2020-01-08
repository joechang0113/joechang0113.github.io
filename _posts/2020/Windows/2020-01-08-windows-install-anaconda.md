---
title: 【Windows 筆記】 Anaconda Install
---
本篇介紹在Windows 10 下安裝Anaconda 環境

### 安裝 Anaconda

進入 [Anaconda 官網](https://github.com/andy6804tw/machine-learning/blob/master/0-introduction)後選取你的系統，並下載安裝檔。若本身有安裝 Python 的朋友建議先移除原先所安裝的 Python 因為安裝 Anaconda 時會自動另外幫你安裝 Python。因此為了避免衝突還是建議讀者先移除舊有版本。

![Image](https://i.imgur.com/J3Yb1kv.png)

基本上一直點選下一步選取預設安裝即可。

![Image](https://i.imgur.com/GdUJOcM.png)

![Image](https://i.imgur.com/vTOrXd9.png)

安裝完成後可以開啟命令提示字元(CMD)或是任一個你習慣的終端機(Terminal)，並輸入 `python` 查看是否有成功安裝好 Python 以及 Anaconda。若有安裝成功則會跟下圖一樣的結果。進入這個畫面後使用者就可以直接在終端機撰寫 Python 程式語言並立即執行成果。

![Image](https://i.imgur.com/utlSxVJ.png)

若出現 python 不是內部或外部命令、可執行的程式或批次檔 的朋友別緊張，可能只是系統尚未成功設定環境。這時必須手動來新增環境變數。手先開啟本機->右鍵內容->進階系統設定

![Image](https://i.imgur.com/MpN5cdn.png)

接著會跳出系統內容的視窗，找到進階->環境變數

![Image](https://i.imgur.com/4rS3uax.png)

接著下方的系統變數欄位中尋找 `Path` 並點選編輯

![Image](https://i.imgur.com/RQk4RCq.png)

接著點選新增，再把系統安裝 Anaconda 的資料夾位置貼上即可，通常預設為C碟。

![Image](https://i.imgur.com/ASFMXg4.png)

一切就緒後就可以啟動 Anaconda，可以在terminal輸入`conda`查看是否有下列訊息

![Image](https://i.imgur.com/mxO5qQc.png)

有的話，就沒有問題可以開始使用相關工具囉!如果有出現錯誤不妨看看上面有沒有步驟漏掉!