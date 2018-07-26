title: 在flask/django中调用hdf5模型
author: Halfopen
date: 2018-05-31 17:42:34
tags:
---
之前直接写，可能会出现　`is not an element of this graph`的问题，解决方法如下：
```python
import tensorflow as tf

...

g = tf.Graph()
with g.as_default():
    print("Loading model")
    model = load_model(os.path.join(MODEL_DIR, 'classifier_model.hdf5'))

...

@app.route('/', methods=['GET','POST'])
def index():
    ...

    with g.as_default():
        round_predict = model.predict_classes(scaled_predict_data,verbose=0)

    ...
```


参考：

https://stackoverflow.com/questions/49018861/tensorflow-keras-flask-unable-to-run-my-keras-model-as-web-app-via-flask