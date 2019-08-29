---
layout: post
title: Jekyll語法範例
date:   2019-08-28 22:49:35 +0800
categories: jekyll update
author: "鬼面散人"
---


在`_config.yml`中可以修改各種建置網站相關的設定，其中也包含了渲染網頁的 markdown解析器。

{% highlight shell %}
markdown: kramdown
{% endhighlight %}

雖然預設為 [kramdown][kramdown-home]，實際上 Jekyll 也同時支援其他多種的markdown解析器。

# 關於kramdown

[kramdown][kramdown-home]是一個用於解析和轉換Markdown的Ruby函式庫。基於Markdown語法，同時也包含其他Markdown旳功能。雖然不盡然相容於Markdown，但是大多數Markdown文件透過kramdown進行解析時仍然可以正常顯示。

# 語法

kramdown文檔可以是任何編碼，例如ASCII，UTF-8或ISO-8859-1，輸出將具有與源相同的編碼。

該文檔包含兩種類型的元素：塊級元素和跨度級元素：

塊級元素定義內容的主要結構，例如，文本的哪個部分應該是段落，列表，塊引用等等。

跨度級元素標記小文本部分，例如，強調文本或鏈接。

因此，跨度級元素只能出現在塊級元素或其他跨度級元素中。

您經常會在塊級元素描述中找到對行的“第一列”或“第一個字符”的引用。始終相對於當前縮進級別採用這樣的引用，因為一些塊級元素打開了新的縮進級別（例如，塊引用）。kramdown文檔的開頭打開默認縮進級別，該級別從文本的第一列開始。

- [換行方式](#line-wrapping)
- [程式碼區塊替代語法](#fenced-code-blocks)
- [使用反斜線`\`進行跳脫](#escaping)
- [標題](#headers)
- [列表](#ordered-and-unordered-lists)
- [文章縮排](#)
- [表格](#table)
- [HTML](#)
- [超連結](#)
- [圖片](#)
- [文本](#)
- [IAL](#inline-attribute-lists)



## 1. 換行方式
{: #line-wrapping}

- 基本就是中間空一行。

- 也可以使用 html 區塊元素

{% highlight html %}
a abbr acronym b big bdo br button cite code del dfn em i img input
ins kbd label option q rb rbc rp rt rtc ruby samp select small span
strong sub sup textarea tt var
{% endhighlight %}

- 使用EOB（End-Of-Block）記號`^` (非標準Markdown語法)

{% highlight html %}
1. list one
^
2. list two
{% endhighlight %}

結果：
1. list one
^
2. list two

<!-- 此外，還有一些像是block IAL（Block Inline Attribute Lists）之類的非標準Markdown語法，就不多說了。 -->


## 2. 程式碼區塊替代語法
{: #fenced-code-blocks}

*非標準Markdown語法*

kramdown還支持程式碼區塊的替代語法，需要以三個以上的波浪符號`~`作為開頭跟結束，用來結束的波浪號數量必須大於或等於開頭的數量。


{% highlight html %}
~~~
def what?
  42
end
~~~
{: .language-ruby}
{% endhighlight %}

或者
{% highlight html %}

~~~ ruby
def what?
  42
end
~~~
{% endhighlight %}


結果是一樣的：

~~~
def what?
  42
end
~~~
{: .language-ruby}

## 3. 使用反斜線`\`進行跳脫
{: #escaping}


在不使用`\`的情況下：
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



####  ＊以下是支援`\`跳脫的特殊字元：

|  |  |
| ------ | ------ |
|\       | backslash 反斜線| 
| ------ | ------ |
|.       | period |
| ------ | ------ |
|*       | asterisk |
| ------ | ------ |
|_       | underscore 下底線|
| ------ | ------ |
|+       | plus   |
| ------ | ------ |
|-       | minus  |
| ------ | ------ |
|=       | equal sign |
| ------ | ------ |
|`       | back tick|
| ------ | ------ |
|()[]{}<>| left and right parens/brackets/braces/angle brackets
| ------ | ------ |
|#       | hash   |
| ------ | ------ |
|!       | bang   |
| ------ | ------ |
|<<      | left guillemet|
| ------ | ------ |
|>>      | right guillemet|
| ------ | ------ |
|:       | colon  |
| ------ | ------ |
|\|       | pipe   |
| ------ | ------ |
|"       | double quote |
| ------ | ------ |
|'       | single quote |
| ------ | ------ |
|$       | dollar sign |
| ------ | ------ | 



## 4. 標題（Headers）
{: #headers}

{% highlight html %}

一級標題
==================

二級標題
------

# H1 標題
## H2 標題
### H3 標題
#### H4 標題
##### H5 標題
###### H6 標題
{% endhighlight %}

結果：

一級標題
==================

二級標題
------
# H1 標題
## H2 標題
### H3 標題
#### H4 標題
##### H5 標題
###### H6 標題



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

結果：
* kram
+ down
- now

1. kram
2. down
3. now


## 6. 文章縮排

## 7. 表格
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

結果：

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



{% highlight html %}
### 

* * *

---

  _  _  _  _

---------------
{% endhighlight %}



## 8. HTML

## 9. 超連結



## 10. 圖片

## 11. 文本


## 12. IAL（Inline Attribute Lists）
{: #inline-attribute-lists}

這些元素用於將屬性附加到另一個元素。
此塊級元素用於將屬性附加到另一個塊級元素。塊內聯屬性列表（塊IAL）具有與ALD相同的結構，除了冒號/引用名稱/冒號部分被冒號替換。塊IAL（或兩個或多個塊IAL）必須直接放在屬性應附加到的塊級元素之前或之後。如果塊IAL直接在塊級元素之後和之前，則將其應用於前一元素。在所有其他情況下，塊IAL被忽略，例如，當塊IAL被空行包圍時。

IAL的鍵值對優先於引用的ALD中同等命名的鍵值對。

以下是塊IAL的一些示例：
{% highlight html %}
A simple paragraph with an ID attribute.
{: #para-one}

> A blockquote with a title
{:title="The blockquote title"}
{: #myid}

{:.ruby}
    Some code here
{% endhighlight %}

產生的Html像這樣：
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




# 參考來源


[kramdown官網][kramdown-home]

[kramdown語法說明][jekyll-kramdown-syntax]

[Jekyll Markdown選項][jekyll-markdown]

[jekyll-markdown]: https://jekyllrb.com/docs/configuration/markdown/
[jekyll-kramdown-syntax]: https://kramdown.gettalong.org/syntax.html
[kramdown-home]: https://kramdown.gettalong.org/