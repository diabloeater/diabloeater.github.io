---
layout: post
title: Jekyll環境安裝 (MacOS)
date:   2019-08-20 21:24:35 +0800
categories: jekyll update
author: "鬼面散人"
---

時間過得飛快，入行不知不覺已將近10年，踩過無數地雷最後痕跡只留在心中，因此開始認真思考留下紀錄的可能性。基於身於工程師的一點小小浪漫，決定利用 [Jekyll][jekyll-docs] 來進行架設。它是一個問世多年的靜態網站生成器，可完全使用markdown語法來撰寫文章內容，最後將網站託管在Github上進行管理。或許不是最好用的，也存在其他更好的選擇，但對於現階段來說足夠矣。

# 建置流程

由於目前使用的個人電腦是Macbook 12"(MacOS版本10.11.6)，因此參考[在MacOS上安裝Jekyll](https://jekyllrb.com/docs/installation/macos/)來進行環境建置。實際安裝過程並不順利，遇到的一些問題及排除方式會在本文後續進行說明。

1.安裝完整的Ruby開發環境。要求如下：
- Ruby版本至少為2.4.0
- RubyGems
- GCC和Make

2.安裝Jekyll和bundler gems：
{% highlight shell %}gem install jekyll bundler{% endhighlight %}

3.建立一個新的Jekyll網站：
{% highlight shell %}
jekyll new myblog
{% endhighlight %}

4.到新建好的目錄下：
{% highlight shell %}
cd myblog
{% endhighlight %}

5.使其生成網站以及在本地服務器上運行：
{% highlight shell %}
bundle exec jekyll serve
{% endhighlight %}

6.最後，打開瀏覽器輸入網址以便預覽網站：
{% highlight shell %}
http：// localhost：4000
{% endhighlight %}


# 安裝途中遇到的問題

首先是安裝Bundler與Jekyll:

{% highlight shell %}
gem install --user-install bundler jekyll
{% endhighlight %}

出現如下錯誤:
{% highlight shell %}
ERROR:  Could not find a valid gem 'bundler' (>= 0), here is why:
          Unable to download data from https://rubygems.org/ - SSL_connect returned=1 errno=0 state=SSLv2/v3 read server hello A: tlsv1 alert protocol version (https://rubygems.org/latest_specs.4.8.gz)

ERROR:  Could not find a valid gem 'jekyll' (>= 0), here is why:
          Unable to download data from https://rubygems.org/ - SSL_connect returned=1 errno=0 state=SSLv2/v3 read server hello A: tlsv1 alert protocol version (https://rubygems.org/latest_specs.4.8.gz)
s{% endhighlight %}


檢查現有的Ruby版本:
{% highlight shell %}
ruby -v
{% endhighlight %}

結果如下:
{% highlight shell %}
ruby 2.0.0p648 (2015-12-16 revision 53162) [universal.x86_64-darwin15]
{% endhighlight %}

因為MacOS自帶的Ruby版本過舊，必須先更新至2.4.0以上。

解決辦法是直接重新安裝Ruby:

{% highlight shell %}
brew install ruby
{% endhighlight %}

*(因為目前暫時沒有使用Ruby開發專案的需求，所以rbenv...嗯，這裡就不折騰了XD)*

安裝結果：

{% highlight shell %}
Updating Homebrew...
==> Auto-updated Homebrew!
Updated 1 tap (homebrew/cask).
No changes to formulae.

Warning: You are using macOS 10.11.
We (and Apple) do not provide support for this old version.
You will encounter build failures with some formulae.
Please create pull requests instead of asking for help on Homebrew's GitHub,
Discourse, Twitter or IRC. You are responsible for resolving any issues you
experience, as you are running this old version.

==> Installing dependencies for ruby: automake, libtool, libyaml and readline
==> Installing ruby dependency: automake
==> Downloading https://homebrew.bintray.com/bottles/automake-1.16.1_1.el_capita
==> Downloading from https://akamai.bintray.com/d5/d552844779f0dc4062f27203f7fac
######################################################################## 100.0%
==> Pouring automake-1.16.1_1.el_capitan.bottle.tar.gz
🍺  /usr/local/Cellar/automake/1.16.1_1: 131 files, 3.4MB
==> Installing ruby dependency: libtool
==> Downloading https://homebrew.bintray.com/bottles/libtool-2.4.6_1.el_capitan.
==> Downloading from https://akamai.bintray.com/b7/b7651d0a082e2f103f03ca3a5ed83
######################################################################## 100.0%
==> Pouring libtool-2.4.6_1.el_capitan.bottle.tar.gz
==> Caveats
In order to prevent conflicts with Apple's own libtool we have prepended a "g"
so, you have instead: glibtool and glibtoolize.
==> Summary
🍺  /usr/local/Cellar/libtool/2.4.6_1: 70 files, 3.7MB
==> Installing ruby dependency: libyaml
==> Downloading https://github.com/yaml/libyaml/archive/0.2.2.tar.gz
==> Downloading from https://codeload.github.com/yaml/libyaml/tar.gz/0.2.2
######################################################################## 100.0%
==> ./bootstrap
==> ./configure --prefix=/usr/local/Cellar/libyaml/0.2.2
==> make install
🍺  /usr/local/Cellar/libyaml/0.2.2: 9 files, 313.4KB, built in 37 seconds
==> Installing ruby dependency: readline
==> Downloading https://ftp.gnu.org/gnu/readline/readline-8.0.tar.gz
######################################################################## 100.0%
==> ./configure --prefix=/usr/local/Cellar/readline/8.0.0_1
==> make install
==> Caveats
readline is keg-only, which means it was not symlinked into /usr/local,
because macOS provides the BSD libedit library, which shadows libreadline.
In order to prevent conflicts when programs look for libreadline we are
defaulting this GNU Readline installation to keg-only.

For compilers to find readline you may need to set:
  export LDFLAGS="-L/usr/local/opt/readline/lib"
  export CPPFLAGS="-I/usr/local/opt/readline/include"

For pkg-config to find readline you may need to set:
  export PKG_CONFIG_PATH="/usr/local/opt/readline/lib/pkgconfig"

==> Summary
🍺  /usr/local/Cellar/readline/8.0.0_1: 48 files, 1.5MB, built in 43 seconds
==> Installing ruby
==> Downloading https://cache.ruby-lang.org/pub/ruby/2.6/ruby-2.6.3.tar.xz
######################################################################## 100.0%
==> ./configure --prefix=/usr/local/Cellar/ruby/2.6.3 --enable-shared --disable-
==> make
==> make install
==> Downloading https://rubygems.org/rubygems/rubygems-3.0.3.tgz
######################################################################## 100.0%
==> /usr/local/Cellar/ruby/2.6.3/bin/ruby setup.rb --prefix=/private/tmp/ruby-20
==> Caveats
By default, binaries installed by gem will be placed into:
  /usr/local/lib/ruby/gems/2.6.0/bin

You may want to add this to your PATH.

ruby is keg-only, which means it was not symlinked into /usr/local,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.

If you need to have ruby first in your PATH run:
  echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_profile
For compilers to find ruby you may need to set:
  export LDFLAGS="-L/usr/local/opt/ruby/lib"
  export CPPFLAGS="-I/usr/local/opt/ruby/include"
For pkg-config to find ruby you may need to set:
  export PKG_CONFIG_PATH="/usr/local/opt/ruby/lib/pkgconfig"
==> Summary
🍺  /usr/local/Cellar/ruby/2.6.3: 19,374 files, 32.4MB, built in 6 minutes 46 seconds
==> Caveats
==> libtool
In order to prevent conflicts with Apple's own libtool we have prepended a "g"
so, you have instead: glibtool and glibtoolize.
==> readline
readline is keg-only, which means it was not symlinked into /usr/local,
because macOS provides the BSD libedit library, which shadows libreadline.
In order to prevent conflicts when programs look for libreadline we are
defaulting this GNU Readline installation to keg-only.
For compilers to find readline you may need to set:
  export LDFLAGS="-L/usr/local/opt/readline/lib"
  export CPPFLAGS="-I/usr/local/opt/readline/include"
For pkg-config to find readline you may need to set:
  export PKG_CONFIG_PATH="/usr/local/opt/readline/lib/pkgconfig"
==> ruby
By default, binaries installed by gem will be placed into:
  /usr/local/lib/ruby/gems/2.6.0/bin
You may want to add this to your PATH.
ruby is keg-only, which means it was not symlinked into /usr/local,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.
If you need to have ruby first in your PATH run:
  echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_profile

For compilers to find ruby you may need to set:
  export LDFLAGS="-L/usr/local/opt/ruby/lib"
  export CPPFLAGS="-I/usr/local/opt/ruby/include"

For pkg-config to find ruby you may need to set:
  export PKG_CONFIG_PATH="/usr/local/opt/ruby/lib/pkgconfig”
{% endhighlight %}


安裝雖然完成了，但是依照上面的訊息，還需要利用<code>bash_profile</code>進行額外的設定：

1.開啟 bash_profile
{% highlight shell %}
open -e .bash_profile 
{% endhighlight %}

沒有的話就另外建一個
{% highlight shell %}
touch .bash_profile
{% endhighlight %}

2.加入設定
{% highlight shell %}
export LDFLAGS="-L/usr/local/opt/readline/lib"
export CPPFLAGS="-I/usr/local/opt/readline/include"
export PKG_CONFIG_PATH="/usr/local/opt/readline/lib/pkgconfig"
export LDFLAGS="-L/usr/local/opt/ruby/lib"
export CPPFLAGS="-I/usr/local/opt/ruby/include"
export PKG_CONFIG_PATH="/usr/local/opt/ruby/lib/pkgconfig"
{% endhighlight %}

3.儲存變更設定
{% highlight shell %}
source .bash_profile
{% endhighlight %}

4.將終端機視窗整個關掉重開，並且再次檢查目前版本。執行結果如下：
{% highlight shell %}
ruby 2.6.3p62 (2019-04-16 revision 67580) [x86_64-darwin15]
{% endhighlight %}
升級完成。


最後，再執行jekyll檢查是否完成安裝：

{% highlight shell %}
jekyll
{% endhighlight %}

執行結果：
{% highlight shell %}
A subcommand is required. 
jekyll 3.8.6 -- Jekyll is a blog-aware, static site generator in Ruby
{% endhighlight %}

嗯...

總算是大功告成。



# 參考來源
[Jekyll 官方網站][jekyll-docs]


[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/ 