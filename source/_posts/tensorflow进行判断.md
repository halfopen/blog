title: tensorflow进行判断
author: Halfopen
tags:
  - tensorflow
categories:
  - 机器学习
date: 2018-08-13 21:52:00
---
直接在graph里进行判断会出现以下错误：

```
TypeError: Using a `tf.Tensor` as a Python `bool` is not allowed
```

这里可以使用 a is not None或者使用tf.cond

```python
import tensorflow as tf
import numpy as np


pred = tf.placeholder(tf.bool, shape=[])
x = tf.Variable([1])

def f1():
    return tf.Variable(1)

def f2():
    return tf.Variable(2)

y = tf.cond(pred, f1, f2)

with tf.Session() as session:
  session.run(tf.initialize_all_variables())
  print(session.run(y, feed_dict={pred:True}))
  print(session.run(y, feed_dict={pred:False}))
  print(y.eval(feed_dict={pred: True}))
  print(y.eval(feed_dict={pred: False}))
  print(y.eval(feed_dict={pred: False}))
  
```

