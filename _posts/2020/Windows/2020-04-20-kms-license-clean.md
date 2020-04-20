---
title: 【Windows 筆記】清除系統上的 KMS 授權認證
tags:

    - Windows
    - KMS

---
如果只需要清除 `office` 的序號重新授權，請使用 `office 指定序號刪除` 就好，如果是想清除電腦中包含 `office` 和 `Windows` 所有 `KMS`

## office 指定序號刪除

到 office 安裝的資料夾路徑

64 位元如下

```txt
C:\Program Files\Microsoft Office\Office16
```

32 位元如下

```txt
C:\Program Files(x86)\Microsoft Office\Office16
```

用 `系統管理員的權限` 在該路徑下打開 terminal，輸入

```bash
cscript "C:\Program Files\Microsoft Office\Office16\ospp.vbs" /dstatus
```

![](https://i.imgur.com/CjlMgkb.png)

選擇要刪除的序號後五碼，輸入

```bash
cscript "C:\Program Files\Microsoft Office\Office16\ospp.vbs" /unpkey:xxxxx
```

## win & office 認證資料刪除

系統管理員打開 `cmd` ，依序輸入

```bash
slmgr /upk

slmgr /ckms

slmgr /rearm
```

重開機，打開 `Win + R` ，輸入

```txt
services.msc
```

找到 `Software Protection` ，右鍵點擊 `屬型（或內容）`

點擊 `啟用` ，就完成 `windows` 和 `office` KMS 清除
