---
title: 【Ubuntu 筆記】 Ubuntu 下打造 Tensorflow 環境
tags: [Ubuntu, TensorFlow]
---
工欲善其事，必先利其器，機器要學習，定需好環境。本文介紹如何使用 Anaconda 建立 Tensorflow 環境

## 硬體環境

OS: Ubuntu16.04
CPU: I7 8700k
GPU: 1080ti

## 下載並安裝 Anaconda

[官方網站](https://www.anaconda.com/distribution/) 下載 Anaconda（無特別需求直接下載 3.7)

![Imgur](https://i.imgur.com/8YWWT2a.png)

然後使用以下指令安裝 Anaconda 的 `.sh` 安裝檔案

``` bash
bash ~/Downloads/Anaconda3-2019.10-Linux-x86_64
```

接著會看到以下訊息

``` bash
安裝過程中看到
Welcome to Anaconda3 2019.10
In order to continue the installation process, please review the license
agreement.
Please, press ENTER to continue
（不斷按 Enter 同意並繼續）
然后看到 Do you accept the license terms? [yes|no]（是否接受協議內容？
直接輸入 yes 進行安裝
Anaconda3 will now be installed into this location:
/home/aeasringnar/anaconda3 （提示安裝路徑）
\- Press ENTER to confirm the location
\- Press CTRL-C to abort the installation
\- Or specify a different location below
按 Enter 進行下一步，注意若按 ctrl + c 會直接終止安裝。
接下 Enter 先等待安裝即可。
```

> 最後看到 Thank you for installing Anaconda3! 表示安裝成功。

Anaconda 在安裝過程中會自動將環境變數添加到 PATH 里面如果下一階段操作錯誤，可以參考此 [連結](https://parg.co/WpE)

### 使用 `conda` 相關命令

查看 conda 版本

``` bash
conda --version
```

更新 conda

``` bash
conda update conda
```

新建名為 tesnsorflow-gpu 的 python3.6 虛擬環境

``` bash
conda create -n tensorflow-gpu python=3.6
```

> 名稱和 python 版本可以自訂，不確定就按照此版本
> >**怕造成誤會所以提個醒，雖然最初安裝的 anaconda 預設為 python3.7 但是透過 conda create 可以在系統建立一個 python3.6 的虛擬環境與之隔離互不影響**

啟用上述所建立的 tensorflow-gpu 環境，出現該字樣即成功

``` bash
source activate tensorflow-gpu
```

安裝 tensorflow-gpu，我們使用 GPU 所以安裝 gpu 版本，詳情見 [這裡](https://parg.co/WZK)

``` bash
conda install tensorflow-gpu==1.10.0
```

接著安裝 keras

``` bash
pip install keras==2.2.4
```

安裝完 keras 後，tensorflow 的環境大致上已經建立完成，剩餘所需 package 可依照個人所需安裝

---

### 可能需要的 package

* PIL

``` bash
conda install -c anaconda pillow
```

* sklearn

``` bash
conda install -c anaconda scikit-learn
```

* cv2

``` bash
pip install opencv-python
```

* keyboard

``` bash
pip install keyboard
```

> conda 和 pip 混用是因為有些 module 用 pip 來安裝需要解決的問題較少

## 可能的 Error 訊息

執行時碰到的一些錯誤，紀錄一下，有碰到夥伴可以試試看，解決方案如下：
在安裝 opencv 時，原先使用 `conda install opencv` 安裝，發生錯誤，移除後，改用 `pip install opencv-python` 可以解決
