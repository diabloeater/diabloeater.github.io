---
layout: post
title: Kramdown語法範例
date:   2019-08-28 22:49:35 +0800
categories: jekyll update
author: "鬼面散人"
---


Jekyll可以通過修改`_config.yml`調整各種網站建置相關的設定，包括使用的markdown解析器，預設為 [kramdown][kramdown-home]，也可以改成其他常見的的markdown解析器。

設定方式：
{% highlight shell %}
markdown: kramdown
{% endhighlight %}


# 關於kramdown

[kramdown][kramdown-home]是一個用於解析和轉換Markdown的Ruby函式庫。基於Markdown語法，同時也包含其他Markdown旳功能。雖然不盡然相容於Markdown，但是大多數Markdown文件透過kramdown進行解析時仍然可以正常顯示。

# 語法

kramdown支援所有的編碼格式，例如ASCII，UTF-8或ISO-8859-1，輸出結果與來源編碼會是一致的。和Html一樣包含區塊元素與行內元素，同樣的，行內元素只能出現在區塊元素或其他行內元素中。

- [換行](#line-wrapping)
- [程式碼區塊替代語法](#fenced-code-blocks)
- [跳脫字元與特殊字元](#escaping)
- [標題](#headers)
- [列表](#ordered-and-unordered-lists)
- [表格](#table)
- [分隔線](#horizontal-rules)
- [HTML區塊](#html-blocks)
- [注釋](#footnote)
- [圖片](#image)
- [文字樣式](#text-formatting)
- [IAL](#inline-attribute-lists)



## 1. 換行
{: #line-wrapping}

可以透過以下方式達到換行的效果：

- 通過保留空行以進行換行。

- 使用下列的區塊元素：

{% highlight html %}
a abbr acronym b big bdo br button cite code del dfn em i img input
ins kbd label option q rb rbc rp rt rtc ruby samp select small span
strong sub sup textarea tt var
{% endhighlight %}

- 使用EOB（End-Of-Block）記號`^` <!-- (非標準Markdown語法) -->

例如：
{% highlight html %}
1. list one
^
2. list two
{% endhighlight %}

產生的Html語法：
{% highlight html %}
<ol>
  <li>list one</li>
</ol>
<ol>
  <li>list two</li>
</ol>
{% endhighlight %}


## 2. 程式碼區塊替代語法
{: #fenced-code-blocks}

<!-- *非標準Markdown語法* -->

kramdown可以使用開頭跟結束的地方具有三個以上的波浪符號`~`的區塊來代替原本的程式碼區塊寫法。

特別要注意的是，用來收尾的波浪符號數量必須`大於`或`等於`開頭的數量。

表示法：
{% highlight html %}
~~~
def what?
  42
end
~~~
{: .language-ruby}
{% endhighlight %}

{% highlight html %}

~~~ ruby
def what?
  42
end
~~~
{% endhighlight %}


結果：

~~~
def what?
  42
end
~~~
{: .language-ruby}

## 3. 跳脫字元與特殊字元
{: #escaping}

在kramdown中的特殊符號都具有改變文件呈現方式的效果，為了使這些特殊符號能夠被正確的顯示出來，需要使用反斜線作為跳脫字元，也就是`\` 。

首先，在不使用`\`的條件下：

{% highlight html %}
This `is not a code` span!
{% endhighlight %}

結果：

This `is not a code` span!

加上`\`之後：
{% highlight html %}
This \`is not a code\` span!
{% endhighlight %}

結果：

This \`is not a code\` span! 

## 4. 標題（Headers）
{: #headers}

支持的標題表示法有Setext與atx：

- Setext風格

{% highlight html %}
First level header
==================

Second level header
------

   Other first level header
=
{% endhighlight %}

產生的Html語法：

{% highlight html %}
<h1 id="first-level-header">First level header</h1>
<h2 id="second-level-header">Second level header</h2>
<h1 id="other-first-level-header">Other first level header</h1>
{% endhighlight %}


- atx風格

{% highlight html %}
# H1 Header
## H2 Header
### H3 Header
#### H4 Header
##### H5 Header
###### H6 Header
{% endhighlight %}

產生的Html語法：

{% highlight html %}
<h1 id="h1-header">H1 Header</h1>
<h2 id="h2-header">H2 Header</h2>
<h3 id="h3-header">H3 Header</h3>
<h4 id="h4-header">H4 Header</h4>
<h5 id="h5-header">H5 Header</h5>
<h6 id="h6-header">H6 Header</h6>
{% endhighlight %}

kramdown會將Header的內容轉成小寫後自動產生id的值，也可以通過下面的方式自訂：

{% highlight html %}
Hello        {#id}
-----

# Hello      {#id}

# Hello #    {#id}

{% endhighlight %}

自訂後的效果：

{% highlight html %}
<h2 id="id">Hello</h2>
<h1 id="id">Hello</h1>
<h1 id="id">Hello</h1>
{% endhighlight %}


## 5. 列表（Ordered and Unordered lists）
{: #ordered-and-unordered-lists}

{% highlight html %}
* kram
+ down
- now

1. kram
2. down
3. now
{% endhighlight %}

產生的Html語法：

{% highlight html %}
<ul>
  <li>kram</li>
  <li>down</li>
  <li>now</li>
</ul>
<ol>
  <li>kram</li>
  <li>down</li>
  <li>now</li>
</ol>
{% endhighlight %}


## 6. 表格 (Tables)
{: #table}

{% highlight html %}
|-----------------+------------+-----------------+----------------|
| Default aligned |Left aligned| Center aligned  | Right aligned  |
|-----------------|:-----------|:---------------:|---------------:|
| First body part |Second cell | Third cell      | fourth cell    |
| Second line     |foo         | **strong**      | baz            |
| Third line      |quux        | baz             | bar            |
|-----------------+------------+-----------------+----------------|
| Second body     |            |                 |                |
| 2 line          |            |                 |                |
|=================+============+=================+================|
| Footer row      |            |                 |                |
|-----------------+------------+-----------------+----------------|
{% endhighlight %}

產生的Html語法：

{% highlight html %}
<table>
  <thead>
    <tr>
      <th>Default aligned</th>
      <th style="text-align: left">Left aligned</th>
      <th style="text-align: center">Center aligned</th>
      <th style="text-align: right">Right aligned</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>First body part</td>
      <td style="text-align: left">Second cell</td>
      <td style="text-align: center">Third cell</td>
      <td style="text-align: right">fourth cell</td>
    </tr>
    <tr>
      <td>Second line</td>
      <td style="text-align: left">foo</td>
      <td style="text-align: center"><strong>strong</strong></td>
      <td style="text-align: right">baz</td>
    </tr>
    <tr>
      <td>Third line</td>
      <td style="text-align: left">quux</td>
      <td style="text-align: center">baz</td>
      <td style="text-align: right">bar</td>
    </tr>
  </tbody>
  <tbody>
    <tr>
      <td>Second body</td>
      <td style="text-align: left">&nbsp;</td>
      <td style="text-align: center">&nbsp;</td>
      <td style="text-align: right">&nbsp;</td>
    </tr>
    <tr>
      <td>2 line</td>
      <td style="text-align: left">&nbsp;</td>
      <td style="text-align: center">&nbsp;</td>
      <td style="text-align: right">&nbsp;</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>Footer row</td>
      <td style="text-align: left">&nbsp;</td>
      <td style="text-align: center">&nbsp;</td>
      <td style="text-align: right">&nbsp;</td>
    </tr>
  </tfoot>
</table>
{% endhighlight %}

效果：

|-----------------+------------+-----------------+----------------|
| Default aligned |Left aligned| Center aligned  | Right aligned  |
|-----------------|:-----------|:---------------:|---------------:|
| First body part |Second cell | Third cell      | fourth cell    |
| Second line     |foo         | **strong**      | baz            |
| Third line      |quux        | baz             | bar            |
|-----------------+------------+-----------------+----------------|
| Second body     |            |                 |                |
| 2 line          |            |                 |                |
|=================+============+=================+================|
| Footer row      |            |                 |                |
|-----------------+------------+-----------------+----------------|

## 7. 分隔線（Horizontal Rules）
{: #horizontal-rules}

kramdown可以利用**3個以上的星號、橫線或底線**（不可混合）產生分隔線`<hr>`。開頭的星號、橫線或底線可以縮進3個空格。下面是示範多種不同的寫法：

{% highlight html %} 
* * *

---

  _  _  _  _

---------------
{% endhighlight %}

產生的Html語法：

{% highlight html %}
<hr>
<hr>
<hr>
<hr>
{% endhighlight %}


## 8. HTML區塊
{: #html-blocks}

可以利用markdown屬性來啓用或停用語法解析：
- `0`: 解析為原始Html
- `1`: 解析kramdown語法
- `block`: 解析為區塊元素
- `span`: 解析為行內元素


### 範例一 ###

在區塊元素設定`markdown="1"`，div內容被正確的解析為行內元素：

{% highlight html %}
<div markdown="1">This is the first part of a para,
which is continued here.
</div>
{% endhighlight %}

產生的Html語法：

{% highlight html %}
<div>
  <p>This is the first part of a para,
which is continued here.</p>
</div>
{% endhighlight %}

### 範例二 ###

在行內元素設定`markdown="1"`，仍然是行內元素，也是完全沒有問題的：

{% highlight html %}
<p markdown="1">This works without problems because it is parsed as
span-level elements</p>
{% endhighlight %}

產生的Html語法：

{% highlight html %}
<p>This works without problems because it is parsed as
span-level elements</p>
{% endhighlight %}

### 範例三 ###

在區塊元素設定`markdown="1"`，div結尾標籤由於和內容位於相同段落導致被解析為文字而消失不見：

{% highlight html %}
<div markdown="1">The end tag is not found because
this line is parsed as a paragraph</div>
{% endhighlight %}

產生的Html語法：

{% highlight html %}
<div>
  <p>The end tag is not found because
this line is parsed as a paragraph&lt;/div&gt;</p>
{% endhighlight %}

## 9. 注釋（Footnotes）
{: #footnote}

可以通過`[^註釋名稱]`的寫法在文章內加入註釋以及其定義：

{% highlight html %}
This is some text.[^1]. Other text.[^footnote].

[^1]: Some *crazy* footnote definition.

[^footnote]:
    > Blockquotes can be in a footnote.

        as well as code blocks

    or, naturally, simple paragraphs.
{% endhighlight %}

說明：

1. 注釋名稱可以是英文或數字，文字之間可以用短橫線相連。
2. 相同名稱的注釋將會連結到相同的注釋定義。
3. 注釋命名本身無關緊要，因為注釋編號是按照在文件出現的順序來編排的。 例如：第一個發現的注釋編號為1，第二個則是編號2，依此類推。
4. 當注釋名稱找不到可以匹配的注釋定義時，則不會被轉為注釋連結。

## 10. 圖片
{: #image}
{% highlight html %}
![Placeholder image](https://placehold.it/800x400 "Placeholder image")

![Image with caption](https://placehold.it/700x400 "Image with caption")
_圖片說明文字_
{% endhighlight %}

呈現結果：

![Placeholder image](https://placehold.it/800x400 "Placeholder image")

![Image with caption](https://placehold.it/700x400 "Image with caption")
_圖片說明文字_

產生的Html語法：

{% highlight html %}
<p>
  <img src="https://placehold.it/800x400" alt="Placeholder image" title="Placeholder image">
</p>
<p>
  <img src="https://placehold.it/700x400" alt="Image with caption" title="Image with caption">
  <em>圖片說明文字</em>
</p>
{% endhighlight %}


## 11. 文字樣式
{: #text-formatting}

{% highlight html %}
- **Bold**
- _Italics_
- ~~Strikethrough~~
- <ins>Underline</ins>
- <sup>Superscript</sup>
- <sub>Subscript</sub>
- Abbreviation: <abbr title="HyperText Markup Language">HTML</abbr>
- Citation: <cite>&mdash; Chester How</cite>
{% endhighlight %}

呈現效果：

- **Bold**
- _Italics_
- ~~Strikethrough~~
- <ins>Underline</ins>
- <sup>Superscript</sup>
- <sub>Subscript</sub>
- Abbreviation: <abbr title="HyperText Markup Language">HTML</abbr>
- Citation: <cite>&mdash; Chester How</cite>


## 12. IAL（Inline Attribute Lists）
{: #inline-attribute-lists}

可以利用IAL將一些屬性附加到元素中。


### 範例一：區塊IAL

置於區塊元素前後：

{% highlight html %}
A simple paragraph with an ID attribute.
{: #para-one}

> A blockquote with a title
{:title="The blockquote title"}
{: #myid}

{:.ruby}
    Some code here
{% endhighlight %}

產生的Html語法：

{% highlight html %}
<p id="para-one">A simple paragraph with an ID attribute.</p>
<blockquote title="The blockquote title" id="myid">
  <p>A blockquote with a title</p>
</blockquote>
<div class="ruby highlighter-rouge">
  <div class="highlight">
    <pre class="highlight">
      <code>Some code here</code>
    </pre>
  </div>
</div>
{% endhighlight %}

### 範例二：行內IAL

必須尾隨在行內元素之後，中間不允許存在其他字符，否則將會被忽略：

{% highlight html %}
This *is*{:.underline} some `code`{:#id}{:.class}.
A [link](test.html){:rel='something'} and some **tools**{:.tools}.
{% endhighlight %}

產生的Html語法：

{% highlight html %}
<p>This <em class="underline">is</em> some <code id="id" class="class highlighter-rouge">code</code>.
A <a href="test.html" rel="something">link</a> and some <strong class="tools">tools</strong>.</p>
{% endhighlight %}


### 範例三：特別行內IAL

特別行內IAL`{::}`不包含任何屬性，可用來分隔連續的元素，如果不分離則會被錯誤地解析：

{% highlight html %}
This *is italic*{::}*marked*{:.special} text
{% endhighlight %}

# 參考來源

[kramdown官網][kramdown-home]

<!-- [kramdown語法說明][jekyll-kramdown-syntax]

[Jekyll Markdown選項][jekyll-markdown] -->

[jekyll-markdown]: https://jekyllrb.com/docs/configuration/markdown/
[jekyll-kramdown-syntax]: https://kramdown.gettalong.org/syntax.html
[kramdown-home]: https://kramdown.gettalong.org/