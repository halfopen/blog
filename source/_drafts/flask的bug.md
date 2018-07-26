title: flask的bug
author: Halfopen
date: 2018-06-05 22:40:30
tags:
---
# flask_sqlalchemy
```
ImportError: No module named 'flask.ext'
```

请把flask 和　flask_sqlalchemy 升级到最新版
```
pip install -U flask
pip install -U Flask-SQLAlchemy

```
