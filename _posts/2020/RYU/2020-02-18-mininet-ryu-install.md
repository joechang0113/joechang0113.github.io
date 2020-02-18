---
title: 【SDN 筆記】 Mininet 介紹與 RYU 相關安裝
tags:

    - SDN

---

 根據 mininet 官方網站的說法，mininet 是一個執行在 Linux 平台中的網路拓墣模擬器，可以同時產生多個虛擬主機 / 交換機 / 控制器，並將其串接起來，由於其交換機支持 OpenFlow 的協定，更有助於軟體定義網路（SDN, Software Defined Networking）的模擬環境開發，建立了 mininet 環境可以利用 ryu 框架來實現 SDN，根據 ryu 官方網站的說法，ryu 提供了軟體定義網路 (software defined networking) 一個很好的開發框架，其支援許多的 API 和協定，如此一來不僅是在網路管理或應用開發層面，都會方便許多，下面從零開始，搭建相關環境。

## VirtualBox & Ubuntu

在 windows 上開發需要虛擬機，這邊安裝常用的 VB(VirtualBox)，請到 [官網](https://www.virtualbox.org/) 先安裝，接著我需要在虛擬機上安裝 Linux 系統，也就是 ubuntu，一樣到 [官方載點](https://www.ubuntu-tw.org/modules/tinyd0/) 進行下載，本文使用 `64 位元 16.04LTS 桌面版本` ，下載完畢後，請依照 [這裡](https://blog.xuite.net/yh96301/blog/432341564-VirtualBox+5.2%E5%AE%89%E8%A3%9DUbuntu+16.04) 將 ubuntu 燒錄至 VB，完成後就可以繼續下一步。

## Mininet 介紹與相關安裝

先更新 ubuntu 環境，然後執行 `reboot` 重啟，依序執行下面三個命令

``` bash
sudo apt-get update
sudo apt-get upgrade
reboot
```

安裝 git 工具

``` bash
apt-get install git
```

利用 `git clone` 下載 `mininet` 安裝檔

``` bash
git clone git://github.com/mininet/mininet
```

到目錄下執行 mininet 安裝檔進行安裝，請依序執行下面兩個命令

``` bash
cd mininet/util/
./install.sh -a
```

安裝完畢看到如下圖顯示 Enjoy Mininet!

![](https://i.imgur.com/wyjbw36.png)

接著測試一下 mininet，先查看版本

``` bash
mn --version
```

如下我的版本為 `2.3.0d6`

![](https://i.imgur.com/5jrLc6P.png)

然後測試 mininet 是否可以與 controller、host 等等的虛擬機溝通

``` bash
sudo mn --test pingall
```

如下圖，看到`completed in 5.730 seconds`就是成功，秒數會不盡相同，沒有關係

![](https://i.imgur.com/MuoLgU2.png)

## RYU 介紹與相關安裝

安裝 python 相關工具，依序執行下面三個命令

``` bash
cd ~
sudo apt-get install python-pip
sudo apt-get install python-setuptools
```

安裝 RYU，依序執行下面四個命令

``` bash
pip install ryu
git clone git://github.com/osrg/ryu.git
cd ryu/
sudo python ./setup.py install
```

執行完會如下圖，出現兩個 `installing`

![](https://i.imgur.com/33pNyjG.png)

安裝完成後，執行 mininet，以下步驟請銜接 [RYU 說明文件-執行 Mininet](https://osrg.github.io/ryu-book/zh_tw/html/switching_hub.html#mininet) 中的內容。

首先， 開 `ssh` 的 `X11 Forwarding` 功能並進行登入。

``` bash
ssh -X <yourhostname>@<yourIP> # ssh -X joe@10.0.2.15
```

> hostname 就是你 terminal 打開後 `@` 前面的名稱，IP 請用 `ifconfig` 進行查詢，如下圖

![](https://i.imgur.com/jaOyMuc.png)

執行並輸入你自己登入的密碼後如下圖

![](https://i.imgur.com/6JxFXDx.png)

接著按照說明文件執行，輸入

``` bash
sudo mn --topo single,3 --mac --switch ovsk --controller remote -x
```

執行之後，會在 x windows 出現 5 個 xterm 視窗。 分別對應到 host 1 ~ 3 ，交換器和 Controller ，如下圖

![](https://i.imgur.com/dnoLCn2.png)

依序按照說明文件在 `switch:s1(root)` 視窗執行下面四個命令

``` bash
ovs-vsctl show
ovs-dpctl show
ovs-vsctl set Bridge s1 protocols=OpenFlow13
ovs-ofctl -O OpenFlow13 dump-flows s1
```

都沒有輸入錯誤應該呈現如下

![](https://i.imgur.com/2jkEcbQ.png)

## 執行交換器

切換到 `controller:c1(root)` 視窗，依序輸入下面三個命令

``` bash
cd ryu/ryu/app/
ls
ryu-manager --verbose ryu.app.simple_switch_13.py
```

> 第一行是切換到 `simple_switch_13.py` 路徑
> 第二行是查看是否有該檔案
> 第三行就是說明文件中的執行

最後執行成功如下圖，這個訊息表示，controller 已經待命在準備 host 與 switch 的溝通。

![](https://i.imgur.com/bw6b1sM.png)
