---
title: 【Windows 筆記】 Windows 和 Office 使用期限及認證序號查詢
tags:
- Windows
---
windows和office都需要有授權碼才能夠使用，往往輸入一次後忘記自己的序號，以下分享如何找出認證序號

## Windows

### 使用期限

windows+R 然後輸入 slmgr.vbs -xpr

![](https://i.imgur.com/BLxtYP5.png)
>永久啟用

![](https://i.imgur.com/v1JFVR1.png)
>大量起用將到期

### 序號查詢

在桌面上新增一個空白記事本，將下面程式碼貼進去

```bash
Set WshShell = CreateObject("WScript.Shell")
MsgBox ConvertToKey(WshShell.RegRead("HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\DigitalProductId"))

Function ConvertToKey(Key)
Const KeyOffset = 52
i = 28
Chars = "BCDFGHJKMPQRTVWXY2346789"
Do
Cur = 0
x = 14
Do
Cur = Cur * 256
Cur = Key(x + KeyOffset) + Cur
Key(x + KeyOffset) = (Cur \ 24) And 255
Cur = Cur Mod 24
x = x -1
Loop While x >= 0
i = i -1
KeyOutput = Mid(Chars, Cur + 1, 1) & KeyOutput
If (((29 - i) Mod 6) = 0) And (i <> -1) Then
i = i -1
KeyOutput = "-" & KeyOutput
End If
Loop While i >= 0
ConvertToKey = KeyOutput
End Function
```

接著點選 `檔案-另存為新檔`，類型選擇 `所有檔案`，檔案名稱請改為 `productkey.vbs`，案存檔

![Image](https://i.imgur.com/c6RQjgK.png)

接著，打開該檔案

![Image](https://i.imgur.com/ByVCpEW.png)

如下視窗就是你的 windows 序號

![Image](https://i.imgur.com/7T0FkQ6.png)

## Office

### 使用期限

沒有更改office安裝路徑前提下，到資料夾路徑`C:\Program Files\Microsoft Office`下，進入你所安裝版本的資料夾

![](https://i.imgur.com/fr3ufPE.png)

在如下頁面，開啟命令視窗(CMD)

![](https://i.imgur.com/0aiowz6.png)


然後輸入` cscript ospp.vbs /dstatus`，出現下方訊息

![Image](https://i.imgur.com/RzG4T6H.png)
> 紅框處就是序號末五碼

將SKU ID 複製，請複製離Exiting最近的那一組，因為列出來的是所有你曾經認證的序號，越下面越新

![](https://i.imgur.com/NhI8AAb.png)

接著，輸入`slmgr /xpr` ，加上剛剛複製的 `SKU ID`

![](https://i.imgur.com/Dwq0x2H.png)

按下 `Enter`

![Image](https://i.imgur.com/B5IuYfi.png)
> 詳細資訊如圖
