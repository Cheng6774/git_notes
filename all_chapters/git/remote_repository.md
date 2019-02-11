# 远程仓库
```
$ ssh-keygen -t rsa -C "youremail@example.com"
# 测试是否成功
$ ssh -T git@github.com

# 把一个已有的本地仓库与之关联
$ git remote add origin git@github.com:Windrivder/Windrivder.git

# 把本地库的所有内容推送到远程库上（推送master分支的内容）
$ git push -u origin master

# 向远程库推送更新
$ git push origin master

# 从远程库克隆
$ git clone git@github.com:michaelliao/gitskills.git
```
