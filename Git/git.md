## 常用命令
```
# 状态查询
git status
git log

# 下载数据
git fetch xxxx

# 提交数据
git add .
git commit -m 'xxx'
git push

# 设置upstream
git branch -vv <branch-name> // 如果分支已配置了upstream，它将显示在输出的方括号中，如：* master 65bcbad [origin/master] update
git branch --set-upstream-to=<remote>/<branch> <local-branch>

# 配置远程仓库
git remote -v
git remote add xxxx https://xxxx.git
git remote remove xxxx
```
