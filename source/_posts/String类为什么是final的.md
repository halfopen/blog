title: String类为什么是final的
author: Halfopen
tags:
  - java基础
categories:
  - java
date: 2017-12-04 19:09:00
---
java有几个基本类型，byte、short、char、int、long、float、double和boolean

实际上也有对应的类，Byte, Short Character, Integer, Long, Float, Double Boolean,不只是String, 这些类也都是final类型的

[参考知乎上的回答](https://www.zhihu.com/question/31345592)

如果String对象可变的话，在我们平常的程序编写中将会带来极大的安全隐患，而如果想杜绝这种隐患，则每次在使用String时都要经过精密考虑，程序也会变得更复杂，而偏偏String是被大量使用的（实际上不管哪种编程语言，字符串及其处理都占有相当大的比重），显然会给我们日常的程序编写带来极大的不便。

如果是不可变的话，传参String类型时就可以看做是按值传递的，不用担心会被修改。

另外一个值得注意的地方就是数组变量名其实也是一个引用，所以final修饰数组时，数组成员依然可以被改变。

这样做还有一个好处，java底层有一个常量池，这样在大量使用字符串的情况下，可以节省内存空间，提高效率。