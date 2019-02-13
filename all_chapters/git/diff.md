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