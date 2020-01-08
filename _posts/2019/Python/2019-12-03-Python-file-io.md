---
title: 【Python 筆記】 Python 檔案讀寫
tags:

    - Python

---
打算依照時間戳歸納三層資料夾，儲存所需 csv 檔案，若欲存目錄不存在則依照路徑新建目錄，再儲存所需 csv 檔案，希望的存檔結構及結果如下圖。

![python-file-io](/assets/images\posts\post_python-file-io.png)

> 其中 csv 檔名 `20191203_11-12-36.csv` 所代表的是 2019/12/03, 11:12:36

## 建立時間戳

直接看程式碼

``` python
local_year = time.strftime(
    "%Y", time.localtime()) # 將 localtime 格式化為 %Y (2019)
local_date = time.strftime(
    "%m%d", time.localtime()) # 將 localtime 格式化為 %m%d (1203)
local_time = time.strftime(
    "_%H-%M-%S", time.localtime()) # 將 localtime 格式化為 _%H-%M-%S (_時-分-秒）
```

> 這邊的底線 `_` 以及連字號 `-` 可依照自身喜歡的檔名樣式做修改

## 建立存檔路徑

利用此段程式碼建立欲存檔的目錄路徑

``` python
path = "./CSV_FILE_IO" + "/" + str(local_year) + "/" + str(local_date)
```

## 按路徑存檔 csv

判斷欲存檔的目錄路徑是否存在，如果不存在則建立，並存檔

``` python
if not os.path.isdir(path): # 若路徑不存在
    os.makedirs(path)  # 建立多層次目錄
    with open(path + '/' + str(local_year + local_date + local_time) + '.csv', 'w') as csvfile: # 在目錄 path 之後存一檔名為上述所建立的時間戳之 csv 檔到 csvfile 中
        data = 'csv test file test!!' # 將欲存檔之 csv 內容存為 data
        csvfile.write(data) # 將 data 存入 csvfile
        print('context: {}'.format(data)) # 打印存入訊息，以確認存檔成功
```

如果欲存檔路徑已經存在，則直接存入該目錄路徑

> 此部分邏輯與上述相同，不多做說明

``` python
else:
    with open(path + '/' + str(local_date + local_day + local_time) + '.csv', 'w') as csvfile:
        data = 'csv test file test!!'
        csvfile.write(data)
        print('context: {}'.format(data))
```

## 完整程式碼

``` python
import os
import csv
import time
# 所需的引入

local_year = time.strftime("%Y", time.localtime())
local_date = time.strftime("%m%d", time.localtime())
local_time = time.strftime("_%H-%M-%S", time.localtime())
path = "./CSV_FILE_IO" + "/" + str(local_year) + "/" + str(local_date)

if not os.path.isdir(path):
    os.makedirs(path)  # 多層次建立目錄
    with open(path + '/' + str(local_year + local_date + local_time) + '.csv',
              'w') as csvfile:
        data = 'csv test file test!!'
        csvfile.write(data)
        print('context: {}'.format(data))
else:
    with open(path + '/' + str(local_year + local_date + local_time) + '.csv',
              'w') as csvfile:
        data = 'csv test file test!!'
        csvfile.write(data)
        print('context: {}'.format(data))
```

最後如果存檔成功會看到

![file-io-final](/assets/images\posts\post_file-io-final.png)
