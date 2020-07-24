---
title: Windows 下添加 tree 到 Git Bash 中
tags:
  - Windows
  - Git Bash
  - tree
author: Shane
img: 'https://myimagebed-1302088591.cos.ap-nanjing.myqcloud.com/%E6%96%87%E7%AB%A0%E7%89%B9%E5%BE%81%E5%9B%BE/wallhaven-0wjr6q.jpg'
toc: true
summary: >-
  解决在 Git Bash 里面输入命令 tree，出现 bash: /usr/bin/tree: No such file or directory
  提示的问题
comments: true
categories:
  - 前端
abbrlink: 9f75cef
date: 2020-05-10 14:35:46
updated: 2020-05-16 11:15:20
---


## Windows 下添加 tree 到 Git Bash 中

### 背景

**操作系统：**`Windows 10 专业版 1909 (18363.778)`

**Git 版本：**`2.26.1.windows.1`

在 Git Bash 里面输入命令 `tree`，出现提示：`bash: /usr/bin/tree: No such file or directory`， 截图如下：

<!--{% asset_img image-20200510111719970.png 提示信息截图 %}-->
![提示信息截图](https://myimagebed-1302088591.cos.ap-nanjing.myqcloud.com/2020-05-10-Windows-%E4%B8%8B%E6%B7%BB%E5%8A%A0-tree-%E5%88%B0-Git-Bash-%E4%B8%AD/image-20200510111719970.png)

### 排查

提示信息告诉我们，没有 `/usr/bin/tree` 这样的文件或目录。

那么 `/usr/bin` 目录在哪呢？

Windows 上 Git Bash 中默认的 `/usr/bin` 目录位于 `C:\Program Files\Git` 目录下。

打开文件资源管理器，进入该目录后查找 `tree`，确实没找到，截图如下：

<!--{% asset_img image-20200510121001838.png bin 目录 %}-->
![目录](https://myimagebed-1302088591.cos.ap-nanjing.myqcloud.com/2020-05-10-Windows-%E4%B8%8B%E6%B7%BB%E5%8A%A0-tree-%E5%88%B0-Git-Bash-%E4%B8%AD/image-20200510121001838.png)

### 解决

所以我们需要下载 `tree`，然后把它添加到 `/usr/bin` 下。

[官网下载 tree](http://gnuwin32.sourceforge.net/packages/tree.htm) 请下载 `Binaries` 版本

<!--{% asset_img image-20200510122041437.png 官网截图 %}-->
![官网截图](https://myimagebed-1302088591.cos.ap-nanjing.myqcloud.com/2020-05-10-Windows-%E4%B8%8B%E6%B7%BB%E5%8A%A0-tree-%E5%88%B0-Git-Bash-%E4%B8%AD/image-20200510122041437.png)


但是可能会遇到网站打不开的情况，这里提供百度云网盘下载方式：

[网盘下载 tree](https://pan.baidu.com/s/1jI-lIh9yqPqrXWoE6sfiew ) 提取码：bp3u 

将下载下来的 `tree-1.5.2.2-bin.zip` 解压后，只需把里面 `bin` 目录下的 `tree.exe` 文件复制粘贴到 Git 默认的安装目录 `C:\Program Files\Git` 下的 `usr\bin` 目录下，如下图所示：

<!--{% asset_img image-20200510124629332.png 粘贴后的目录 %}-->
![粘贴后的目录](https://myimagebed-1302088591.cos.ap-nanjing.myqcloud.com/2020-05-10-Windows-%E4%B8%8B%E6%B7%BB%E5%8A%A0-tree-%E5%88%B0-Git-Bash-%E4%B8%AD/image-20200510124629332.png)

好了，下面我们再用命令 `tree` 试试呢？

<!--{% asset_img image-20200510130854153.png tree 命令成功执行 %}-->
![命令成功执行](https://myimagebed-1302088591.cos.ap-nanjing.myqcloud.com/2020-05-10-Windows-%E4%B8%8B%E6%B7%BB%E5%8A%A0-tree-%E5%88%B0-Git-Bash-%E4%B8%AD/image-20200510130854153.png)

成功啦！