---
title: 【ROS 筆記】 Ubuntu16.04 建立 ROS 環境
tags:
    - ROS
    - Ubuntu
---
ROS 需要 python2.7 建立，使用 anaconda 會出現較多問題，會增加複雜度，建議基於系統 python2.7 環境建立並搭配 Virtualenv 使用即可

## Build ROS Kinetic and Setup

### 使用設備與環境

* PC: I7-8600, 1080TI
* RPLiDAR A2M8 R4
* Ubuntu16.04
* System Python2.7
* ROS Kinetic Kame
* 使用 zsh(z shell)

> 有興趣使用 zsh 可以參考 [這篇](https://joechang0113.github.io/2020/03/23/ubuntu-install-oh-my-zsh.html)

### 安裝 ROS

進行更新

``` bash
sudo apt-get update
sudo apt-get upgrade
```

安裝 ROS Kinetic Kame，並初始化及更新

``` bash
sudo apt-get install ros-kinetic-desktop-full
sudo rosdep init
rosdep update
```

> Ubuntu16.04 使用 kinetic

配置環境並安裝必要套件包

``` bash
echo "source /opt/ros/kinetic/setup.zsh" >> ~/.zshrc
source ~/.zshrc
sudo apt-get install python-rosinstall
sudo apt install python-rosinstall python-rosinstall-generator python-wstool build-essential -y
```

> rosinstall 是 ROS 中一個獨立分開的常用命令行工具，他可以方便讓你通過一條命令就可以給某個 ROS 軟件包下載很多開源碼

## ROS 基本使用測試

安裝完畢後，進行一些測試確定 ROS 能正常使用

### 測試 roscore

打開一個新 terminal 執行指令

``` bash
roscore
```

如下圖

![roscore](https://i.imgur.com/d19lrwP.png)

### 啟動 turtlesim

啟動一個 turtlesim 節點，並通過鍵盤控制其運動，新開一個 termianl，執行

``` bash
rosrun turtlesim turtlesim_node
```

如圖

![turtlesim_node](https://i.imgur.com/JyuV0cw.png)

![turtlesim](https://i.imgur.com/bEiVaBE.png)

接著另外開啟新 terminal, 執行

``` bash
rosrun turtlesim turtle_teleop_key
```

> 用以鍵盤控制的命令，若成功如下圖，可透過方向鍵控制小烏龜

如圖

![turtle_teleop_key](https://i.imgur.com/8tWdxfP.png)

### 啟動 rviz

新開啟一個終端輸入

``` bash
rviz
```

若成功，如圖開啟一個 RViz 視窗

![rviz_window](https://i.imgur.com/4Lj71SI.png)

### 啟動 Gazebo

新開啟一個終端輸入

``` bash
gazebo
```

若成功，如圖開啟一個 Gazebo 視窗

![Gazebo](https://i.imgur.com/Eip7533.png)

### 測試完畢

以上是針對 ROS 使用的測試步驟，到這邊告一段落，可以正常使用 ROS 以及下一步的 [LiDAR 環境建立](https://joechang0113.github.io/2019/12/23/ROS-LiDAR-build.html)
