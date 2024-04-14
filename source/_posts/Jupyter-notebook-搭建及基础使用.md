---
title: Jupyter notebook 搭建及基础使用
date: 2024-04-07 21:30:15
tags:
- Jupyter Notebook
---

### 搭建

配置文件的地址：C:\Users\24964\.jupyter\jupyter_notebook_config.py

c.NotebookApp.ip = '*' #所有绑定服务器的IP都能访问，若想只在特定ip访问，输入ip地址即可
c.NotebookApp.port = 6666 #将端口设置为自己喜欢的吧，默认是8888
c.NotebookApp.open_browser = False #我们并不想在服务器上直接打开Jupyter Notebook，所以设置成False
c.NotebookApp.notebook_dir = '/root/jupyter_projects' #这里是设置Jupyter的根目录，若不设置将默认root的根目录，不安全
c.NotebookApp.allow_root = True # 为了安全，Jupyter默认不允许以root权限启动jupyter 

这是一些基础配置

$ jupyter notebook 启动 Jupyter notebook

