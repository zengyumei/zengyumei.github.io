---
layout: post
title:  利用 Github + jekyll 搭建个人博客
summary: "搭建自己的个人博客"
date:   2018-12-16 16:19:52 +0700
categories: jekyll
tags: '个人博客'
author: 曾宇媚
comment: true
---

第一次尝试利用Jekyll来搭建个人博客，从开始的慢慢摸索，到成功发布自己的第一篇博文，学习到了很多。下面想将自己的经历和大家一起分享。


### 前言

在科研学习过程中遇到不懂的问题就会去网上查找参考资料，发现博客是干货最多而且有很多是大佬们分享的各类知识，看完一篇博文能帮助自己不少。这时我就萌生了想搭建自己的个人博客这一想法，所以就去学习如何开始搭建自己的个人博客了。

### 入门准备

搭建个人博客的方法很多，最终我选择了利用Jekyll来搭建个人博客。

[jekyll](http://jekyll.com.cn/)是一个静态站点生成器，会根据网页源码生成静态文件。它有一个模板目录，其中包含原始文本格式的文档，因此可以通过Markdown（或者Textile）、Liquid转化成一个完整的可发布的静态网站。Jekyll也可以运行在Github Page上，我们可以利用Github的服务来搭建自己的博客。

使用 Jekyll 搭建博客之前要确认下本机环境，如Git环境（用于将博客部署到远端）、Ruby 环境（Jekyll是基于Ruby开发的）、包管理器 [RubyGems](http://rubygems.org/pages/download)等。 

### 环境配置

1. **注册一个Github账号，并为博客创建一个仓库，仓库一般以用户名.github.io命名**[参照此教程](https://blog.csdn.net/Maple_ROSI/article/details/79484691)

2. **下载Git，用于将博客部署到远端**, [git for windows](https://git-for-windows.github.io/)， 以及[windows下的安装教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137396287703354d8c6c01c904c7d9ff056ae23da865a000)

3. **安装Ruby 和 DevKit**, Window 系统下，我们可以使用 RubyInstaller 来安装 Ruby 环境，[下载地址](http://rubyinstaller.org/downloads/), [安装教程](https://blog.csdn.net/qiujuer/article/details/44620019)

4. **完成以上环境安装之后，接着配置jekyll环境**

* 安装 jekyll

```
$ gem install jekyll
```
出现错误：
```
ERROR: Could not find a valid gem 'jekyll' (>= 0) in any repository
```
原因： rubygems.org被block了，需要使用国内镜像
```
$ gem sources --remove https://rubygems.org/
$ gem sources --add http://ruby.taobao.org/
```
再次运行:
```
$ gem install jekyll
```
命令行显示：
```
Fetching: public_suffix-3.0.3.gem (100%)
Successfully installed public_suffix-3.0.3
Fetching: addressable-2.5.2.gem (100%)
Successfully installed addressable-2.5.2
……
25 gems installed
```
此时 jekyll 安装完成

* 创建博客

```
$ cd
//选择目录
$ jekyll new blog
```

出现了如下错误：

```
ERROR: Coulf not load Bundler.Bundle install skipped.
New jekyll site installed in C://ruby路径/blog
```

原因：没有安装 bundler , 因此回退到 ruby 路径，执行安装 bundler 命令

```
$ cd ..
$ gem install jekyll bundler
```

命令行显示：

```
Successfully installed jekyll-3.8.5
Parsing documentation for jekyll-3.8.5
Done installing documentation for jekyll after 0 seconds
Fetching: bundler-1.17.2.gem (100%)
Successfully installed bundler-1.17.2
Parsing documentation for bundler-1.17.2
Installing ri documentation for bundler-1.17.2
Done installing documentation for bundler after 4 seconds
2 gems installed
```

* 进入博客目录

```
$ cd blog
```

* 启动本地服务
```
$ jekyll serve
```

出现了以下一些错误，都是由于缺少了相应的依赖

```
C:/Ruby25-x64/lib/ruby/gems/2.5.0/gems/bundler-1.17.2/lib/bundler/resolver.rb:287:in `block in verify_gemfile_dependencies_are_found!': Could not find gem 'minima (~> 2.0) x64-mingw32' in any of the gem sources listed in your Gemfile. (Bundler::GemNotFound)
```

提示缺少 minima，继续安装

```
$ gem install jekyll minima
```

```
C:/Ruby25-x64/lib/ruby/gems/2.5.0/gems/bundler-1.17.2/lib/bundler/resolver.rb:287:in `block in verify_gemfile_dependencies_are_found!': Could not find gem 'tzinfo-data x64-mingw32' in any of the gem sources listed in your Gemfile. (Bundler::GemNotFound)
```

提示缺少 tzinfo-data，继续安装

```
gem install jekyll tzinfo-data
```

```
C:/Ruby25-x64/lib/ruby/gems/2.5.0/gems/bundler-1.17.2/lib/bundler/resolver.rb:287:in `block in verify_gemfile_dependencies_are_found!': Could not find gem 'wdm (~> 0.1.0) x64-mingw32' in any of the gem sources listed in your Gemfile. (Bundler::GemNotFound)
```

提示缺少 wdm，继续安装

```
$ gem install jekyll wdm
```

然后重新启动本地服务

```
$ jekyll serve
```

在浏览器里输入： [http://localhost:4000](http://localhost:4000)，就可以看到你的博客效果了。

![这是我的博客主页](C:/Ruby25-x64/blog/zengyumei.github.io/assets/images/Jekyll_blog.png)

### 目录结构

Jekyll 的核心其实是一个文本转换引擎。它的概念其实就是： 你用你最喜欢的标记语言来写文章，可以是 Markdown，也可以是 Textile,或者就是简单的 HTML, 然后 Jekyll 就会帮你套入一个或一系列的布局中。在整个过程中你可以设置URL路径, 你的文本在布局中的显示样式等等。这些都可以通过纯文本编辑来实现，最终生成的静态页面就是你的成品了。

一个基本的 Jekyll 网站的目录结构一般是像这样的：


```
.
├── _config.yml
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   ├── post.html
|   └── page.html
├── _posts
|   └── 2016-10-08-welcome-to-jekyll.markdown
├── _sass
|   ├── _base.scss
|   ├── _layout.scss
|   └── _syntax-highlighting.scss
├── about.md
├── css
|   └── main.scss
├── feed.xml
└── index.html

```

这些目录结构以及具体的作用可以参考 [官网文档](http://jekyll.com.cn/docs/structure/) 

进入 _config.yml 里面，修改成你想看到的信息，重新 jekyll server ，刷新浏览器就可以看到你刚刚修改的信息了。

到此，博客初步搭建算是完成了，

### 将博客部署到远端

部署到远端即是部署到Github Page上，把刚才建立的blog项目push到（github用户名.github.io）仓库中，

运行命令

```
git add .
git commit -m "我的博客"
git remote add origin https://github.com/(github用户名)/(github仓库名).git
git push -u origin master
```

然后我们在浏览器中输入http://github用户名.github.io， 就可以访问自己的博客啦

### 编写文章

博客中所有的文章都是在_post目录下，文章格式为markdown格式，文章的文件名可以是 .markdown 或者 .md 。

编写一篇新的文章，文章命名必须为 年-月-日-article1.markdown/md

**注意**：文章名的格式前面必须为 年-月-日- 格式，如 2018-12-16- ，日期可以修改成当前日期。后面的 article1 是整个文章的连接 URL，如果文章名为中文，那么文章的连接URL就会变成这样的：http://username.github.io/2015/08/%E6%90%AD%E5/ ， 所以建议文章名最好是英文的或者阿拉伯数字。 

双击 2016-06-28-welcome-to-jekyll.markdown 打开

```
---
layout: post
title:  "Welcome to Jekyll!"
crawlertitle: "How to use jekyll"
summary: "Jekyll default page"
date:   2016-06-28 23:09:47 +0700
categories: posts
tags: 'jekyll'
author: redVi
---

正文...
```

title: 显示的文章名， 如：title: 我的第一篇文章                    
date:  显示的文章发布日期，如：date: 2018-12-16                          
categories: tag标签的分类，如：categories: 随笔            
author: 作者名称

注意：文章头部格式必须为上面的，... 就是文章的正文内容。

我写文章使用的是 Sublime Text3 编辑器，[Markdown简单语法](http://www.appinn.com/markdown/)


### 使用博客模板

虽然博客部署完成了，你会发现博客太简单不是你想要的，[这里有很多漂亮的模板](http://jekyllthemes.org/)。

选择你喜欢的模板下载解压到目录下， 将_config.yml, _posts修改成自己的信息和文章，再次开启本地服务，就可以看到新换后的博客模板啦


### 总结

所以通过配置jekyll环境，我们就可以通过在站点文件夹中运行 jekyll server命令并通过 http://localhost:4000 查看我们对网页做出的修改，修改满意后再push到 github 远程仓库，然后就通过 http://username.github.io 访问自己的博客啦。

### 写在最后

这是我的第一篇博文，从刚开始安装环境遇到的各种问题，到最后成功发布第一篇文章，看到这个博客有了雏形内心很激动，有了一个学习分享的基地，督促自己向优秀的人看齐！

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
