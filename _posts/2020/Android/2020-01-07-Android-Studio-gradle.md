---
title: 【Android 筆記】 Gradle 版本更新問題
tags:

    - Android

---
最近修改 Android Sensor Driver 碰到了 Gradle 相關問題，錯誤訊息如下

``` java
Gradle DSL method not found: 'google()'
```

## 解決方法

將 gradle 版本由 3.3 更新為 4.6，如下圖，到 **Gradle Script** 下的 **gradle-wrapper.properties** 將舊版本的 `distributionUrl` 替換為新版本連結，如下

``` java
distributionUrl=https\://services.gradle.org/distributions/gradle-3.3-all.zip
```

``` java
distributionUrl=https\://services.gradle.org/distributions/gradle-4.6-all.zip
```

改完如下圖

![gradle-wrapper.properties](https://i.imgur.com/mAsgxSJ.png)

接著到** build.gradle(Project android_sensors_driver)** 文件修改 `gradleVersion` 版本為 `4.6` ，如下圖

![build.gradle](https://i.imgur.com/klhru51.png)

接著按下 Sync Now

![build.gradle](https://i.imgur.com/rmLyhSS.png)

同步完成後又碰到錯誤如下

``` bash
Configuration 'compile' is obsolete and has been replaced with 'implementation' and 'api'.
```

![Sync Now](https://i.imgur.com/l2haatk.png)

查詢一下，發現 [官方說明文件](https://developer.android.com/studio/build/dependencies?utm_source=android-studio#dependency_configurations)，有提到將 **build.gradle** 相關文件中的 `compile` 修改為 `implementation` 的需求，文件中我們要注意的內容如下方截圖

![compile instead of api](https://i.imgur.com/G3icdGn.png)

大致上的意思就是說 `compile` 被 `implementation` 或是 `api` 所替代
至於 `implementation` 和 `api` 差異，我的理解如下

* api 指令

完全等同於 compile 指令，沒區別，你將所有的 compile 改成 api，完全沒有錯。

* implement

這個指令的特點就是，對於使用了該命令編譯的依賴，對該項目有依賴的項目將無法訪問到使用該命令編譯的依賴中的任何程序，也就是將該依賴隱藏在內部，而不對外部公開。

所以我們到所有 **build.gradle** 相關文件，將 `compile` 替換成 `implementation` ，如下圖

![compile](https://i.imgur.com/OS9ywrf.png)

改為

![implementation](https://i.imgur.com/5MDtg6a.png)

再次 RUN，解決問題了！
