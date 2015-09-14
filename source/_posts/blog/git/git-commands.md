title: git常用命令
date: 2015-09-06 10:09:39
categories: blog
tags: git
keywords: git
---
##### 创建标签
```bash
git tag -a v1.0.0 -m "version 1.0.0"
```
##### 删除标签
```bash
git tag -d v1.0.0
```
<!-- more -->
##### 恢复单个被误删的文件
```bash
git checkout --README.md
```
##### 恢复全部被误删的文件
```bash
git ls-files -d | xargs git checkout --
```