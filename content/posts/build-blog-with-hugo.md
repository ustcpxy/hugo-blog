---
title: "基于hugo搭建个人博客"
date: 2018-04-23T12:23:00+08:00
lastmod: 2018-12-20T14:56:55+08:00
tags: ["hugo", "blog"]
categories: ["指南"]
draft: false
toc: true
---

本文记录了本博客站点的建立过程。


## Quick Start {#quick-start}

在本地快速建立一个 `hugo` 博客框架。

```sh
sudo apt install hugo
cd ~
hugo new site blog-hugo
cd blog-hugo
git init
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
echo 'theme = "ananke"' >> config.toml
git add .
git commit

```

稍后将该项目提交到 `github` 管理。

参考官网：[Quick Start](https://gohugo.io/getting-started/quick-start/)


## Host on GitHub {#host-on-github}

将博客内容部署到 [Github Pages](https://pages.github.com/) 。首先要创建一个项目：ustcpxy.github.io

```sh
# 将 ustcpxy.github.io 作为子模块添加到 blog 项目
cd ~/blog-hugo
git submodule add -b master git@github.com:ustcpxy/ustcpxy.github.io.git public

# public 目录是生成的博客站点内容，执行 hugo 命令即可生成

```

这些步骤是机械化的，可以使用脚本实现一键部署。
在 blog-hugo 项目中创建 `deploy.sh` 文件并赋予可执行权限。
执行命令 `./deploy.sh` 即可将博客内容发布到 github pages。

```sh
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project.
hugo # if using a theme, replace with `hugo -t <YOURTHEME>`

# Go To Public folder
cd public
# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back up to the Project Root
cd ..
```

参考官网：<https://gohugo.io/hosting-and-deployment/hosting-on-github/>


## HowTo Post {#howto-post}

使用 Emacs Orgmode + **ox-hugo**

下一篇将介绍具体用法。
