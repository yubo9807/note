# git

- 版本库：用于记录 文件变动、提交人、提交时间、备注等
- 工作区：项目文件夹

> svn 中：版本库存放在服务器，版本库与工作区相分离
> git 中：单机版的 svn，pull 和 fecth 使 git 具有了分布式的特点

### 本地仓库操作：

```bash
git config --global user.name "belong-you"  # 用户名
git config --global user.email "1781926993@qq.com"  # 邮箱

git init  # 初始化文件
git init --bare project  # 创建一个裸库

git add test.js  # 添加文件
git add .  # 添加所有文件
git commit -m "注释"  # 添加注释

git reset --soft HEAD^  # 撤销注释
git reset --hard HEAD~  # 回退操作
git reset --hard HEAD@{1}  # 撤销回退
git reset --hard HEAD^  # 控制 merge 之后的回退方向

git reflog  # 本地操作记录

# 分支
git branch  # 查看所有分支
git branch demo1  # 创建分支
git checkout demo2  # 切换分支
git merge demo1 demo2  # 合并分支
git branch -m old_name new_name  # 修改分支名
git branch -d demo1  # 删除分支（前提：退出要删除的分支）
git reset --hard main  # 设置主分支为 main

# 制作补丁包 (windows 可以用 makecab，用法上有些区别)
git diff-tree -r --name-only --no-commit-id 465dabd | xargs zip ~/Desktop/patch.zip
```

### 线上仓库操作：

```bash
git clone <url>  # 克隆线上仓库
git clone -b <branch> <url>  # 克隆线上仓库
# 修改 ./git/config 文件 url：https://belong-you:password@github.com/belong-you/case
git push  # 提交
git pull  # 拉取代码  == git fetch + git merge
git fetch  # 拉取代码

git log  # 提交记录
git log --pretty=oneline  # 提交记录（精简版）
git reset --hard 版本号  # 回退操作

git push origin --delete <branch_name>  # 删除远程分支
```
