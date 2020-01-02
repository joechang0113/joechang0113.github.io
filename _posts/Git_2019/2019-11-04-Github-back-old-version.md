---
title: 【Git 筆記】git 指令回復舊版本並更新遠端
tags: Git
---
假設發現最新的 code 版本有 bugs，想回復更新前的版本，你可以查看、複製並強制還原

## git reset -- hard 穿梭你提交的版本之間

輸入

``` bash
git log --oneline -n
```

來查看過去提交的 commit ID。

> n 表示想看前 n 次提交數

假設 n=5，輸入 `git log --oneline -n` ，則為

``` bash
joe-MacBook-Pro:test stevechung$ git log --oneline -5  // 最近 5 次提交記錄
ba2f0a4 (HEAD -> master, origin/master) test4  //最新提交的記錄
f3a6683 test1  // 上一個提交的記錄
4f0f054 test2
6fefa2d test1
77f9ec8 reset
```

或是可以輸入：

``` bash
git reflog
```

像是

``` bash
joe-MacBook-Pro:test stevechung$ git reflog  // 查看所有訊息版本
4f0f054 (HEAD -> master) HEAD@{0}: reset: moving to HEAD~2  // 這是例子一、回復的當前提交記錄
ba2f0a4 (origin/master) HEAD@{1}: commit: test4  // 假設你要回復到例子一、開頭使用的這個版本
f3a6683 HEAD@{2}: commit: test1
4f0f054 (HEAD -> master) HEAD@{3}: commit: test2
6fefa2d HEAD@{4}: commit: test1
77f9ec8 HEAD@{5}: commit: reset
58f0631 HEAD@{6}: reset: moving to HEAD
58f0631 HEAD@{7}: commit (initial): gitreset
```

來查看完整 commit 訊息和 commit ID。

接著複製要回復的 commit ID，輸入：

``` bash
git reset --hard "commit ID"
```

> 將 commit ID 替換為自己要回復的版本，此時本機儲存庫已經完成舊版本更新。

若要更新遠端儲存庫，輸入：

``` bash
git push -f
```

> 此命令為強制上傳，忽略舊版本覆蓋較新版本的提醒

以上，完成本機和遠端儲存庫更新
