---
title:【Windows 筆記】使用命令提示字元刪除合併磁碟
tags:
- Windows
---
在整理磁區常常碰到無法合併或刪除的情形，透過命令提示字元的磁碟管理工具可以很好解決，以下分享常用工具

## 指令使用

在 Terminal 輸入指令

```
diskpart
```

一段時間會跳出DiskPart管理視窗，接著輸入

```
list disk
```
會列出目前讀取到的磁碟

![](https://i.imgur.com/XqOHHEx.png)

這邊最簡單區分的方法就是容量，如果容量相同無法分辨要處理的是哪一顆硬碟，請按下 `Windows + R`，然後輸入

```
diskmgmt.msc
```

![](https://i.imgur.com/SmhEOwL.png)

在這邊可以看到自己的磁碟編號

![](https://i.imgur.com/nu37IXq.png)

確定後，回到 `diskpart.exe` 視窗，並輸入 `select Disk` + `空格` + `磁碟代號`，這邊我選擇代號`1`

```
select disk 1
```

輸入完畢後，再接著檢查自己選擇的磁碟是否正確，輸入

```
list partition
```

確定無誤後，輸入

```
clean
```

![](https://i.imgur.com/D6agi9N.png)

完成清理後，會顯示 `DiskPart 成功的清理了磁碟`，就大功告成，回到 `磁碟管理` 執行初始化。