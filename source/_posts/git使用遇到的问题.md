---
title: git使用遇到的问题
date: 2017-12-09 19:34:07
tags: [git]
categories: [coding]
---
###git使用和群晖git server搭建遇到的问题
记录一下在使用群晖搭建git server在使用时遇到的一些问题：
#### 1. 群晖git server搭建时的问题
群晖搭建git server是非常容易的具体网上随便搜方法：
想要使用git server就要打开群晖的家目录(控制面板->用户账号->高级设置)。但是一旦打开家目录就会使每个用户都可以访问其他用户的存储信息，只能分别设置不同文件夹的权限将非本账号的home文件都设置为拒绝读取和写入。但是从群晖的DSM说明中可以看到原来是有一个用户主目录选项可以达到权限控制的效果,不懂为什么要去掉。
![用户主目录](/assets/img/用户主目录.jpg)
#### 2. git使用中的问题
- 远程存储库的地址输入写错
```
fatal: 'origin' does not appear to be a git repository
fatal: The remote end hung up unexpectedly
```
对比正确的格式`git remote add [origin或别的名字] ssh://[Git 用户]@[您的 Synology 服务器 IP 地址或主机名]/[Git 存储库路径]`  **不要忘记`ssh://`**
- git server 建远程仓库
用`git init --bare`建远程仓库，
用`git init`建本地库。(目前还没弄明白，反正就这样用吧)

建仓库时用 git_repos/你要的名字.git
而不是 git_repos/你要的名字/.git
- git push 卡在write object
`git config --global sendpack.sideband false`
- git broken pipe
`git config http.postBuffer 209715200`
