---
title: 【NN 筆記】 Keras implementation of RetinaNet
tags:

    -NN

---
以下實作基於 GitHub 作者 fizyr 的 keras-retinanet 實現過程，詳細說明可以參考 [原文](https://github.com/fizyr/keras-retinanet)，以下紀錄實作過程中碰到的問題和解決方式，以及使用的環境。

### 環境

* OS: Win10 pro
* GPU: 1060 6G
* TF-GPU: 1.10.0
* keras: 2.0.5

### install

安裝好自己硬體配置的 tensorflow 環境後依照下面步驟

#### 安裝相關套件

numpy 安裝請用以下指令

``` bash
pip install numpy --user
```

接著在 `setup.py` 的目錄執行下面命令

```bash
pip install . --user
```

```bash
python setup.py build_ext --inplace
```

以上兩行指令執行過程中，如果跳出 `error: Microsoft Visual C++ 14.0 is required` 的訊息請到
[Visual C++ 2015 Build Tools](http://go.microsoft.com/fwlink/?LinkId=691126&fixForIE=.exe.) 安裝 C++相關套件，因為 windows 大多沒有預設安裝，安裝完成後再次執行 `pip install . --user`

#### 執行 ResNet50RetinaNet.py

到 example 目錄下執行命令

```bash
python ResNet50RetinaNet.py
```

執行成功顯示如下圖

![](https://i.imgur.com/zcceIDc.png)

接著，我們開啟 ResNet50RetinaNet.ipynb 這支 jupyter notebook 的檔案，這邊我直接用 vscode 開啟，如下圖

![](https://i.imgur.com/CxrrvCv.png)

我們先 Run 第一個 cell 看看，點擊左上角綠色開始按鈕，如圖
![](https://i.imgur.com/DEgnPQj.png)

如果碰到下圖錯誤，表示 `pip install . --user` 沒有執行完全，請到此 [步驟](#安裝相關套件)看看

![](https://i.imgur.com/6upVaRx.png)

如果成功執行但是有一些如下 `WARNING` 可以忽略不要緊

![](https://i.imgur.com/robyXOC.png)

接著，在執行下一段之前，先到 [這裡](https://github.com/fizyr/keras-retinanet/releases) 安裝 models，如下圖

![](https://i.imgur.com/Dkpz3FM.png)

存放位置請放在 `keras-retinanet\snapshots` 底下

![](https://i.imgur.com/3dG2zNy.png)
![](https://i.imgur.com/hQFuoZL.png)

下載好後，可以 Run 看看這個 cell，成功後還是會有很多警告，這些大部分是版本和建議替代方案的警告，我們先確定整個代碼可以 run，在修改版本即可

![](https://i.imgur.com/KSgW2cX.png)

最後，他預設了一張 `test data` 給我們做測試，如下圖

![](https://i.imgur.com/praBYWN.jpg)

按照該網路架構我們能判別圖片中的人物、領帶等等物件，我們就來 Run 看看，第一張圖可以看到我們的過程花費約 7.8 秒

![](https://i.imgur.com/Pq8Zv5N.png)

第二張圖可以看出各物件以及其準確度

![](https://i.imgur.com/X4c9DtP.jpg)

#### 結論

可以看出來與作者的結果有些微差異，這部有可能因為在過程中出現的版本或是硬體差異，而對結果有一些不同，可以試著改善這些警告或許會有更佳的表現
