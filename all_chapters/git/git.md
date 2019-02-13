# git_notes

学习 git 相关材料和笔记

[git教程](https://backlog.com/git-tutorial/cn/)

# 基本命令
```
# 打开git GUI界面
$ gitk

# 查找 git 命令对用操作可用 -h
# 对 config 命令查询帮助
$ git confi -h

# 安装 Git
$ sudo apt install git

# 打开文件
$ cat text.txt

# 配置个人信息
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
    "system"表示系统使用的配置
    "global"表示用户级别使用的配置
    "local"表示当前仓本库使用的配置
    它们的优先等级从上到下依次提高

# 查看配置信息
$ git config --list

# 删除某项配置信息
$ git config --unset user.name

# add 和 commit 同时操作，只针对修改的文件（创建文件不适用）
$ git commit -am 'commit-message'

# 切换目录初始化
$ git init

# 文件添加到仓库
$ git add -p <file>

# 将工作区所有修改添加到暂存区
$ git add .

# 把文件提交到版本库
$ git commit -m "first commit"

# 修改上次提交的信息
git commit --amend "first commit"

# 修改提交作者
$ git commit --amend --reset-author

# 查看仓库当前状态
$ git status

# 查看 difference
$ git diff

# 显示从最近到最远的提交日志
$ git log --graph --pretty=oneline --abbrev-commit
$ git log --graph           # 表示图形化显示
$ git log --pretty=oneline  # 表示每次提交单行显示
$ git log --abbrev-commit   # 表示简化显示 commit id

# 查看命令记录
$ git reflog

# 查看修改提交人和提交时间
$ git blame text.txt

# 退回前面提交过的版本
$ git reset --hard HEAD^      # 当前版本 HEAD, 上一个版本 HEAD^, 上上个版本 HEAD^^
$ git reset --hard 130f10a    # 根据 commit id 向前或向后切换提交的版本
$ git reset --hard HEAD~100   # 前第 100 个版本

# 将之前添加到暂存区 (stage, index) 的内容从暂存区移除到工作区 (unstage)
$ git reset HEAD text.txt

# 丢弃工作区的某个文件修改，回到最近一次 git commit 或 git add 时的状态：
$ git checkout -- text.txt

# 删除文件
$ git rm text.txt      （该步骤包括在工作区的删除并提交到暂存区)
  如果使用了 git rm 命令，需要先进行 git reset HEAD 再进行 git checkout
$ rm text.txt          （系统命令，该步骤只是在工作区进行删除)
```

# diff
原始文件用 - 表示，目标文件用 + 表示  
```
# 简单查看比较，前者原始文件，后者为目标文件
$ diff <file1-name> <file2-name>

# 逐行查看比较
$ diff -u <file1-name> <file2-name>

# 比较暂存区和工作区的差别，暂存区为原始文件，工作区为目标文件
$ git diff

# 比较最新提交版本和工作区的差别，提交版本为原始文件，工作区为目标文件
$ git diff HEAD
$ git diff 54djf  # 换成 commit id 表示某次提交与工作区的差别

# 比较最新提交版本与暂存区的差别，提交版本为原始文件，暂存区为目标文件
$ git diff --cached

```

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

# 标签管理
标签有两种：轻量级标签 (lightweight) 与带有附注的标签 (annotated)  
tag 不随分支的切换而改变  
```

# 创建一个轻量级标签
$ git tag v1.0

# 创建带有附注的标签
$ git tag -a v0.1 -m "version 0.1 released"

# 查看所有标签
$ git tag

# 查找标签
$ git tag -l 'v1.0'  # 查找 v1.0 标签
$ git tag -l 'v*'    # 查找 v 开头的标签（支持正则表达式）

# 给历史提交的 commit id 打标签
$ git log --pretty=oneline --abbrev-commit # 查看 commit id
$ git tag v0.9 6224937

# 删除标签
$ git tag -d v1.0 # 删除本地标签

# 查看标签信息
$ git show v0.9

# 用 PGP 签名标签
$ git tag -s <tagname> -m "blablabla..."

# 推送某个标签到远程
$ git push origin v1.0

# 一次性推送全部尚未推送到远程的本地标签
$ git push origin --tags

# 删除远程标签
$ git tag -d v0.9 # 删除本地
$ git push origin :refs/tags/v0.9 # 删除远程
```

# 远程仓库
push 推送  
pull 拉取会执行合并 merge pull == fetch+merge  
远程协作如遇同时修改一个文件，需要先进行pull操作，并在本地手动合并修改文件的冲突，然后才能执行push操作  

```
$ ssh-keygen -t rsa -C "youremail@example.com"
# 测试是否成功
$ ssh -T git@github.com

# 把一个已有的本地仓库与之关联
$ git remote add origin git@github.com:Windrivder/Windrivder.git

# 把本地库的所有内容推送到远程库上（推送 master 分支的内容）
$ git push -u origin master

# 向远程库推送更新
$ git push origin master

# 从远程库克隆
$ git clone git@github.com:michaelliao/gitskills.git

# 查看远程库的名称
$ git remote

# 查看远程 pull 和 push 对象库
$ git remote -v

# 查看远程库详细信息
$ git remote shwo origin  # origin 为远程库名称

# 推送其他分支
$ git push origin dev

# 从远程库 clone，默认情况只能看到 master 分支，需要在 dev 分支，必须创建远程 origin 的 dev 分支到本地
$ git checkout -b dev origin/dev
$ git checkout -b branch-name origin/branch-name
$ git branch --set-upstream branch-name origin/branch-name # 关联

# 向远程库推送 dev 有冲突
$ git pull # 抓取到本地合并解决冲突，再向远程推送
$ git push origin dev
```

# .gitignore
.gitignore 文件包含要忽略的文件名，这些文件将不纳入版本管理中  
.gitignore 中的输入支持正则表达式  
```
# 创建.gitignore文件
$ vi .gitignore

# 查看。gitignore 文件
$ cat .gitignore
```
# 自定义 Git
```
# 显示颜色，会让命令输出看起来更醒目
$ git config --global color.ui true

# 忽略某些文件时，需要编写。gitignore，然后将。gitignore 放到版本库中
# st 就表示 status
$ git config --global alias.st status

# 配置一个 unstage 别名
$ git config --global alias.unstage 'reset HEAD'
$ git unstage test.py # 等价于
$ git reset HEAD test.py

# 显示最后一次提交信息
$ git config --global alias.last 'log -1'

# log
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
# 每个仓库的配置文件放在。git/config
# 当前用户的配置文件放在用户主目录下的一个隐藏文件。gitconfig 中
```

搭建 Git 服务器
```
1. 安装 git：

$ sudo apt-get install git
2. 创建一个 git 用户，用来运行 git 服务：

$ sudo adduser git
3. 创建证书登录：收集所有需要登录的用户的公钥，就是他们自己的 id_rsa.pub 文件，把所有公钥导入到 /home/git/.ssh/authorized_keys 文件里，一行一个

4. 初始化 Git 仓库：

# 选定一个目录作为 Git 仓库，假定是 /srv/sample.git，在 /srv 目录下输入命令

$ sudo git init --bare sample.git
# 把 owner 改为 git
$ sudo chown -R git:git sample.git
5. 禁用 shell 登录：

# 编辑 /etc/passwd 文件
git:x:1001:1001:,,,:/home/git:/bin/bash # 修改成下面的内容
git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell
6. 克隆远程仓库，在各自的电脑上运行：

$ git clone git@server:/srv/sample.git
```