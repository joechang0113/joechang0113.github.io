---
title: 【Markdown 筆記】MarkDown-Socialpage
tags:
    - Markdown
---
許多技術文章都是以 markdown 來撰寫，其中 GitHub 上的 `README.md` 也不例外，大家對於 markdown 的語法熟悉度相較於其他或許更為容易上手，本 blog 的 About 頁面也是使用 markdown 編寫，大篇幅的文字敘述總是較為無聊，希望可以在聯絡方式上做一些改變

這樣的社群連結可以使用在 GitHub 上的 [README.md](https://github.com/joechang0113/joechang0113.github.io) 或是 blog 上的相關 social media 頁面，像是這樣

![Image](https://i.imgur.com/2MQPrZp.png)

## 在 markdown 使用社群連結

在想要插入 link 的地方貼上以下程式碼

``` md
<!-- Please don't remove this: Grab your social icons from https://github.com/joechang0113/socialpage -->

<!-- display the social media buttons in your README -->

[![alt text][1.1]][1]
[![alt text][2.1]][2]
[![alt text][3.1]][3]
[![alt text][4.1]][4]
[![alt text][5.1]][5]
[![alt text][6.1]][6]

<!-- links to social media icons -->
<!-- no need to change these -->

<!-- icons with padding -->

[1.1]: https://i.imgur.com/GmxhYO0.png (instagram icon with padding)
[2.1]: https://i.imgur.com/oFsAcMx.png (facebook icon with padding)
[3.1]: https://i.imgur.com/YCdR3o9.png (twitter icon with padding)
[4.1]: https://i.imgur.com/AYLF0go.png (weibo icon with padding)
[5.1]: https://i.imgur.com/5BWvIrF.png (github icon with padding)
[6.1]: https://i.imgur.com/UA7Oh6z.png (medium icon with padding)

<!-- links to your social media accounts -->
<!-- update these accordingly -->

[1]: https://www.instagram.com/joechang0113
[2]: http://www.facebook.com/joechang0113
[3]: https://twitter.com/joechang0113
[4]: http://weibo.com/7331813538/profile
[5]: https://github.com/joechang0113
[6]: https://medium.com/@joechang0113

<!-- Please don't remove this: Grab your social icons from https://github.com/joechang0113/socialpage -->

```

不要懷疑，請全部貼上，雖然這個在你的 `.md` 上會佔據一定的版面，但是為了效果就讓步吧！

這時候你的頁面應該已經有這些 social media links 了

<!-- Please don't remove this: Grab your social icons from https://github.com/joechang0113/socialpage -->

[![alt text][1.1]][1] <!--(instagram) -->
[![alt text][2.1]][2] <!--(facebook) -->
[![alt text][3.1]][3] <!--(twitter) -->
[![alt text][4.1]][4] <!--(weibo) -->
[![alt text][5.1]][5] <!--(github) -->
[![alt text][6.1]][6] <!--(medium) -->

## 替換 social media links

來做點簡單的 🔗鏈結 替換

``` md
[1]: https://www.instagram.com/joechang0113
[2]: http://www.facebook.com/joechang0113
[3]: https://twitter.com/joechang0113
[4]: http://weibo.com/7331813538/profile
[5]: https://github.com/joechang0113
[6]: https://medium.com/@joechang0113
```

將上述的 `yourname` 更改為自己的即可，如果不知道 name 也可以直接把對應的社群連結替換為您要跳轉的頁面，效果是一樣的！

替換後再試試看點擊這些 icon 就能成功連結到自己的 social media 囉！

> 注意事項，這個方法用在某些 `.md` 檔案會出現只有跳轉到圖片網址的問題，實測 [README.md](https://github.com/joechang0113/socialpage) 可以呈現，如果有朋友知道為什麼或是怎麼解決的也請多指教了！
<!-- icons with padding -->

[1.1]: https://i.imgur.com/GmxhYO0.png (instagram icon with padding)
[2.1]: https://i.imgur.com/oFsAcMx.png (facebook icon with padding)
[3.1]: https://i.imgur.com/YCdR3o9.png (twitter icon with padding)
[4.1]: https://i.imgur.com/AYLF0go.png (weibo icon with padding)
[5.1]: https://i.imgur.com/5BWvIrF.png (github icon with padding)
[6.1]: https://i.imgur.com/UA7Oh6z.png (medium icon with padding)

<!-- links to your social media accounts -->
<!-- update these accordingly -->

[1]: https://www.instagram.com/joechang0113
[2]: http://www.facebook.com/joechang0113
[3]: https://twitter.com/joechang0113
[4]: http://weibo.com/7331813538/profile
[5]: https://github.com/joechang0113
[6]: https://medium.com/@joechang0113

<!-- Please don't remove this: Grab your social icons from https://github.com/joechang0113/socialpage -->
