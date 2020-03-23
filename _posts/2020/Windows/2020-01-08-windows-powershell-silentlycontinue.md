---
title: 【Windows 筆記】Powershell 關閉下載進度條
tags:

    - Windows
    - PowerShell

---
在 windows 中，PowerShell 有個很常用的內建 Cmdlet 叫做 Invoke-WebRequest，他可以幫我們發出一個 HTTP 要求，從網路上下載一個檔案，有很多情況都會用到。

> `Invoke-WebRequest` 有個很簡便的別名 `wget` ，可以縮短這個 `Cmdlet` 命令。

## PowerShell 進度條

使用 powershell 下載的過程中你會看到如下進度調顯示，這是 powershell 的偏好設定變數 (Preference Variables) `$ProgressPreference` ，他的預設值為 `continue` 所導致，這個設定在 `Cmdlet` 執行時會預設顯示進度列：

![Image](https://i.imgur.com/hG3HsXE.png)

這個看起來很方便的進度條，可能造成下載檔案的執行速度降低，如果想了解執行速度相關指令可以參考 [Measure-Command](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/measure-command?view=powershell-6)，接著我們要將 `$ProgressPreference` 這個設定變數改為 `SilentlyContinue` ，然後重新執行 `Powershell` 。

## SilentlyContinue 設定

首先，找到這個檔案

`%USERPROFILE%\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1`

沒有這個檔案的話可以自己建立一個，他的路徑在 `WindowsPowerShell` 下，我們先切換到該目錄：

``` bash
cd .\Documents\WindowsPowerShell\
```

![Image](https://i.imgur.com/2Y1zvxT.png)

接著在該目錄找到檔案

``` bash
ls
```

![Image](https://i.imgur.com/uuYzKFa.png)

使用自己的編譯器打開，這邊使用 VSCode，接著加入

``` bash
$ProgressPreference = 'SilentlyContinue'
```

如下，為了不誤導，其餘不相關已註解掉

![Image](https://i.imgur.com/OYbK4Yc.png)

最後存檔，關閉 `.ps1` 檔案，重新啟動 `Powershell` 即可
