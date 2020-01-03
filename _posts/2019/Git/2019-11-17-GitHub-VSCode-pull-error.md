---
title: 【VSCode 筆記】 GitLens 執行 git pull 報錯
tags: VSCode
---
從 A 電腦 push 新資料到遠端儲存庫後，在作業到一半的 B 電腦，在 VSCode 利用 GitLens 從遠端庫 pull 時，發生 `在 pull 前，請先清理工作樹` ，這個情況是因為 git 倉庫的 code 和 本地的 code 產生衝突，所以發生錯誤。

### 解決辦法

> 以下兩個方法二擇一即可

1. 利用 VSCode 中的內建 Git 功能 - 原始檔控制，執行 `取消所有暫存變更` ，若還是出現同樣狀況沒直接使用 `捨棄所有變更` 即可

![cancel temp save](/images/posts/post_cancel-temp-save.png)

2. 在命令列輸入以下指令，在接著做 pull 相關動作

``` bash
git reset --hard
```

### 關於 `git reset` 使用方式參考

* 回退前一版本，將暫存區和本地已提交內容恢復到未暫存狀態，且不影響本地版本

``` bash
git reset --mixed
```

* 回退前一版本，將已提交內容恢復到暫存區版本，不影響本地版本，且不清空暫存區

``` bash
git reset --soft
```

* 回退前一版本，將已提交內容恢復到本地並覆蓋本地版本，且清空暫存區

``` bash
git reset --hard
```

以上做個簡單記錄！
