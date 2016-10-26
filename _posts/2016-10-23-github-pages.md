---
layout: post
title: "用GithubPages建博客"
subtitle: "GithubPages, Jkeyll, Blog"
author: "Lulu"
header-img: "img/post-bg/githubpages.jpg"
date: 2016-10-23
catalog: true
tags:
    - 前端
---
## 前言

>本文章主要内容在介绍如何在GithubPages上搭建属于自己的博客，以及搭建过程中可能遇到的问题。

## Github Pages

>Q: What is Github Pages?
>A: Websites for you and your projects.

简而言之，Github Pages是Github为你提供的网站，你可以在上面部署自己的博客。并提供给你的博客提供一个属于你的域名：`http://username.github.io`

迫不及待想动手了么？不要着急，先花点时间阅读下相关教程，边学边做。

虽然在网上，有不少关于如何在Github Pages上搭建博客的文章，但是我还是建议参考官方的教程。如果你遇到问题的话，请先仔细查看下是否正确使用了官方的指导，然后再搜索解决方法。

**搭建过程中的信息来源**：

1. 官方网站
2. Stackoverflow等论坛
3. 相关的博客

## 相关的教程

 1. 按照官网的教程能很快部署Github。边看边动手，你先试试吧[GithubPages官网地址](https://pages.github.com/)
 2. 如果遇到什么不明白的问题，请优先参考官网的指导[Github Pages Help](https://help.github.com/categories/github-pages-basics/)
 3. 如果官网的指导不能解决你的具体问题，请参考[Creating and Hosting a Personal Site on GitHub](http://jmcglone.com/guides/github-pages/)，这篇博客有详细的执行步骤。
 4. 对于想对博客进一步DIY的同学，可参考[利用GITHUBpage搭建个人博客](http://www.ituring.com.cn/article/197976?utm_source=tuicool)，这篇博客有关于如何实现站内搜索和留言评论等功能的介绍。

## 相关问题

事实上，我自己在建博客的过程中，走了不少弯路。虽然网上的资料很繁杂，但是实际上，不同的“指导”并不能完全解决自己具体遇到的问题，每出现一次问题还是需要自己花时间解决。并且有些资料实际上已经过期，会对你的判断造成误导，增加试错成本。

所以，我还是建议你，优先按照官方指导来。总之，祝你好运！

读到这里，相信你已经阅读过官方指导，大概了解了Github Pages。那么以下文章就是关于Github Pages的部署问题。

## 使用Github官方支持的工具Jkyll

>Q: 如何将你的博客生成网页，部署在你自己的`http://username.github.io`上呢？
>A: 使用Jkyll工具，将你的文章，自定义网站的设计，转化为静态网站和博客。

### [Jekyll安装](http://jekyllrb.com/docs/installation/)

 1. Jekyll安装之前，需要安装[Ruby](https://www.ruby-lang.org/en/downloads/)`实测下载速度很慢`，也可以通过直接[rubtinstall](http://rubyinstaller.org/)安装ruby`比之前那个链接下载速度稍微快一点`。备注：以上两个链接使用代理也很慢，所以Be patient。
如果你并不太了解如何安装，请使用[Windows下安装ruby](http://jingyan.baidu.com/article/48b558e33558ac7f38c09aee.html)
 2. 安装完ruby之后，还需要安装[rubygems](https://rubygems.org/pages/download)。下载完解压缩在文件夹中就ok。
 3. 以上两项完成后，打开ruby的命令行窗口，并输入以下命令
 
```
$ gem sources --add http://gems.ruby-china.org/ --remove https://rubygems.org/
$ gem sources -l
*** CURRENT SOURCES ***
$ gem install jekyll
```

注意：此处需要留心的是ruby的官网地址`**http://gems.ruby-china.org/**`
因为国内的GreatWall，所以在大陆的gems维护只能交由国内社区维护。因此，你就能理解为什么这里的sources地址是`**http://gems.ruby-china.org/**`。

如果你使用的是网上搜索的suorces地址，`https//gems.ruby-china.org/`或者是`https://gems.ruby-china.org/`，那么安装过程则会出现以下报错

>Error fetching https://ruby.taobao.org/:
        SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed (https://ruby.taobao.org/specs.4.8.gz)
        
>Error fetching https://gems.ruby-china.org/: 
SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed (https://gems.ruby-china.org/specs.4.8.gz)

原因是以上地址已不再维护gems。如果你先知道了这些，那么可以为你省点时间。 

如果你需要使用到`bundle exec jkyll serve`进行本地调试，请阅读下一小节Bundle安装。如果你只是使用`jkyll serve`进行调试，可以等你需要的时候再阅读。

### Bundle安装

你已经使用过ruby命令，请先切换到你的仓库地址，这里使用的是`C:\Software\AndroidProjects\Git\Thinny>`，试试看输入以下指令

```
$ gem bundle install
```

Opps，出现问题了，不过不用担心。按照提示来，你就能解决。

如果你安装过程中出现以下相似的问题，试着看看窗口的提示，然后使用`gem install wdm -v '0.1.1'`，问题就解决了。

很简单吧，你说呢。

> Gem::InstallError: The 'wdm' native gem requires installed build tools.
Please update your PATH to include build tools or download the DevKit from 'http://rubyinstaller.org/downloads' and follow the instructions at 'http://github.com/oneclick/rubyinstaller/wiki/Development-Kit'
An error occurred while installing wdm (0.1.1), and Bundler cannot continue.
Make sure that `gem install wdm -v '0.1.1'` succeeds before bundling.

### 下载安装DevKit

如果你按照以上步骤完成了，那么接下来你还可能会发现，命令行窗口会提示你安装Devkit。你接下来要做的就是它所提示的，安装Devkit开发工具。

[DevKit下载地址](http://rubyinstaller.org/downloads)
[Devkit Install Guide安装指导](https://github.com/oneclick/rubyinstaller/wiki/Development-Kit)

要是你下载并且安装了Devkit，接下来要做的，是打开ruby命令行窗口，依次输入`ruby dk.rb init`和`ruby dk.rb install`,那么你会得到和我一样的结果，如下所示：

> C:\Software\Devkit>ruby dk.rb init
[INFO] found RubyInstaller v2.3.1 at C:/Software/Ruby23-x64
Initialization complete! Please review and modify the auto-generated
'config.yml' file to ensure it contains the root directories to all
of the installed Rubies you want enhanced by the DevKit.
C:\Software\Devkit>ruby dk.rb install
[INFO] Installing 'C:/Software/Ruby23-x64/lib/ruby/site_ruby/2.3.0/rubygems/defaults/operating_system.rb'
[INFO] Installing 'C:/Software/Ruby23-x64/lib/ruby/site_ruby/devkit.rb'

恭喜你，到这一步，基本已经完成了。要是你不放心，可以阅读下一小节，进行验证你安装是否正确。

### 验证安装

按照指令输入并验证

> C:\Software\Devkit>gem install jason --platform=ruby
Fetching: jason-0.6.0.gem (100%)
Successfully installed jason-0.6.0
Parsing documentation for jason-0.6.0
Installing ri documentation for jason-0.6.0
Done installing documentation for jason after 0 seconds
1 gem installed

> C:\Software\Devkit>ruby -rubygems -e "require 'json'; puts JSON.load('[42]').inspect"
[42]

### 安装bundle

最后，回到本章节的开头，还记得你的指令么？

切换到你本机的仓库地址，然后输入指令：

```
$ gem bundle install
```

> C:\Software\AndroidProjects\Git\Thinny>bundle install
Fetching gem metadata from https://rubygems.org/............
Fetching version metadata from https://rubygems.org/...
Fetching dependency metadata from https://rubygems.org/..
Resolving dependencies...
Using i18n 0.7.0
Using json 1.8.3
Using minitest 5.9.1
Using thread_safe 0.3.5
Using addressable 2.4.0
Using coffee-script-source 1.10.0
Using execjs 2.7.0
Using colorator 1.1.0
Using colored 1.2
Using ffi 1.9.14
Using multipart-post 2.0.0
Using forwardable-extended 2.6.0
Using gemoji 2.1.0
Using net-dns 0.8.0
Using public_suffix 1.5.3
Using sass 3.4.22
Using rb-fsevent 0.9.7
Using kramdown 1.11.1
Using liquid 3.0.6
Using mercenary 0.3.6
Using rouge 1.11.1
Using safe_yaml 1.0.4
Using jekyll-feed 0.5.1
Using mini_portile2 2.1.0
Using jekyll-paginate 1.1.0
Using jekyll-sitemap 0.10.0
Using jekyll-swiss 0.4.0
Using minima 1.2.0
Using unicode-display_width 1.1.1
Using parallel 1.9.0
Using yell 2.0.6
Installing wdm 0.1.1 with native extensions
Using bundler 1.13.6
Using tzinfo 1.2.2
Using coffee-script 2.4.1
Using ethon 0.9.1
Using rb-inotify 0.9.7
Using faraday 0.9.2
Using pathutil 0.14.0
Using jekyll-sass-converter 1.3.0
Using nokogiri 1.6.8.1
Using terminal-table 1.7.3
Installing activesupport 4.2.7
Installing jekyll-coffeescript 1.0.1
Installing typhoeus 0.8.0
Installing listen 3.0.6
Installing sawyer 0.7.0
Installing html-pipeline 2.4.2
Installing html-proofer 3.3.1
Using jekyll-watch 1.5.0
Installing octokit 4.3.0
Installing jekyll 3.2.1
Installing github-pages-health-check 1.2.0
Installing jekyll-gist 1.4.0
Installing jekyll-github-metadata 2.1.1
Installing jekyll-mentions 1.2.0
Installing jekyll-redirect-from 0.11.0
Installing jekyll-seo-tag 2.0.0
Installing jemoji 0.7.0
Installing github-pages 98
Bundle complete! 3 Gemfile dependencies, 60 gems now installed.
Use `bundle show [gemname]` to see where a bundled gem is installed.
Post-install message from html-pipeline:
Thank you for installing html-pipeline!
You must bundle Filter gem dependencies.
See html-pipeline README.md for more details.
https://github.com/jch/html-pipeline#dependencies
Post-install message from github-pages:
Thank you for installing github-pages!
GitHub Pages recently upgraded to Jekyll 3.0, which
includes some breaking changes. More information:
https://github.com/blog/2100-github-pages-jekyll-3

Finally！完成了。

### 本机调试

到这步，你终于可以看看自己实现的博客了。1请先将ruby命令行窗口切换到你仓库的地址，然后使用`jkyll serve`。阅读窗口提示，打开浏览器，输入默认的地址`127.0.0.1:4000`。回车。

应该是你想象中的网页吧~

恭喜你，你可以在本机上调试你的博客了~

## 调试小记

我在用jekyll 3.3.0本地调试的时候`jekyll serve --watch `。
Ps:`jekyll serve`默认是会monitor file changes。出现了以下问题，你可以参考：
 
 >--watch arg is unsupported on Windows.
                    If you are on Windows Bash, please see: https://github.com/Microsoft/BashOnWindows/issues/216

[StackoverFlow解决办法](http://stackoverflow.com/questions/39970672/watch-arg-is-unsupported-on-windows)

修改办法是注释`C:\Software\Ruby23-x64\lib\ruby\gems\2.3.0\gems\jekyll-3.3.0\lib\jekyll\commands\build.rb`中的关于windows平台的限制。

如果卸载3.3.0，转用3.2.1也是可以的。请你等待bug修复。

### 参考链接

 1. [ERROR: Could not find a valid gem 'jekyll' (>= 0), here is why: #34](https://github.com/juthilo/run-jekyll-on-windows/issues/34)
 2. [taobao Gems 源已停止维护，现由 ruby-china 提供镜像服务](http://www.oschina.net/news/71749/taobao-gems-ruby-china?p=1#comments)
 3. [RubyGems 镜像](https://ruby.taobao.org/)

## 发布文章

你已经阅读过官方指导，但我还是提醒下。在你的仓库中_posts中，MD文章的名称必须是`2016-10-23-github-pages`也就是：`年-月-日-文章标题`。

你通过Github客户端或者是Git，将_posts中的文章push到你在Github上的仓库中，就完成了文章的发布。

## 后记

目前来看，从CSDN Markdown编辑器的MD文件不能直接发布在Jekyll上。各种Markdown编辑器对于markdown语言的支持不尽相同，也就是说，你的MD文章可能在博客中显示效果不同。这是由于Jekyll对于Markdown的支持程度。

选择一款你喜欢的Markdown编辑器吧。你就可以开始发博客了。

以上。

Good Luck！










