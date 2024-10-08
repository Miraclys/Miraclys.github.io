---
title: tmux 使用
date: 2024-02-01 10:05:33
tags:
description: the configuration and use of tmux
---

tmux（terminal multiplexer）是一款终端复用器，很有用，属于常用的开发工具。

tmux attach -t session_name 重新连接到一个已经存在的会话

tmux kill-session -t session_name 关闭一个会话

tmux new -s session_name 创建一个新的会话

prefix + d 退出当前会话

prefix + w 列出当前会话的所有窗口

prefix + c 创建一个新窗口

prefix + " 横向分割当前窗口，分为上下两部分

prefix + % 纵向分割当前窗口，分为左右两部分

prefix + x 关闭当前窗口

tmux 中有会话、窗口和面板的概念，分别是 session、window 和 pane。

启动 tmux 时会启动一个服务器，它可以同时管理多个会话。

每个会话包含多个窗口。会话可以独立存在，允许你为不同的任务或项目创建隔离的工作环境。

每个窗口对应于一个终端窗口，一个会话可以有多个窗口。窗口可以在同一会话内切换，窗口内可以进一步拆分为多个窗格。

窗口内的子单元，一个窗口可以拆分为多个窗格，每个窗格是一个独立的终端区域，可以并行操作和查看。

1. https://www.ruanyifeng.com/blog/2019/10/tmux.html

2. https://zhuanlan.zhihu.com/p/98384704

3. https://cloud.tencent.com/developer/article/1530522
