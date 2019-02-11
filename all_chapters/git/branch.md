# 分支管理
```
# 创建+切换dev分支
$ git checkout -b dev

# 相当于
$ git branch dev # 创建分支
$ git checkout dev

# 查看当前分支，当前分支前面标有×号
$ git branch

# 切换回master分支
$ git checkout master

# 合并指定分支到当前分支
$ git merge dev

# 删除dev分支
$ git branch -d dev

# 查看分支合并情况
$ git log --graph --pretty=oneline --abbrev-commit
*   59bc1cb conflict fixed
|\
| * 75a857c AND simple
* | 400b400 & simple
|/
* fec145a branch test

# 删除feature1分支
$ git branch -d feature1

# 创建并切换dev分支
$ git checkout -b dev

# 修改readme.txt文件，并提交一个新的commit
$ git add readme.txt
$ git commit -m "add merge"

# 切换回master
$ git checkout master

# 合并dev分支，请注意--no-ff参数，表示禁用Fast forward
$ git merge --no-ff -m "merge with no-ff" dev

# 看看分支历史
$ git log --graph --pretty=oneline --abbrev-commit
*   7825a50 merge with no-ff
|\
| * 6224937 add merge
|/
*   59bc1cb conflict fixed

# 如果需要临时修复Bug，可以把当前工作现场“储藏”起来，等Bug修复后恢复现场后继续工作
$ git stash

# 此时查看工作区是干净
# 切换到需要修复Bug的分支，创建临时分支来修复
$ git checkout master
$ git checkout -b issue-101

# 修复完成后切换到master分支，完成合并，删除临时分支
$ git checkout master
$ git merge --no-ff -m "merged bug fix 101" issue-101
$ git branch -d issue-101

# Bug修复后，切换回dev分支继续干活
$ git checkout dev

# 查看工作现场列表
$ git stash list

# 恢复工作现场
$ git stash pop # 恢复的同时把stash内容也删了
$ git stash apply # 恢复，不删除stash的内容，使用git stash drop

# 再次查看工作现场列表，干净
$ git stash list

# 可以多次stash，恢复时指定恢复
$ git stash apply stash@{0}

# 强行删除一个没有合并过的分支
$ git branch -D <name>

# 要查看远程库的信息
$ git remote
$ git remote -v

# 推送其他分支
$ git push origin dev

# 从远程库clone，默认情况只能看到master分支，需要在dev分支，必须创建远程origin的dev分支到本地
$ git checkout -b dev origin/dev
$ git checkout -b branch-name origin/branch-name
$ git branch --set-upstream branch-name origin/branch-name # 关联

# 向远程库推送dev有冲突
$ git pull # 抓取到本地合并解决冲突，再向远程推送
$ git push origin dev
```