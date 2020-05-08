---
title: 【Git 筆記】error:modified content, untracked content
tags:

    - Git

---
在 `git push` 時出現如下錯誤狀況

```bash
modified content, untracked content
```

## 解決方式

到出現此狀況的資料目錄下，輸入

```bash
git rm -rf --cached <untrackfile>
```

然後，重新執行上傳步驟

```bash
git add .
```

或是

```bash
git add <untrackfile>
```
