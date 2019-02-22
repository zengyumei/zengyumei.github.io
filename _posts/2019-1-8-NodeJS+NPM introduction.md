---
layout: post
title:  NodeJS和NPM的入门整理
summary: "介绍NodeJS和NPM"
date:   2019-1-8 14:25:23 +0700
categories: 框架和工具
tags: '框架和工具'
author: 曾宇媚
comment: true
---

由于组里可视化项目的需求，我需要搭建一个网站来进行数据的展示、统计分析等，网站模块很多，涉及到很多工具和库。我通过一步步的查找资料，发现node.js是目前比较火热的js后端开发工具，因此接下来我将会简单介绍一下nodejs和npm这两个工具。


### NodeJS

Node.js是目前比较火热的技术，简单的说它是运行在服务端的JavaScript，是一个基于Chrome V8 引擎的JavaScript运行时搭建的一个平台。  



#### Node.js安装
由于Node.js平台是在后端运行JavaScript代码，所以，必须首先在本机安装Node环境。
  
从[Node.js官网](https://nodejs.org/en/)下载对应平台的安装程序。
安装完成后，在Windows环境下，打开命令提示符，然后输入**node -v**
可以看到当前安装的node.js的版本信息。 
 
```
C:\>node -v
v10.15.0
```

在命令提示符输入**node**，此刻你将进入Node.js的交互环境。在交互环境下，你可以输入任意JavaScript语句，并能够直接运行。

#### Node.js的优势
- 在Node上运行的JavaScript相比其他后端开发语言有何优势？
- 最大的优势是借助JavaScript天生的事件驱动机制加V8高性能引擎，使编写高性能Web服务轻而易举。
- 非常快的内置谷歌Chrome的V8 JavaScript引擎，Node.js库代码执行是非常快的。
- 单线程但高度可扩展 - Node.js使用具有循环事件单线程模型。事件机制有助于服务器在一个非阻塞的方式响应并使得服务器高度可扩展，而不是创建线程限制来处理请求的传统服务器。Node.js使用单线程的程序，但可以提供比传统的服务器(比如Apache HTTP服务器)的请求服务数量要大得多。
- 没有缓冲 - Node.js的应用从来不使用缓冲任何数据。这些应用只是输出数据在块中。

### NPM

在正式开始Node.js学习之前，我们先认识一下npm。 
 
npm是什么？npm其实是Node.js的包管理工具（package manager）。  
**这个包管理工具有什么作用呢？ ** 

- 当我们在Node.js上开发时，会用到很多别人写的JavaScript代码。如果我们要使用别人写的某个包，每次都根据名称搜索一下官方网站，下载代码，解压，再使用，非常繁琐。于是一个集中管理的工具应运而生：大家都把自己开发的模块打包后放到npm官网上，如果要使用，直接通过npm安装就可以直接用，不用管代码存在哪，应该从哪下载。  
- 更重要的是，如果我们要使用模块A，而模块A又依赖于模块B，模块B又依赖于模块X和模块Y，npm可以根据依赖关系，把所有依赖的包都下载下来并管理起来。否则，靠我们自己手动管理，肯定既麻烦又容易出错。
#### npm安装

其实npm已经在Node.js安装的时候顺带装好了。我们在命令提示符或者终端输入 **npm -v**，会输出npm的版本信息。
```
C:\>npm -v  
6.4.1
```

### 创建Node程序

在未安装Node.js之前，我编写的JavaScript代码都是在浏览器中运行的，而当安装了Node环境之后，以后所编写的JavaScript代码就是在Node环境中执行了。  

使用文本编辑器来开发Node程序，最大的缺点是效率太低，运行Node程序还需要在命令行单独敲命令。如果还需要调试程序，就更加麻烦了。

所以我们需要一个IDE集成开发环境，让我们能在一个环境里编码、运行、调试，这样就可以大大提升开发效率。

网上很多大牛们推荐了Visual Studio Code。由微软出品，但它不是那个大块头的Visual Studio，它是一个精简版的迷你Visual Studio，并且，Visual Studio Code可以跨平台，在Windows、Mac和Linux中都通用。 
   
在VS Code中，我们可以非常方便地运行JavaScript文件。

VS Code以文件夹作为工程目录（Workspace Dir），所有的JavaScript文件都存放在该目录下。此外，VS Code在工程目录下还需要一个.vscode的配置目录，里面存放里VS Code需要的配置文件。

假设我们在C:\Work\目录下创建了一个hello目录作为工程目录，并编写了一个hello.js文件，则该工程目录的结构如下：

```  
hello/ <-- workspace dir    
|
+- hello.js <-- JavaScript file   
|
+- .vscode/  <-- VS Code config       
   |
   +- launch.json <-- VS Code config file for JavaScript
```

在我们创建 Node.js 第一个 "Hello, World!" 应用前，让我们先了解下 Node.js 应用是由哪几部分组成的：

**1. 引入 required 模块**：我们可以使用 require 指令来载入 Node.js 模块，并将实例化的 HTTP 赋值给变量 http。
```
var http = require('http');
```

**2. 创建服务器**：服务器可以监听客户端的请求，类似于 Apache 、Nginx 等 HTTP 服务器。  
使用 http.createServer() 方法创建服务器，并使用 listen 方法绑定 8888 端口。 函数通过 request, response 参数来接收和响应数据。

```

//导入http模块
var http = require('http');

// 创建http server，并传入回调函数
var server = http.createServer(function (request, response) {

// 回调函数接收request和response对象,获得HTTP请求的method和url
console.log(request.method + ': ' + request.url);

// 将HTTP响应200写入response, 同时设置Content-Type: text/html
response.writeHead(200, {'Content-Type': 'text/html'});

// 将HTTP响应的HTML内容写入response
response.end('<h1>Hello world!</h1>');
});

// 让服务器监听8080端口
server.listen(8080);

//终端打印
console.log('Server is running at http://127.0.0.1:8080/');

```

**3. 接收请求与响应请求**：服务器很容易创建，客户端可以使用浏览器或终端发送 HTTP 请求，服务器接收请求后返回响应数据。

以上代码我们完成了一个可以工作的 HTTP 服务器。
使用 node 命令执行以上的代码：

```
node server.js
Server running at http://127.0.0.1:8080/
```

接下来，打开浏览器访问 http://127.0.0.1:8080/，既可以获得对应的网页，得到你所展示的内容。

#### 模块

计算机程序的开发过程中，随着程序代码越写越多，在一个文件里代码就会越来越长，越来越不容易维护。

为了编写可维护的代码，我们把很多函数分组，分别放到不同的文件里，这样，每个文件包含的代码就相对较少，很多编程语言都采用这种组织代码的方式。在Node环境中，一个.js文件就称之为一个模块（module）。

使用模块有什么好处？

- 最大的好处是大大提高了代码的可维护性。其次，编写代码不必从零开始。当一个模块编写完毕，就可以被其他地方引用。我们在编写程序的时候，也经常引用其他模块，包括Node内置的模块和来自第三方的模块。
- 使用模块还可以避免函数名和变量名冲突。相同名字的函数和变量完全可以分别存在不同的模块中，因此，我们自己在编写模块时，不必考虑名字会与其他模块冲突。

如上面hello world程序中，就引入了http模块，使得它能够在浏览器中运行http服务。


[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
