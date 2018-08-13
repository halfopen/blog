title: 'ValueError: No variables to optimize.'
author: Halfopen
tags:
  - tensorflow
categories:
  - 机器学习
date: 2018-08-13 16:39:00
---
```
ValueError: No variables to optimize.
```

1. 没有进行feed_dict

2. 有tensor在初始化之后出现
	构建图的时候　with graph.as_default():

3. 没有进行变量初始化
	self.sess = tf.Session()
    self.sess.run(tf.global_variables_initializer())
