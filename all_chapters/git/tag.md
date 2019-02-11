# 标签管理
```
# 切换到需要打标签的分支
$ git branch
$ git checkout master

# 创建标签
$ git tag v1.0

# 查看所有标签
$ git tag

# 给历史提高的commit id打标签
$ git log --pretty=oneline --abbrev-commit # 查看commit id
$ git tag v0.9 6224937

# 查看标签信息
$ git show v0.9

# 创建带有说明的标签
$ git tag -a v0.1 -m "version 0.1 released" 3628164

# 用PGP签名标签
$ git tag -s <tagname> -m "blablabla..."

# 推送某个标签到远程
$ git push origin v1.0

# 一次性推送全部尚未推送到远程的本地标签
$ git push origin --tags

# 删除远程标签
$ git tag -d v0.9 # 删除本地
$ git push origin :refs/tags/v0.9 # 删除远程
```
