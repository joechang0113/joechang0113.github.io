---
title: 【Windows 筆記】 Windows10 安裝 Anaconda 環境
---
本篇介紹在 Windows 10 下安裝 Anaconda 環境

### 安裝 Anaconda

進入 [Anaconda 官網](https://github.com/andy6804tw/machine-learning/blob/master/0-introduction) 後選取你的系統，並下載安裝檔。若本身有安裝 Python 的朋友建議先移除原先所安裝的 Python 因為安裝 Anaconda 時會自動另外幫你安裝 Python。因此為了避免衝突還是建議讀者先移除舊有版本。

![Image](https://i.imgur.com/J3Yb1kv.png)

基本上一直點選下一步，但是到了是否加入 `path` 頁面時記得勾選。

![Image](https://i.imgur.com/xsqGWSq.png)

按下 `install` ，等待安裝完畢即可

![Image](https://i.imgur.com/GdUJOcM.png)

![Image](https://i.imgur.com/vTOrXd9.png)

安裝完成後可以開啟命令提示字元 (CMD) 或是任一個你習慣的終端機 (Terminal)，並輸入 `python` 查看是否有成功安裝好 Python 以及 Anaconda。若有安裝成功則會跟下圖一樣的結果。進入這個畫面後使用者就可以直接在終端機撰寫 Python 程式語言並立即執行成果，進一步使用 Anaconda 直接跳到 [啟動 Anaconda](#啟動Anaconda)。

![Image](https://i.imgur.com/Y86qfaY.png)

## 修正 `python` 命令錯誤

若出現 python 不是內部或外部命令、可執行的程式或批次檔 的朋友別緊張，可能只是系統尚未成功設定環境。這時必須手動來新增環境變數。首先到本機->右鍵內容->進階系統設定

![Image](https://i.imgur.com/MpN5cdn.png)

接著會跳出系統內容的視窗，找到進階->環境變數

![Image](https://i.imgur.com/4rS3uax.png)

接著下方的系統變數欄位中尋找 `Path` 並點選編輯

![Image](https://i.imgur.com/RQk4RCq.png)

接著點選新增，再把系統安裝 Anaconda 的資料夾位置貼上即可，通常預設為 C 碟。

![Image](https://i.imgur.com/ASFMXg4.png)

## 啟動 Anaconda

一切就緒後就可以啟動 Anaconda，可以在 terminal 輸入 `conda` 查看是否有下列訊息

![Image](https://i.imgur.com/Udn6ZVY.png)

有的話，就沒有問題可以開始使用相關工具囉！如果有出現錯誤不妨看看上面有沒有步驟漏掉！

## Anaconda 建立虛擬環境

簡單介紹一下 Anaconda 的虛擬環境建立，在一台電腦上難免需要不同的環境來開發，ROS 需要 python2，Tendorflow 需要 Python3，這時候虛擬環境就很重要。

首先，我們查看一下當前環境

``` bash
conda env list
```

可以看到顯示出 `base` 並且帶有一個 `*` ，代表目前處於 `base` 環境

![Image](https://i.imgur.com/Aunxw2d.png)

接著，假設我需要建立一個 `python2.7` 名稱為 `fordemo` 的虛擬環境，我需要輸入

``` bash
conda create --name fordemo python=2.7
```

他得到建立環境的指令後會詢問是否建立一些必要的 package 如下圖

![Image](https://i.imgur.com/gtrNJoI.png)

當然選'y'

建立完成後，在一次使用 `conda env list` 查看環境

![Image](https://i.imgur.com/dJj4H26.png)

有看到自己建立的 `fordemo` 就是成功了，但可以看到 `*` 還在 `base` ，接著我們要切換到這個 `fordemo` 環境

輸入

``` bash
conda activate fordemo
```

切換成功後會在命令列最前方看到 `(fordemo)`

我們輸入指令查看這個 `fordemo` 的 python 環境，輸入

``` bash
python
```

可以看到 python 環境不是當初 `base` 的 python3.7，而是我們建立 `fordemo` 的 `python2.7` ，如下

![Image](https://i.imgur.com/gVC45qG.png)
