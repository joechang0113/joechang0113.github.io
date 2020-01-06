---
title: 【Windows 筆記】 Windows 下打造 TensorFlow 環境
tags: [Windows]
---
工欲善其事，必先利其器，機器要學習，定需好環境。之前介紹在 Ubuntu 系統安裝，這次在 Windows 也快速利用 Anaconda 建立 Tensorflow 環境

## Anaconda 建立 Tensorflow 環境

至 [Anaconda 官網下載點](https://www.anaconda.com/distribution/) 下載所需版本（這邊使用 Python3.7)。

> 下載後詳細安裝步驟請參考此 [頁面](https://www.woodowlab.com/python-tutorial-0-anaconda/)

![Anaconda DL](https://pic.pimg.tw/kk665403/1541065448-12595397_n.png)

叫出終端機 (cmd)，輸入指令 `conda --version` 查看 conda 版本。

> 叫出終端機的方式可參考此 [頁面](https://parg.co/WuR)

如下圖顯示出 conda 版本表示安裝成功（版本或許不同）

![Imgur](https://i.imgur.com/qxp38jL.png)

輸入指令 `conda create --name tensorflow python=3.6` 建立一虛擬 python 環境用以搭建 TensoFlow。

> 詳細步驟可以至此 [頁面](https://parg.co/iqF) 學習

輸入指令 `conda env list` 來查看是否將 tensorflow 虛擬環境建立成功。

> 如下圖有顯示 tensorflow 就成功建立此虛擬環境

![Imgur](https://i.imgur.com/BvQqV7M.png)

輸入指令` ` ` activate tensorflow ` ` `激活 tensorflow 環境。

> 如下圖使用者名稱前方顯示 tensorflow 表示激活成功

![Imgur](https://i.imgur.com/zcxdQ8A.png)

輸入指令 `conda install tensorflow-gpu==1.10.0` 安裝 tensorflow-gpu（這邊只適用電腦有顯示卡 (GPU) 的使用者）。

輸入指令 `pip install keras==2.0.5` 安裝對應於 **tensorflow 版本 1.10.0** 的 **keras 版本 2.0.5**

輸入指令 `conda list` 查看所安裝的 tensorflow 和 keras 是否完成安裝

> 如下圖顯示其 package 名稱以及對應的版本表示安裝完成

![Imgur](https://i.imgur.com/suRBprH.png)

![Imgur](https://i.imgur.com/4lg8ag4.png)
