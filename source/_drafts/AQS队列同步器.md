title: AQS队列同步器
author: Halfopen
tags:
  - 并发
categories:
  - java
date: 2018-04-02 23:07:00
---
AbstractQueuedSynchronizer是用来构建锁或者其他同步组件的基础框架，它使用了一个int成员变量表示同步状态，通过内置的FIFO队列来完成资源获取线程的排队工作，并发包的作者（Doug Lea）期望它能够成为实现大部分同步需求的基础

