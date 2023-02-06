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
git branch <branch_name>  # 创建分支
git checkout <branch_name>  # 切换分支
git merge <branch_name1> <branch_name2>  # 合并分支
git branch -m <old_name> <new_name>  # 修改分支名
git branch -d <branch_name>  # 删除分支（前提：退出要删除的分支）
git reset --hard <branch_name>  # 设置主分支

# 制作补丁包 (windows 可以用 makecab，用法上有些区别)
git diff -r --name-only --no-commit-id | xargs zip ~/Desktop/patch.zip

git mv --force Test.js test.js  # 改变文件名而不修改内容

git rm test.js  # 删除文件
git rm --cached test.js  # 删除文件，但本地保留该文件

# 贮藏
git stash  # 暂存所有改动
git stash push test.js  # 暂存指定文件
git stash -u test.js  # 排除指定文件，暂存其他文件
git stash save <name>  # 本地暂存名字
git stash push -m <name>  # 暂存到指定的暂存区
git stash list  # 查看暂存记录

# 标签
git tag <tag_name> -a ''  # 创建标签
git tag  # 查看本地所有标签
git show <tag_name>  # 查看标签
git tag -d <tag_name>  # 删除标签
git tag origin <tag_name>  # 推送到远程仓库

# 操作记录
git reflog  # 查看本地操作记录

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
