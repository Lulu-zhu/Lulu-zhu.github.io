---
layout: post
title: "利用GithubPages建博客"
quote: "test"
image:
      url: /media/2014-02-27-hello-cosette/cover.jpg
video: false
comments: true
theme_color: 302F2D
---

## Github Pages

之前在github看到有人在用仓库建博客的时候，就在想Github会不会直接做一个博客系统。在这之前一直使用CSDN markdown编辑器，这个编辑器对markdown的支持也做了很不错的更新。
闲下来上Github发现果然有这个功能。于是，当然是要开始吃螃蟹了。
根据网上的教程已经搭建完毕。[我的Github Page](http://lulu-zhu.github.io/)正在搭建，欢迎访问。
目前正在学习怎么用Git添加博客。

## 相关的教程

 1. 按照官网的教程能很快部署Github。试试吧[GithubPages官网地址](https://pages.github.com/)
 2. 如果遇到什么问题，可以先参考官网的指导[Github Pages Help](https://help.github.com/categories/github-pages-basics/)
 3. 如果是前端的同学话，当然可以自定义你的主页。Go and try！
 4. 具体的步骤请参考[Creating and Hosting a Personal Site on GitHub](http://jmcglone.com/guides/github-pages/)
 5. DIY的部分可参考[利用GITHUBpage搭建个人博客](http://www.ituring.com.cn/article/197976?utm_source=tuicool)

## 遇到的相关问题

事实上，在建博客的过程中，走了不少弯路。原因是网上的资料很繁杂，并且有些已经过期。不同的`指导`实际上都不能完全解决具体遇到的问题。所以，祝你好运。
以下是在部署中遇到的问题，可参考：

## [Jekyll安装](http://jekyllrb.com/docs/installation/)

 1. Jekyll安装需要安装[Ruby](https://www.ruby-lang.org/en/downloads/)`实测下载速度很慢`，也可以通过直接[rubtinstall](http://rubyinstaller.org/)安装ruby`比之前那个链接下载速度稍微快一点`。备注：以上两个链接用代理也很慢，所以Be patient。百度经验以备不时之需，[Windows下安装ruby](http://jingyan.baidu.com/article/48b558e33558ac7f38c09aee.html)
 2. 安装完ruby之后，还需要安装[rubygems](https://rubygems.org/pages/download)。下载完解压缩就ok。
 3. 以上两项完成后，打开ruby的命令窗口

```
$ gem sources --add http://gems.ruby-china.org/ --remove https://rubygems.org/
$ gem sources -l
*** CURRENT SOURCES ***
$ gem install jekyll
```

注意：此处需要注意的是**http://gems.ruby-china.org/**
因为GreatWall，此处gems的维护只能交由国内社区维护。所以需要改sources。
要是你使用网上搜索的https//gems.ruby-china.org/或者是https://gems.ruby-china.org/会出现报错

>Error fetching https://ruby.taobao.org/:
        SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed (https://ruby.taobao.org/specs.4.8.gz)
        
>Error fetching https://gems.ruby-china.org/: 
SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed (https://gems.ruby-china.org/specs.4.8.gz)
原因是以上地址已不再维护gems。 

### Gem Bundle install

> Gem::InstallError: The 'wdm' native gem requires installed build tools.
Please update your PATH to include build tools or download the DevKit from 'http://rubyinstaller.org/downloads' and follow the instructions at 'http://github.com/oneclick/rubyinstaller/wiki/Development-Kit'
An error occurred while installing wdm (0.1.1), and Bundler cannot continue.
Make sure that `gem install wdm -v '0.1.1'` succeeds before bundling.

### 下载安装DevKit
[DevKit下载地址](http://rubyinstaller.org/downloads)
[Devkit Install Guide](https://github.com/oneclick/rubyinstaller/wiki/Development-Kit)

以下是按照步骤，以备查错

> C:\Software\Devkit>ruby dk.rb init
[INFO] found RubyInstaller v2.3.1 at C:/Software/Ruby23-x64
Initialization complete! Please review and modify the auto-generated
'config.yml' file to ensure it contains the root directories to all
of the installed Rubies you want enhanced by the DevKit.
C:\Software\Devkit>ruby dk.rb install
[INFO] Installing 'C:/Software/Ruby23-x64/lib/ruby/site_ruby/2.3.0/rubygems/defaults/operating_system.rb'
[INFO] Installing 'C:/Software/Ruby23-x64/lib/ruby/site_ruby/devkit.rb'

### 验证安装

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

Finally！完成

### 参考链接

 1. [ERROR: Could not find a valid gem 'jekyll' (>= 0), here is why: #34](https://github.com/juthilo/run-jekyll-on-windows/issues/34)
 2. [taobao Gems 源已停止维护，现由 ruby-china 提供镜像服务](http://www.oschina.net/news/71749/taobao-gems-ruby-china?p=1#comments)
 3. [RubyGems 镜像](https://ruby.taobao.org/)

目前来看，从CSDN Markdown编辑器的MD文件不能直接发布在Jekyll上。Jekyll对于Markdown的支持还有待改进。

以上。

Good Luck！







