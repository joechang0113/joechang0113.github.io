---
title: 【VSCode 筆記】 大型工作區問題
tags:

    - VSCode

---
Visual Studio Code 無法監視這個大型工作區的變化 Visual Studio Code is unable to watch for file changes in this large workspace(error ENOSPC)

## 解決辦法

查看目前工作區最大監控數量

``` bash
cat /proc/sys/fs/inotify/max_user_watches
```

編輯系統檔

``` bash
code /etc/sysctl.conf
```

在最下方新增一行

``` bash
fs.inotify.max_user_watches=524288
```

最後 terminal 輸入

``` bash
sudo sysctl -p
```

更改完成，正常使用

![image](https://i.imgur.com/9Tx27hh.png)
