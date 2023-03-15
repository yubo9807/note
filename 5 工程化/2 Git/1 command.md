# git

- 版本库：用于记录 文件变动、提交人、提交时间、备注等
- 工作区：项目文件夹

> svn 中：版本库存放在服务器，版本库与工作区相分离
> git 中：单机版的 svn，pull 和 fecth 使 git 具有了分布式的特点

## 本地仓库操作：

```bash
git config --global user.name "username"              # 设置用户名
git config --global user.email "useremail@email.com"  # 设置邮箱

git init                 # 初始化文件
git init --bare project  # 初始化一个裸库（服务器上存的就是这样一个版本库）
```

### add / commit

```bash
git add <filename>  # 添加指定文件
git add .           # 添加所有文件

git commit -m "注释"  # 添加注释
```

### branch

```bash
git branch                               # 查看所有分支
git branch <branch_name>                 # 创建分支
git checkout <branch_name>               # 切换分支
git merge <branch_name1> <branch_name2>  # 合并分支
git branch -m <old_name> <new_name>      # 修改分支名
git branch -d <branch_name>              # 删除分支（前提：退出要删除的分支）
git reset --hard <branch_name>           # 设置主分支
```

### reset

```bash
git reset --soft HEAD^     # 撤销注释
git reset --hard HEAD~     # 回退操作
git reset --hard HEAD@{1}  # 撤销回退
git reset --hard HEAD^     # 控制 merge 之后的回退方向

git reflog  # 本地操作记录
```

### 制作补丁包

```bash
# 基于当前工作区代码与某一次 commit
git diff <commit_id> -r --name-only --no-commit-id | xargs zip ~/Desktop/patch.zip
```

> windows 可以用 makecab，用法上有些区别

### stash

```bash
git stash                  # 暂存所有改动
git stash push test.js     # 暂存指定文件
git stash -u test.js       # 排除指定文件，暂存其他文件
git stash save <name>      # 本地暂存名字
git stash push -m <name>   # 暂存到指定的暂存区
git stash list             # 查看暂存记录
git stash apply stash@{0}  # 恢复指定贮藏
git stash pop              # 恢复最近的一次贮藏，对应的 list 中贮藏将删除
git stash drop stash@{1}   # 删除指定贮藏
```

### tag

```bash
git tag <tag_name> -a ''   # 创建标签
git tag                    # 查看本地所有标签
git show <tag_name>        # 查看标签
git tag -d <tag_name>      # 删除标签
git tag origin <tag_name>  # 推送到远程仓库
```

### mv / rm

```bash
git mv --force Test.js test.js  # 改变文件名而不修改内容

git rm test.js           # 删除文件
git rm --cached test.js  # 删除文件，但本地保留该文件
```

## 线上仓库操作：

```bash
git clone <url>  # 克隆线上仓库
git clone -b <branch> <url>  # 克隆线上仓库
# 修改 ./git/config 文件 url：https://username:password@github.com/user/repositories

git push   # 提交
git pull   # 拉取代码  == git fetch + git merge
git fetch  # 拉取代码

git log  # 提交记录
git log --pretty=oneline    # 提交记录（精简版）
git reset --hard <version>  # 回退操作

git push origin --delete <branch_name>  # 删除远程分支
```
