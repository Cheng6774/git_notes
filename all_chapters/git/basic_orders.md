# 基本命令
```

# 安装Git
$ sudo apt install git

# 打开文件
$ cat text.txt

# 配置个人信息
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
    "system"表示系统使用的配置
    "global"表示所有版本库使用的配置
    "local"表示当前版本库使用的配置
    它们的优先等级从上到下依次提高

# 切换目录初始化
$ git init

# 文件添加到仓库
$ git add -p <file>

# 将工作区所有修改添加到暂存区
$ git add .

# 把文件提交到版本库
$ git commit -m "add LICENSE" 

# 查看仓库当前状态
$ git status

# 查看difference
$ git diff

# 显示从最近到最远的提交日志
$ git log --pretty=oneline # 格式化输出信息

# 版本退回
$ git reset --hard HEAD^ # 当前版本HEAD,上一个版本HEAD^,上上个版本HEAD^^
$ git reset --hard 130f10a # 或HEAD~100，前第100个版本

# 查看命令记录
$ git reflog

# 丢弃工作区的修改，回到最近一次git commit或git add时的状态：
$ git checkout -- text.txt

# 将之前添加到暂存区(stage, index)的内容从暂存区移除到工作区(unstage)
$ git reset HEAD text.txt

# 从版本库中删除该文件
$ git rm text.txt
$ git commit -m "remove READER.md"

# 把误删的文件恢复到最新版本，checkout其实用版本库里的版本替换工作区的版本,丢弃掉相对于暂存区中最后一个添加的文件内容所做的变更
$ git checkout -- text.txt

```
