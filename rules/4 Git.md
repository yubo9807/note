## commit
1. commit 参考大厂标准，每次 commit 要写尽可能的写详细；
2. push 命令要写完整：`git push origin dev`，防止提交到错误分支上；

```git
docs     文档修改
add      增加依赖
delete   删除代码/文件
feat     增加新功能
fix      修改代码/bug
style    代码修改，但未影响逻辑（不是指样式的修改）
merge    合并代码
perfect  功能完善
refactor 代码重构
ci       持续继承
test     测试代码
release  发布
deploy   部署
chore    更改配置文件
revert   版本回退
```

## 自动部署
1. 项目打包目录统一使用 dist ；
2. 打包脚本统一使用 `npm run build` ，（需部署特殊环境跟运维同事沟通）；
3. 项目稳定后向 master 分支合并，无需手动部署（需运维配置脚本。合并间隔至少 **5 分钟** 以上，不要过于频繁）；
4. readme.md 中注明 node 版本；

```git
// 切换分支
git checkout master

// 合并分支
git merge dev

// 提交
git push origin master
```

