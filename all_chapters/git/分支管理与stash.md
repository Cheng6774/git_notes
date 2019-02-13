# 分支管理与 stash
HEAD 指向的是分支当前所处版本状态，master（分支名）指向当前所处分支  
分支的最佳实践，通常来说分支有如下几种：  
master 分支：最稳定的分支，生产系统分支，变化最少  
test 分支：用于测试人员测试  
develop 分支：变化最频繁，用于开发  
hotfix 分支：线上系统出问题用于紧急修复的分支  

git合并原则：三方合并原则  
只有一个提交人的提交是线性提交  
当有两个人进行提交，则从原始提交点开始进行分叉出两个新的提交点，合并时将这两个提交点进行合并，则比原始提交点前进了两次提交  

合并 dev分支到master分支时，如果master分支的状态没有被更改过，那么这个合并是非常简单的。 dev分支的历史记录包含master分支所有的历史记录，所以通过把master分支的位置移动到dev的最新分支上，Git 就会合并。这样的合并被称为fast-forward（快进）合并。  

```
# 创建并切换 dev 分支
$ git checkout -b dev

# 相当于 branch＋checkout
$ git branch dev      # 创建分支
$ git checkout dev    # 切换分支

# 查看所有分支，当前分支前面标有×号
$ git branch

# 切换到 master 分支
$ git checkout master

# 合并指定分支到当前分支
$ git merge dev

# 删除 dev 分支
$ git branch -d dev

# 强行删除一个没有合并过的分支
$ git branch -D dev

# 合并 dev 分支，请注意 --no-ff 参数，表示禁用 Fast forward
$ git merge --no-ff -m "merge with no-ff" dev
禁用 Fast forward 合并会比 dev 分支多一次历史提交，即合并也是一次提交

# 利用 commit id 切换到某次历史提交版本
$ git checkout 67e5d
此时 HEAD 指向一个游离状态的分支，在当前版本进行修改后，通过 add 和 commit 操作进行提交可以创建一个游离的历史提交点，再通过
$ git branch <new-branch-name> <commit-id>
可以通过创建一个分支将这个游离的历史提交点工作内容保存下来

# 分支改名
$ git branch -m 《原分支名》 《现分支名》

# 如果需要临时切换到其他分支，可以把当前工作现场先保留
$ git stash

# 查看工作现场列表
$ git stash list

# 保存工作现场时加注释
$ git stash save 'message'

# 恢复工作现场
$ git stash pop   # 恢复的同时把 stash 内容也删了
$ git stash apply # 恢复，不删除 stash 的内容，

# 手动删除 stash 现场（后面的数字时编号）
$ git stash drop@{0}

# 可以多次 stash，恢复时指定恢复某个 stash
$ git stash apply stash@{0}

```