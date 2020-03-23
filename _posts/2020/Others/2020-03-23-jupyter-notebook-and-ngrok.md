---
title: jupyter notebook & ngrok 外部網路存取
tags:

    - jupyter notebook
    - ngrok
---

利用 ngrok 解決 jupyter notebook 無法透過外部網路存取的問題

## jupyter notebook 遠端連線

我們要做的流程是：
1. 為 jupyter notebook 設定允許遠端連線
2. 透過 ngrok 來做外部網路轉發

### jupyter notebook 相關配置

輸入指令，跳出訊息如下圖

```bash
jupyter notebook --generate-config
```

![jupyter notebook](https://i.imgur.com/RF1Rss3.png)

建立遠端連線的訪問密碼

```bash
 jupyter notebook password
```

輸入自己密碼並確認，如下圖

![jupyter notebook](https://i.imgur.com/rUtaWJX.png)

到上圖產生密碼的 `.json` 路徑，將如下密碼複製

```bash
sha1:67c9e60bxxxx:9ffedxxxxx894254b2e042eaxxxxx71089xxxaed
```

![sha1](https://i.imgur.com/Ek0dwIS.png)

該路徑下有看到 `jupyter_notebook_config.py` ，將其打開找到下列被註解的程式碼並修改

```bash
c.NotebookApp.ip='*' #表示任何地方的 IP 可連線
c.NotebookApp.password = u'sha:67... 上面複製的密碼' #將其貼上
c.NotebookApp.open_browser = False #遠端是否打開瀏覽器
c.NotebookApp.port =8888 #要訪問的 port
```

完成後，在遠端機器輸入 `jupyter notebook` ，保持啟動 server 啟動，接著在本地機器輸入 `IP:port` 然後輸入自行設定的訪問密碼即可

### ngrok 相關配置

首先，註冊 [ngrok](https://dashboard.ngrok.com/get-started) 並下載 `ngrok` ，並且按照步驟 1-3 完成。

> windows 用戶可能會碰到 `./ngrok 無法辨識` 等等的問題，如下圖

![ngrok](https://i.imgur.com/BtIJeMx.png)

這是因為在該目錄下沒有找到解壓縮後的 `ngrok.exe` ，因此只要把 `ngrok.exe` 移動到常用的目錄下即可，在這邊我移動到 `C:\Users\(username)` 底下，因為這是終端機預設目錄，要執行 `ngrok` 命令我就不用切換目錄，如下圖

![ngrok](https://i.imgur.com/4ozw5Ro.png)

接著，再次執行步驟 3 的 `./ngrok authtoken <YOUR_AUTH_TOKEN>` 就沒有問題了！最後利用 `./ngrok http (yourport)` 就可以產生能外部網路訪問的連結了！
![ngrok](https://i.imgur.com/Br3nYvQ.png)

### jupyter notebook 小撇步（選用）

如果你跟我一樣，有建立一個獨立給 jupyter notebook 開發的 workspace 目錄，不想要每次開啟時都要切換目錄，可以將 jupyter notebook 的預設路徑做更改，我們打開上面有看到的 `jupyter_notebook_config.py` ，用快速搜尋 (Ctrl+F) 找到 `c.NotebookApp.notebook_dir` 這行命令，取消註解 (#)，並將路徑改為你要的目錄，如下圖

![jupyter noteboo](https://i.imgur.com/4REQdeh.png)

以上就完成外部網路存取 jupyter notebook!

> ngrok 的缺點就是每次的啟動外部連結都會改變，所以比較適合做一些小 demo 和開發測試喔！
