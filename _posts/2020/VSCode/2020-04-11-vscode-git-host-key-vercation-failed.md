---
title: 【VSCode 筆記】Host key verification failed
tags:

- VSCode
- Git

---
更換 `ssh` 後，透過 VSCode 的 Git 工具更新時出現下面問題

![Image](https://i.imgur.com/o6U1Wuk.png)

## 解決辦法

在 terminal 依序輸入

``` bash
ssh-keygen -R domain.com
ssh-keyscan -t rsa domain.com >> ~/.ssh/known_hosts
```

接著，利用命令的方式，先執行 `git pull` , `git push` 等等的相關動作，會出現以下詢問

``` bash
The authenticity of host 'domain.com (a.b.c.d)' can't be established.
RSA key fingerprint is XX:XX:...:XX.
Are you sure you want to continue connecting (yes/no)?
```

填入 `yes` ，經過認證後，VSCode 的工具就不會再有以上問題了！

![Image](https://i.imgur.com/2us1c5V.png)
