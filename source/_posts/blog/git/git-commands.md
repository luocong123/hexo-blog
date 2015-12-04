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
##### 合并分支
如需把dev分支合并到master分支，则先要切换到master分支  

```bash
git checkout master
get merge dev
```
默认是fast-forward方式，fast-forward方式就是当条件允许的时候，git直接把HEAD指针指向合并分支的头，完成合并。属于“快进方式”，不过这种情况如果删除分支，则会丢失分支信息。因为在这个过程中没有创建commit,如果不想快速合并，你可以：

```bash
get merge dev --no-ff  
```
no-ff：不使用fast-forward方式合并，保留分支的commit历史  

```bash
get merge dev --squash  
```
squash：使用squash方式合并，把多次分支commit历史压缩为一次，比如说，你的dev在开发的时候写的commit很乱，那么我们合并的时候不希望把这些历史commit带过来，于是使用--squash进行合并，此时文件已经同合并后一样了，但不移动HEAD，不提交。需要进行一次额外的commit来“总结”一下，然后完成最终的合并
##### 恢复单个被误删的文件
```bash
git checkout --README.md
```
##### 恢复全部被误删的文件
```bash
git ls-files -d | xargs git checkout --
```