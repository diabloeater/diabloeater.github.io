---
layout: post
title: 開始使用 Jekyll
date:   2019-08-26 21:44:12 +0800
categories: jekyll update
author: "鬼面散人"
---



建立一個新的Jekyll網站`myblog`：
{% highlight shell %}
jekyll new myblog
{% endhighlight %}

執行命令：
{% highlight shell %}
bundle exec jekyll serve
{% endhighlight %}

打開瀏覽器輸入網址：
{% highlight shell %}
http：// localhost：4000
{% endhighlight %}

此時會出現預設的文章範本`Welcome to Jekyll!`。

範本所在的目錄為`_posts`，我們可以試著修改。文件命名原則`YYYY-MM-DD-name-of-post.ext`。副檔名`.ext`可以是`.markdown`或是縮寫`.md`，甚至是`.html`。


值得注意的是，`jekyll serve`在執行期間會在啓動本地端伺服器的同時自動更新**整個網站**。文章量累積到一定程度的時候勢必會會浮現效能問題。




# 參考來源
[Jekyll 官方網站][jekyll-docs]


[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-markdown]: https://jekyllrb.com/docs/configuration/markdown/
[jekyll-kramdown-syntax]: https://kramdown.gettalong.org/syntax.html
