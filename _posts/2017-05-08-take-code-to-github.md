---
layout: post
title: 把项目发布到Github上
bigimg: /img/path.jpg
---

> * 绑定SSH，生成的SSH key 放到github->setting中
> * win ：c/Documents and Settings/username/.ssh
> * Linux/Mac :~/.ssh
> * 下id_rsa.pub中
> * 测试：ssh -T git@github.com 
> * 在Git中cd到项目下
> * 初始化仓库 git init
> * 提交所有文件到缓存 git add .
> * 提交到仓库 git commit -m 'first commit'
> * 克隆远程仓库 git clone [仓库地址]
> * 关联远程仓库 git remote add origin [仓库地址]
> * 查看关联仓库 git remote -v
> * 提交到远程仓库 git push origin master
> * 提交指定分支
> * 新建分支 git branch develop
> * 切换分支 git checkout develop
> * 上两步等价于 git checkout -b develop
> * 分支提交到远程 git push origin develop