---
title: hexo blog instructions list
date: 2023-08-23 15:52:48
description: a list of basic instructions of hexo.
---

| 指令                                    | 操作             |
| --------------------------------------- | ---------------- |
| hexo n "我的博客" / hexo new "我的博客" | 新建文章         |
| hexo p / hexo publish                   | 发表草稿文章     |
| hexo g / hexo generate                  | 生成             |
| hexo s / hexo server                    | 启动本地预览服务 |

### 插入图片
1. 
由于我们的博客是要部署在网站上，部署后会生成新的文件目录，所以我们选择使用相对路径的方式。
在 hexo 中使用 **文章资源文件夹** 需要在 `config.yaml` 文件中更改一下配置：
```
post_asset_folder: true
``` 
当该配置被应用后，使用 hexo new 命令创建新文章时，会生成相同名字的文件夹，也就是文章资源文件夹。
但是若干原因，需要使用 `{ %asset_image xxx.jpg 这是一张图片% }` 来引用。
2. 
另一种方法是，在 `source` 文件夹下建立一个文件夹 `_pic` 专门用来存放图片，此时在 md 文件中 `![img](/_pic/xxx.jpg)` 的格式引用就可以了。
(不知道为啥这种没成功)

### 搭建参考

1. https://zhuanlan.zhihu.com/p/94038688#:~:text=hexo

2. https://zhuanlan.zhihu.com/p/44213627

3. https://segmentfault.com/a/1190000002632530 hexo 常用命令笔记

4. https://blog.csdn.net/as480133937/article/details/100138838 hexo 博客美化配置

5. https://theme-next.js.org/docs/getting-started/

6. https://theme-next.js.org/docs/theme-settings/

7. https://hexo.io/zh-cn/docs/configuration

8. https://zhuanlan.zhihu.com/p/552639819

9. https://blog.csdn.net/qq_34243930/article/details/103994419#2_65 关于 hexo 创建文章的讲解

10. https://zhuanlan.zhihu.com/p/265077468 hexo 博客插入图片