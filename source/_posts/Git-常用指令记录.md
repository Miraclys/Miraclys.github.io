---
title: Git 常用指令记录
date: 2024-02-26 23:50:05
tags: 
- Git
description: record some common git commands. 
---

网址：https://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html

1. 查看 Git 用户名和邮箱地址
    ```
    git config user.name
    git config user.email
    ```
2. 修改用户名和邮箱地址
    ```
    git config --global user.name "username"
    git config --global user.email "useremail"
    ```
3. `git init` 在当前目录新建一个 Git 代码库
4. `git clone [url]` down 一个项目到本地
5. `git config` 显示当前的 Git 配置
6. `git add [file1] [file2]` 添加文件到「暂存区」
7. `git add [dir]` 添加目录到暂存区，包括子目录
8. `git add .` 添加当前目录的所有文件到暂存区
9. `git commit -m "message"` 提交暂存区到仓库区
10. `git branch` 列出本地所有分支
11. `git branch -r` 列出远程所有分支
12. `git checkout [branch-name]` 切换到指定分支，并且更新工作区
13. `git merge [branch]` 合并指定分支到当前分支
14. `git branch -d [branch-name]` 删除分支
15. `git status` 显示所有变更文件
16. `git log` 显示当前分支到历史版本
17. `git log -S [keyword]` 根据关键词搜索提交历史
18. `git fetch [remote]` 下载远程仓库的所有变动
19. `git remote -v` 显示所有的远程仓库
20. `git remote` 显示远程仓库的别名（没有 -v 的信息全）
21. `git branch -m <old_branch_name> <new_branch_name>` 可以用来重命名分支
22. `git config --global init.defaultBranch <branch-name>` 可以用来配置默认分支
