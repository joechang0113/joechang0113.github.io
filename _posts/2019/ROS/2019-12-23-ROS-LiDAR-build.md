---
title: 【ROS 筆記】 Tracking by LiDAR & Inertial Sensor
tags:

    - ROS

---
建立好ROS環境後，接著我們要假設LiDAR相關環境，還沒搭建好ROS環境可以參考 [這篇](https://joechang0113.github.io//2019/12/23/Ubuntu-build-ROS/)

## 工作區建立

* 建立一個名為 catkin_ws 的資料夾，將 src 資料夾複製進去，在 terminal 中 catkin_ws 目錄下輸入

``` bash
catkin_make
```

若出現下圖錯誤

![cmake_error](https://i.imgur.com/kXS3SIN.png)

請輸入

``` bash
sudo apt-get install libarmadillo-dev
```

安裝後，重新輸入

``` bash
catkin_make
```

成功執行後如下圖

![cmake_100](https://i.imgur.com/jQ1GHTc.png)

> 顯示 100%安裝完成

* 到 zshrc 檔案設定

> 這邊如果使用的是原先的 bash shell, 請將以下 `zsh` 相關字樣更改為 `bash`

打開 terminal 輸入

``` bash
code ~/.zshrc
```

> 此為 zshrc 設定檔，無安裝 VSCode 可以使用 vim

至 zshrc 設定檔最下方，輸入

``` bash
export ROS_HOSTNAME= (your IP)
export ROS_IP= (your IP)
export ROS_MASTER_URL= http://(your IP):11311
```

## 在 ROS 上配置 LiDAR 並執行

首先，將　RPLiDAR 連接電腦並輸入

``` bash
ls –l /dev | grep ttyUSB
```

> 用來找到 ttyUSB0，如圖

![grep ttyUSB](https://i.imgur.com/Ytptgw3.png)

接著輸入

``` bash
sudo chmod 666 /dev/ttyUSB0
```

> 每次插拔都需要執行一次

如下圖

![chmod 666](https://i.imgur.com/aulBvmC.png)

然後輸入

``` bash
source devel/setup.zsh
```

> bash shell 記得自行更改 setup.zsh 為 setup.bash

![source devel](https://i.imgur.com/XYW8PD8.png)

最後執行　nodes.launch

``` bash
roslaunch obstacle_detector nodes.launch
```

部份過程如下圖

![nodes.launch](https://i.imgur.com/5cpN082.png)

執行完畢後，即可測試 LiDAR 建模掃描，顯示如下

![roslaunch_result](https://i.imgur.com/f3eW1hy.png)

### 執行 roslaunch obstacle_detector nodes_demo.launch 錯誤

當執行 nodes_demo.launch 時出現如下圖錯誤

![version_error](https://i.imgur.com/ePn8RvM.jpg)

這是因為 ROS 在 python2 環境下建立，但是 `fusion.py` 和 `listener_new1.py` 這兩個程式要用 python3 的環境執行，因此我們需要在 python2 環境下建立一個虛擬的 python3 環境來執行這兩支程式

方法如下，依序執行

``` bash
sudo pip install virtualenv
sudo virtualenv -p /usr/bin/python3.5 venv
source venv/bin/activate
sudo chmod 777 venv/lib/python3.5/site-packages/
sudo chmod 777 venv/bin/
sudo chmod 777 venv/lib/python3.5/site-packages/__pycache__/
pip install catkin_pkg pyyaml empy rospkg numpy
pip install pandas editdistance dtaidistance
```

此時，名稱前面應該會有我們建立的 venv 如下

![venv](https://i.imgur.com/BKg0PFK.png)

檢視一下目前的環境狀態如下

![check py2 py3](https://i.imgur.com/3jHWBGc.jpg)

> 可以看到 terminal 視窗是 ROS 執行環境 python2.7.12，VSCode 中 roslaunch 執行環境 venv 虛擬環境下為 python3.5.2

接著我們再次執行

``` bash
roslaunch obstacle_detector nodes_demo.launch
```

如下圖，最後完成 Rviz 開啟，成功執行以上兩隻程式

![demo_done_fusion](https://i.imgur.com/bKPrG40.png)

Terminal 中也成功獲取相關訊息

![run_venv](https://i.imgur.com/MvKcFnC.png)

### 可能問題

如果在venv裡執行還是出現同樣的錯誤請執行

``` bash
cd pmcn_ws/src/beginner/src/ # 切換到error訊息的檔案目錄下
ls # 查詢是否看到fusion.py 和 listener_new1.py
```

![Image](https://i.imgur.com/C1Qr4GT.png)

對這兩隻檔案分別執行

``` BASH
chmod 777 fusion.py
chmod 777 listener_new1.py
```

接著再次執行

``` BASH
roslaunch obstacle_detector nodes_demo.launch
```

## Demo執行步驟小結

``` bash
source venv/bin/activate  # 啟動 virtualenv
source devel/setup.zsh
roslaunch obstacle_detector nodes_demo.launch  # 程式執行
```
