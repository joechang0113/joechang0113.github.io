---
title: Embedding youtube in Jekyll
tags:
    - Jekyll
---
將 youtube 影片嵌入至 Jekyll

## 設置一

到 `_includes` 資料夾中，新增一支 `youtube.html`，貼上以下程式碼

```html
<iframe src="https://www.youtube.com/embed/{{ include.id }}" width="560" height="315" frameborder="0" allowfullscreen>
</iframe>
```

## 設置二

在要嵌入的`.md`檔案中根據所要位置貼上以下程式

```
{% include youtube.html id="videoID" %}
```
> 其中`videoID`就是youtube影片網址中 `v=xxxxxxxx`，的 `xxxxxxxx`
