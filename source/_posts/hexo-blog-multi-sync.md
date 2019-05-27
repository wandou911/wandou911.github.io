---
title: Hexo多设备同步
tags: [Hexo]
date: 2019-05-27 17:10:49
categories: "Hexo教程"
---

# 前言

在公司的 Mac 上使用 hexo 搭建了 GitHub 博客，然而我在自己的电脑上也想要同步 GitHub 博客到本地并发布更新，或者以后更换电脑了也希望最快的同步到最新的博客，不必重新搭建一遍。查询了一些网上的资料，现在记录一下，也给遇到同样问题的小伙伴们一个参考。

# 多设备同步

同步思路与 GitHub 推拉源码思路相同，使用 git 指令，保持本地的博客文件与 GitHub 上的博客文件相同即可，其步骤如下：

## 1 上传博客工程

部署博客到 GitHub 以后，我们可以在 GitHub 仓库的 master 分支上看到我们上传的博客文件。

「使用 hexo 搭建部署 GitHub 博客」步骤请移步另一篇博文查看更多。

但是这个博客文件是不包含 hexo 配置的，所以我们需要新建分支，使用 git 指令将带 hexo 配置的 GitHub 工程文件上传到新建的分支上。

（1）删除根目录和主题目录下面的隐藏 .git 文件夹

（2）在本地博客根目录下使用 git 指令上传项目到 GitHub

```
// git 初始化
git init
// 添加仓库地址
git remote add origin https://github.com/用户名/仓库名.git
// 新建分支并切换到新建的分支
git checkout -b 分支名
// 添加所有本地文件到 git
git add .
// git 提交
git commit -m ""
// 文件推送到 hexo 分支
git push origin hexo
```

## 2 其他设备上 clone 下 GitHub 上新建的分支的文件到本地

在另一台设备上使用 git 指令下载 GitHub 新建分支上的文件：

```
// 克隆文件到本地
git clone -b 分支名 https://github.com/用户名/仓库名.git
```

## 3 本地写文章

在 source -> _posts 文件夹下新建 md 文件，编辑并保存。

或是用命令创建文章

```
hexo new post "新建文章" #简写形式 hexo n "新建文章"
```
## 4 部署到 GitHub

```
// 安装 hexo
npm install -g hexo
// 注意这里不需要 hexo 初始化：hexo init；否则之前的 hexo 配置参数会重置
// 安装依赖库
npm install
// 安装部署相关配置
npm install hexo-deployer-git
```

## 5 同步项目源文件到 GitHub

```
// 添加源文件
git add .
// git 提交
git commit -m ""
// 先拉原来 GitHub 分支上的源文件到本地，进行合并
// 分支名后面的“--allow-unrelated-histories”是为了弹出“fatal: refusing to merge unrelated histories.”的错误
git pull origin 分支名 --allow-unrelated-histories
// 比较解决前后版本冲突后，push 源文件到 GitHub 的分支
git push origin 分支名
```

## 6 更新博客

```
$ hexo clean
$ hexo g
$ hexo d
```

至此多设备同步到此为止。多设备环境都搭建成功，以后的更新博文操作3、5、6步骤即可。

##### 参考链接1：[hexo 博客搭建——多设备同步 hexo 搭建的 GitHub 博客](https://lishide.github.io/2018/02/12/hexo-blog-multi-sync/)

##### 参考链接2: [Hexo实现多终端同步管理](https://github.com/dxxzst/dxxzst.github.io/blob/master/source/_posts/Hexo实现多终端同步管理.md)