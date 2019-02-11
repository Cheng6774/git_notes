# 自定义 Git
```
# 显示颜色，会让命令输出看起来更醒目
$ git config --global color.ui true

# 忽略某些文件时，需要编写.gitignore，然后将.gitignore放到版本库中
# st就表示status
$ git config --global alias.st status

# 配置一个unstage别名
$ git config --global alias.unstage 'reset HEAD'
$ git unstage test.py # 等价于
$ git reset HEAD test.py

# 显示最后一次提交信息
$ git config --global alias.last 'log -1'

# log
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
# 每个仓库的配置文件放在.git/config
# 当前用户的配置文件放在用户主目录下的一个隐藏文件.gitconfig中
```

# 搭建 Git 服务器
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

# 编辑/etc/passwd文件
git:x:1001:1001:,,,:/home/git:/bin/bash # 修改成下面的内容
git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell
6. 克隆远程仓库，在各自的电脑上运行：

$ git clone git@server:/srv/sample.git
