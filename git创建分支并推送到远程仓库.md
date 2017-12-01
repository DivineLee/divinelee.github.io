---
title: git创建分支并推送到远程仓库
categories:
  - 日常总结
tags:
  - git
date: 2017-11-29 23:43:52
archives:
---

提交一个文件到本地仓库
DivineLee@Lee MINGW64 ~ (master)
$ git commit -m "a"
[master (root-commit) 2958cbe] a
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 a.txt

查看本地分支
DivineLee@Lee MINGW64 ~ (master)
$ git branch
 *master

新建分支
DivineLee@Lee MINGW64 ~ (master)
$ git branch hexo

DivineLee@Lee MINGW64 ~ (master)
$ git branch
  hexo
 *master

推送分支到远程仓库
DivineLee@Lee MINGW64 ~ (master)
$ git push origin hexo
Counting objects: 3, done.
Writing objects: 100% (3/3), 198 bytes | 198.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:DivineLee/divinelee.github.io.git
 *[new branch]      hexo -> hexo
