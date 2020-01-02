---
title: 【SDN 筆記】 SDN、OpenFlow、Ryu 之間的關係
tags: [SDN]
---
以下說明一下在軟體網路定義(SDN)中，SDN、OpenFlow、Ryu 扮演的腳色以及他們之間是如何運作，若有興趣繼續深入探討，非常推薦研讀一下 [官方說明文件]([https://link](https://osrg.github.io/ryu-book/zh_tw/html/switching_hub.html#ryu))

## RYU

首先，Ryu 作為開發的框架目的是為了實現軟體定義網路（ Software Defined Networking, SDN ）。那麼為什麼要選擇 Ryu 作為開發平台呢？透過 SDN 、OpenFlow、Ryu 之間的關係逐一探討。透過實際的例子，如 Simple Switch 的實作，接著是流量監控（ Traffic Monitor ）以及網路聚合（ Link Aggregation ），將一一介紹 Ryu 的程式是如何運作的。透過 OpenFlow 通訊協定（ OpenFlow Protocol ）以及封包函數的使用方法。接著也會討論如何使用 Ryu 內建的防火牆（ Firewall ）和測試工具（ test tool ）來開發應用程式。最後基於 Ryu 的架構（ Architecture ）及實際應用案例釐清三者間的關係。

## SDN

SDN 並不等於 OpenFlow，它僅僅是 SDN 中控制器控制轉發面裝置的協議而已，控制器本身的架構、網路拓撲演算法、執行環境、程式設計工具，以及和上層應用的整合技術都是 SDN 的一部分，更是架構的核心部分。

## OpenFlow

1. OpenFlow 最初由矽谷的搖籃-斯坦福大學提出，由 GENI 專案通過試驗床合同推進，進而吸引了 Google、Facebook、微軟這樣多金的 IT/網際網路企業參與，最終形成了強大的產業聯盟，被業界廣泛應用。

2. OpenFlow 網路由 OpenFlow 交換機、FlowVisor 和 Controller 三部分組成。OpenFlow 交換機 (Switch) 進行資料層的轉發；FlowVisor 網路進行虛擬化；Controller 對網路進行集中控制，實現控制功能。Controller 在網路中相當於上帝，可以知道網路中所有的訊息，可以給交換機下發指令。Switch 就是一個實現 Controller 指令的實體，只不過這個交換機跟傳統的交換機不一樣，他的轉發規則由流表 (Flow Table) 指定，而流表由控制器傳送。

3. 關於 Controller。 NOX、 POX、 Beacon、 Floodlight、 Trema、 Ryu、 Maestro、 Jaxon、 OVS-controller、OpenDaylight、 Open Contrail、 NSX、 cisco ACI、 Cyaninc 等等，這些只是實現 controller 的工具！其中各分別以不同語言開發，如

    NOX：C++和 Python
    POX：Python
    Beacon：Java
    Floodlight：Java
    Ryu：Python
    OpenDaylight：Java

    利用以上工具編寫合適的 Controller。例如：Ryu controller（利用 Ryu 編寫的 Controller）, 因為 Ryu 是完全用 python 語言編寫，如果喜歡 python ，就可以利用 Ryu。OpenDaylight controller（利用 OpenDaylight 寫出的 controller），因為 OpenDaylight 是完全用 Java 語言編寫，如果需要和 Java 打交道，就可以利用 OpenDaylight。

## 小結]

SDN 包含 OpenFlow，而 OpenFlow 又包含 Controller，而 Controller 又可以使用像是 RYU 等等的不同工具來實現！

## 交換器實作

在交換器中有許多功能。以下列出一些簡單功能的交換器所能做的事情。

* 學習連接到連接埠的 host 之 MAC 位址，並記錄在 MAC 位址表當中。
* 對於已經記錄下來的 MAC 位址，若是收到送往該 MAC 位址的封包，則轉送該封包到相對應的連接埠。
* 對於未指定目標 MAC 位址的封包，則執行 Flooding。

接著來看如何使用 RYU 實作（ Software Defined Networking，SDN ）。

### OpenFlow 實作之交換器

OpenFlow 交換器會接受來自于 Controller 的指令並達到以下功能

* 對於接收到的封包進行修改或針對指定的連接埠進行轉送。
* 對於接收到的封包進行轉送到 Controller 的動作（ Packet-In ）。
* 對於接收到來自 Controller 的封包轉送到指定的連接埠（ Packet-Out ）

上述的功能所組合起來的就是一台交換器的實現。進一步探討參考 [這裡](https://osrg.github.io/ryu-book/zh_tw/html/switching_hub.html#ryu)

接著，我們要建立 RYU Controller，在這邊我們會使用到 Mininet

> mininet 是一個可以透過一些虛擬終端機、路由器、交換器等連接創建虛擬網路拓樸的平台，因此可以輕易的在自己的個人電腦中創作支援 SDN 的區域網路，在裡面創造出的虛擬的 host 並以真實電腦般發送封包，且可以使用 SSH(Secure Shell) 登錄虛擬 host 中操作。

如果對 Mininet 陌生不妨到 [這裡](https://ithelp.ithome.com.tw/articles/10197633) 先了解一下，對於安裝 mininet 也淺顯易懂的介紹了。

### RYU Controller 運作原理

當 Ryu Controller 要與 mininet 建立連接時，我們會執行 `ryu-manager –verbose ryu/app/simple_switch_13.py` ，其中 simple_switch_13.py 它是一個由 python 所撰寫的程式原始碼，其主要功能包含 switch 的 mac address 對應 port 關係，以及 flow entry 的新增與刪除作業。

## simple_switch_13.py 程式碼分析

我們以程式碼區塊逐一做簡單介紹，詳細步驟和程式碼解析，可參考 [官方文件](https://osrg.github.io/ryu-book/zh_tw/html/switching_hub.html#ryu)

* 程式碼區塊一解析：

``` python
def switch_features_handler(self, ev):
```

該程式碼區塊主要負責監控關於 switch 的各種狀態，包含初次建立連接時的握手訊息交換，目前該 switch 的連線狀態（連接 or 斷線）等

> OpenFlow 交換器的握手協議完成之後，新增 Table-miss Flow Entry 到 Flow table 中為接收 Packet-In 訊息做準備。

Table-miss Flow Entry 的優先權為 0 即最低的優先權，而且此 Entry 可以 match 所有的封包。 這個 Entry 的 Instruction 通常指定為 output action ，並且輸出的連接埠將指向 Controller。

* 程式碼區塊二解析：

``` python
def _packet_in_handler(self, ev):
```

此程式區塊處理的事情為，當 Ryu 中有未知的封包流經 switch 時，便會觸發 PacketIn 事件，也就是此段程式區塊所做的事情

> 目的 MAC 位址若存在于 MAC 位址表，則判斷該連接埠的號碼為輸出。反之若不存在于 MAC 位址表則 OUTPUT action 類別的實體並生成 flooding（ OFPP_FLOOD）給目的連接埠使用。

對於 Flow Entry 來說，設定 match 條件以分辨目標封包、設定 instruction 以處理封包以及 Entry 的優先權和有效時間。
對於交換器的的實作，Apply Actions 是用來設定那些必須立即執行的 action 所使用。
最後透過 Flow Mod 訊息將 Flow Entry 新增到 Flow table 中。

## Network Slice 實作

### 設備使用

* Switch：RT188T
* Controller：RYU Controller
* AP：ASUS RT-AC68U
* OpenFlow：OpenFlow 1.3

### 程式執行

執行步驟可以參考 [這裡](https://github.com/joechang0113/sdn_demo)，相關環境設定與程式碼解析可以參考 [官方中文說明文件](https://osrg.github.io/ryu-book/zh_tw/html/switching_hub.html#id5) 或是 [官方原文說明文件](https://ryu.readthedocs.io/en/latest/ryu_app_api.html)，理解程式碼相關運行後，撰寫自己的編譯檔案，並透過以下指令執行

``` python
ryu-manager --verbose ryu.app.sdn_5G_107_Final_Project.py
```

> `sdn_5G_107_Final_Project.py` 可以替換為自己編寫的檔案名稱
