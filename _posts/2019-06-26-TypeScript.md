---
layout: post
title:  初识TypeScript
summary: "TypeScript"
date:   2019-6-26 20:51:18 +0700
categories: js知识点
tags: 'js知识点'
author: 曾宇媚
comment: true
---

&emsp;作为前端开发程序猿，JavaScript可以说是我们最先开始接触且是必须不断深入学习的语言，在敲代码过程中不断帮助自己探索关于它的特性。然而，在开发过程中，我们常常遇到运行得到的结果与自己预期不相符的情况，由于JavaScript解释性语言的特点，所以我们往往要在调试过程中才能最终判断一个变量或者一个函数最终返回的是什么类型的值，这是它的便利，但同时类型不确定也带来了很多问题。

&emsp;在项目中开发主要是用到了TypeScript，所以我也花时间去了解学习它，并整理如下自己的学习心得，若有叙述不当之处，欢迎大家批评指正。

# 什么是TypeScript？

官方是这么介绍的：
>TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. Any browser. Any host. Any OS. Open source.

&emsp;一提起TypeScript，大家的第一印象就是：它是JavaScript的一个超集，是强类型的语言。我对它的理解，主要从它和JavaScript的对比出发，


## 初次使用TypeScript
### 强类型变量
一开始使用TypeScript给我最大的不同时，需要在定义变量时就要明确它的数据类型。

    @Prop() private msg!: string;
    @Prop() private name!: string;
    @Prop() private memberCount!: number;
    
上面这些变量在定义时就已经明确了它的数据类型，因此在如果该变量不是定义的类型，就会报错。

另外，是在函数参数中，也需要定义参数的类型

    export default class nameClass extends Vue{
		private onModifyName(name: string) {
	      this.$emit('modify-name', name);
	    }
	}
    
如果传入变量可以是任意类型，就定义其数据类型为'any'

### 类

Typescript引入了类的概念，类似c语言，可以使用三种访问修饰符，分别是public、private和protected

* **public**: 修饰的属性或方法是公有的，可以在任何地方被访问到，默认是public;
* **private**: 修饰的属性或方法是私有的，不能在声明它的类的外部访问;
* **protected**: 修饰的属性或方法是受保护的，它和private类似，区别是它在子类中也是允许被访问的。

例如上面写的 onModifyName() 函数，前面的修饰符是private，因此它就只能在定义它的类中访问。


## 小结
TypeScript是JavaScript的超集，语法上其实和js是差不多，但增加了变量的强类型和class中函数的修饰符，使得它在出现错误时能比较快地定位到可能发生错误的地方。

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
