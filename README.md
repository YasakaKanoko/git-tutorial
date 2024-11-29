# Git-tutorial

目录：

- 



## 配置

```shell
# 查看全局配置
git config --global -l
# 查看局部配置
git config --local -l

# 设置全局用户名/邮箱
git config --global user.name "username"
git config --global user.email "example@gmail.com"

# 查看已设置的全局用户名/邮箱
git config --global --get user.name
git config --global --get user.email

# 设置当前工作区用户名/邮箱
git config --local user.name "username"
git config --local user.email "example@gmail.com"

# 查看所有配置及其所在文件
git config --list --show-origin

# 删除配置
git config --unset --global user.name
git config --unset --global user.email

# 文件权限的变动也会视为改动, 可通过以下配置忽略文件权限变动
git config core.fileMode false

# 文件大小写设为敏感, git默认是忽略大小写
git config --global core.ignorecase false

# 配置 git pull 时默认拉取所有子模块内容
git config submodule.recurse true

# 记住提交账号密码, 下次操作可免账号密码
git config --global credential.helper store # 永久
git config --global credential.helper cache # 临时，默认15分钟
```

## 别名

```shell
# git st 等价于 git status
git config --global alias.st status

# 如果之前添加过，需要添加 --replace-all 进行覆盖
git config --global --replace-all alias.st status

# 删除 st 别名
git config --global --unset alias.st
```

## 初始化仓库

```shell
# 会在当前目录生成.git
git init

# 以安静模式创建，只会打印错误或警告信息
git init -q

# 在当前目录下创建一个裸仓库，里面只有 .git 下的所有文件
git init --bare
```

## 克隆

```shell
# https 协议克隆
git clone https://github.com/YasakaKanoko/git-tutorial.git

# SSH 协议克隆
git clone git@github.com:YasakaKanoko/git-tutorial.git

# 克隆指定分支， -b 指定分支名字，实际上是克隆所有分支并切换到 develop 分支上
git clone -b develop https://github.com/YasakaKanoko/git-tutorial.git

# --single-branch 完全只克隆指定分支
git clone -b develop --single-branch https://github.com/YasakaKanoko/git-tutorial.git

# 指定克隆后的文件夹名称
git clone https://github.com/YasakaKanoko/git-tutorial.git git-study # 如果后面是 . 在当前目录创建

# 递归克隆，如果项目包含子模块就非常有用
git clone --recursive https://github.com/YasakaKanoko/git-tutorial.git

# 浅克隆, 克隆深度为1, 只克隆指定分支且历史记录只保留最后一条, 通常用于减少克隆时间和项目大小
git clone --depth=1 https://github.com/YasakaKanoko/git-tutorial.git
# --no-single-branch 同时克隆其他所有分支
git clone --depth=1 --no-single-branch https://github.com/YasakaKanoko/git-tutorial.git 

# 裸克隆, 没有工作区内容，不能进行提交修改，一般用于复制仓库
git clone --bare https://github.com/xjh22222228/git-manual.git

# 镜像克隆, 也是裸克隆, 区别于包含上游版本库注册
git clone --mirror https://github.com/xjh22222228/git-manual.git
```

### 克隆指定文件夹

```shell
# 1. 创建目录并进入
cd ./example

# 2. 初始化仓库
git init

# 3. 设置仓库地址
git remote add origin https://github.com/YasakaKanoko/git-tutorial.git

# 4. 开启稀疏检出功能
git config core.sparsecheckout true

# 5. 配置要检出的文件
echo 'path/to/file' >> .git/info/sparse-checkout

# 6. 拉取内容
git pull origin main
```

## 管理仓库

```shell
# 查看远程仓库服务器, 一般打印 origin , 这是 Git 给你克隆的仓库服务器的默认名字
# 一般只会显示 origin , 除非你有多个远程仓库地址
git remote

# 指定-v, 查看当前远程仓库地址
git remote -v

# 添加远程仓库地址 example 是自定义名字
# 添加完后可以通过 git remote 就能看到 example
git remote add example https://github.com/YasakaKanoko/git-tutorial.git

# 查看指定远程仓库信息
git remote show example

# 重命名远程仓库
git remote rename oldName newName

# 移除远程仓库
git remote remove example

# 修改远程仓库地址，从HTTPS更改为SSH
git remote set-url origin git@github.com:YasakaKanoko/git-tutorial.git

# 后续的推送可以指定仓库名字
git push example
```

### 暂存

```shell
# 暂存所有
git add -A

# 暂存某个文件
git add ./README.md

# 暂存当前目录所有改动文件
git add .

# 暂存一系列文件
git add 1.txt 2.txt ...
```

## 提交

```shell
# -m 提交的描述信息
git commit -m "changes log"

# 只提交某个文件
git commit README.md -m "message"

# 提交并显示diff变化
git commit -v

# 允许提交空消息，通常必须指定 -m 参数
git commit --allow-empty-message

# 重写上一次提交信息，确保当前工作区没有改动
git commit --amend -m "新的提交信息"
```

**修改提交日期**：`git commit --date="月 日 时间 年 +0800" -m "init"`

```bash
git commit --date="Mar 7 21:05:20 2021 +0800" -m "init"
```

## 推送

```shell
# 等价于 git push origin, 实际上推送到一个叫 origin 默认仓库名字
git push

# 推送到主分支
git push -u origin main

# 本地分支推送到远程分支， 本地分支:远程分支
git push origin <branchName>:<branchName>

# 强制推送, --force 缩写
git push -f
```

## 查看分支

```shell
# 查看所有分支
git branch -a

# 查看本地分支
git branch

# 查看远端分支
git branch -r

# 查看本地分支所关联的远程分支
git branch -vv

# 查看本地 main 分支创建时间
git reflog show --date=iso main

# 搜索分支, 借助 grep 命令搜索, 包含关键字 dev
git branch -a | grep dev
```

## 切换分支

```shell
# 切换到main分支
git checkout main

# 切换上一个分支
git checkout -

# 强制切换, 但是要小心，如果文件未保存修改会直接覆盖掉
git checkout -f main

# -t, 切换远端分支, 如果用了 git remote 添加一个新仓库就需要用 -t 进行切换
git checkout -t upstream/main
```

