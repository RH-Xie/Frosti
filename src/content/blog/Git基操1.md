---
title: Git基操（1）
pubDate: 2023-03-21 14:49:18
tags:
  - Git
  - 团队协作
description: 基操篇。Git用了一段时间，反复体验下来总结一套流程，以及处理了一些常见需求，现在是命令行选手了。下一篇总结Git的协作模式。
image: https://images.weserv.nl/?url=s2.loli.net/2023/09/01/GUIBnxyM25gvkLA.webp
---



# Git

【认证】如果换了设备、重装了系统·，Permission Deny，那需要在本地重新生成ssh-rsa，然后去github上建立这个key，才能post（奇怪的是没有弹出之前的登录账号）

## 如何更新一个文件

```tsx
git add <要更新的文件>
git commit -m '注释，不如一"-"而过？'
git push origin master -u
```

## 查看状态、版本和仓库

本地：git status

远程：git remote -v

## origin是什么

origin是指代仓库url的变量，可以用origin以缩短命令

## 比较与合并

git fetch后，比对一下本地仓库和远程仓库：

![](https://s2.loli.net/2023/09/01/JGiNj4xZrVwf21M.png)

origin是地址，main是github默认的远程分支名

## 绿色的U

在VSCode里，文件后的U指Unchecked，和Vue没关系

还有：

- A：Added，已添加暂存区
- M：Modified，被修改

VSCode在提示框里输入注释

## 如何在git中指定只要某些文件/文件夹

🔗参考：[Git如何屏蔽特定结构目录?](https://ruby-china.org/topics/node11)

- 内有前后/的含义明晰，建议熟记

`.gitignore`本身用于忽略某些文件，即写入的是被忽略，默认以被忽略为少数

如果被忽略的是多数，剩余的文件夹按照正则的方法纳入track，怎么做？

1. 先忽略所有文件
`/*`
2. 其次使用感叹号!声明不忽略（以.gitignore为例）
`!/.gitignore`
3. 其后再声明其他需要忽略的细节文件
`/**/*.png`

**原需求为**：对于nonebot的虚拟环境.venv中的site-packages里的包，我需要在插件的基础上开发其他功能/修复bug，而nonebot插件属于site-packages中的少数，如何只要nonebot开头的文件夹和.gitignore？

其次，我需要忽略图片、字体和RECORD文件，以及__pycache__文件夹，如何设计？

由于.gitignore中并没有完整的正则体系，但是勉强能用：*表示任意字符（0~n），?表示单个字符

### 最终可行的.gitignore

```bash
# ignore all files and directories
/*
# but except .gitignore and nonebot folders
!/.gitignore
!nonebot*/
# but none of pictures, fonts or RECORD files are allowed
/**/*.png
/**/*.jpg
/**/*.ttf
/**/RECORD
# or any __pycache__ folder
/**/__pycache__/
```


 💡 使用**`git status --ignored`** 查看哪些文件已经被忽略

## 如何将PC2已有仓库连接到Git Repo，并且同步到一个环境版本与PC2不同的本地仓库PC1？

🔗参考：[https://blog.51cto.com/u_9869701/3698451](https://blog.51cto.com/u_9869701/3698451)

环境：

- PC1、PC2均有本地仓库，但是有所差别
- PC1、PC2运行环境不同
- 已经将PC2的代码上传至Github，并且PC1可以拿到.gitignore

需求：

- 将Github的仓库同步到PC1、合并（尽量少的冲突）

### 步骤

**初始化**

1. [PC1] 找到对应位置，git init

**创建分支**

1. git add *
2. git commit -m “init: local repo”

必须要初始化、commit了本地才有master分支

**链接仓库**

1. git remote add origin [仓库url]
2. git branch --set-upstream-to=origin/master master

链接远程仓库，绑定拉取分支

**拉取，处理冲突**

1. git pull origin master --allow-unrelated-histories

git默认不允许unrelated histories，pull需要带上允许

这时候可以去vscode上查看冲突了

![](https://s2.loli.net/2023/09/01/coMFgiJG6U4ZTkL.png)

❓ 冲突解决后push，在PC2 pull时，是否会在PC2上产生冲突？
答：按需解决冲突后，PC2拉取没有产生冲突

🛑 注意：版本不同依旧会引起很大的问题
在当天因为Python环境不同折腾了很多相关包的版本，换了版本极端一点的情况是有一些是恰好互斥的，~~所以能润就最好别动~~

## 初次git commit后无法reset

如果希望撤销本次commit到untracked状态，那么可以使用

```bash
git reset --soft "HEAD^"
```

然而第一次commit时，是没有上一次commit的，也就没有HEAD^（其实就是HEAD~1，即）

## 解决每次git commit后LF变成CRLF的问题

### 问题描述

源于前端工程化，兼容别人的mac，统一调成了LF，但是每次git commit后变成CRLF。

在commit的时候，也会显示一大堆的警告：

> ***warning: LF will be replaced by CRLF***

### 解决方案

🔗参考：[How to Fix LF Will Be Replaced by CRLF Warning in Git](https://linuxhint.com/fix-lf-will-replaced-by-crlf-warning-in-gif/)
文章给读者复现了问题的过程，十分详细，并随后附上解决办法，解决思路和习惯值得点赞



查看当前是否自动CRLF：

```bash
git config core.autocrlf
```

Windows下默认这个是开的，即true，所以关掉即可：

```bash
git config --global core.autocrlf false
```

此后，commit pull全是TL

😱 注意：以后进入其他团队公司可能会遇到冲突的统一规定，建议主动询问

