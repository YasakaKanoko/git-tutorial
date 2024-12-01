# Git-tutorial

目录：

- [安装](#安装)
- [配置](#配置)
- [别名](#别名)
- [初始化仓库](#初始化仓库)
- [暂存区](#暂存区)
- [commit](#提交)
- [log](#log)
- [文件操作](#文件操作)
- [还原](#还原)
- [删除](#删除)
- [移动/重命名文件](#移动重命名文件)
- [分支](#分支)
- [查看分支](#查看分支)
- [切换分支](#切换分支)
- [创建分支](#创建分支)
- [删除分支](#删除分支)
- [重命名分支](#重命名分支)
- [合并分支](#合并分支)
- [变基](#变基)
- [远程](#远程)
- [推送](#推送)
- [克隆](#克隆)
- [管理仓库](#管理仓库)
- [tag](#tag)
- [SSH_Key](#sshkey)
- [gitignore](#gitignore)
- [gh-pages](#gh-pages)

## 安装

```shell
# 查看版本号
git -v
```

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
# git status: 查看仓库的状态
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

## 暂存区

```shell
# 暂存所有
git add -A

# 暂存某个文件
git add ./README.md

# 暂存所有未跟踪的文件
git add *

# 暂存当前目录所有改动文件
git add .

# 暂存一系列文件
git add 1.txt 2.txt ...
```

## 提交

```shell
# -m 提交的描述信息
git commit -m "xxxx"

# -a 提交所有已修改的文件(未跟踪的文件不会提交)
git commit -a -m "xxxx"

# 只提交某个文件
git commit README.md -m "xxxx"

# 提交并显示diff变化
git commit -v

# 允许提交空消息，通常必须指定 -m 参数
git commit --allow-empty-message

# 重写上一次提交信息，确保当前工作区没有改动
git commit --amend -m "xxxx"
```

**修改提交日期**：`git commit --date="月 日 时间 年 +0800" -m "init"`

```bash
git commit --date="Mar 7 21:05:20 2021 +0800" -m "init"
```

### log

```shell
# 查看文件提交记录
git log
```

## 文件操作

### 还原

```shell
# 重置到最后一次提交时的状态
git restore ./1.txt

# 重置所有文件到最后一次提交时状态
git restore *

# 将文件从暂存状态取消
git restore --staged ./1.txt
```

### 删除

```shell
# 删除文件, 有改动时不删
git rm ./file.txt

# 强制删除
git rm ./file.txt -f

# 删除所有文件, 但不删除.git目录
git rm -rf .

# 清除工作区缓存, 但不删除文件
git rm -r --cached
```

### 移动/重命名文件

```shell
# git mv from源文件 to重命名文件
git mv ./1.txt ./2.txt
```

## 分支

git 存储文件时，每次代码提交会产生与之对应的节点，git 通过节点记录代码状态，构成一个**树状结构**

Master/Main ：分支主干

```shell
# 查看当前分支
git branch 

# 创建新分支
git branch <branch_name>

# 删除分支
git branch -d <branch_name>

# 切换分支
git switch <branch_name>

# 创建分支并切换
git switch -c <branch_name>

# 合并分支
git merge <branch_name>
git branch -d <branch_name> # 合并后必须删除
```

分支冲突

1. 切回 `main` 分支，然后合并分支 `git merge`，产生冲突
2. 源文件中处理分支， `git commit`
3. `git branch -d` 删除副分支

### 查看分支

```shell
# 查看当前分支
git branch

# 查看所有分支
git branch -a

# 查看远端分支
git branch -r

# 查看本地分支所关联的远程分支
git branch -vv

# 查看本地 main 分支创建时间
git reflog show --date=iso main

# 搜索分支, 借助 grep 命令搜索, 包含关键字 dev
git branch -a | grep dev
```

分支备注

```shell
# 命令
git config branch.{branch_name}.description 备注内容

# 给 hotfix/tip 分支添加备注信息
git config branch.hotfix/tip.description 修复细节
```

### 切换分支

- `git checkout`

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

- `git switch`

  ```shell
  # 切换到 develop 分支
  git switch develop
  
  # 切换到上一个分支
  git switch -
  
  # 强制切换到 develop 分支，并抛弃本地所有修改
  git switch -f develop
  
  # 创建分支并切换
  git switch -c newBranch
  
  # 强制创建分支
  git switch -C newBranch
  
  # 从前3次提交进行创建新的分支
  git switch -c newBranch HEAD〜3
  
  # -t, 切换远端分支, 如果用了 git remote 添加一个新仓库就需要用 -t 进行切换
  git switch -t upstream/main
  ```

### 创建分支

```shell
# 创建一个名为 develop 本地分支
git branch develop

# 强制创建分支, 不输出任何警告或信息
git branch -f develop

# 创建本地 develop 分支并切换
git checkout -b develop

# 创建远程分支, 实际上创建本地分支然后推送到远端
git checkout -b develop
git push origin develop

# 创建一个空的分支, 不继承父分支，历史记录是空的，一般至少需要执行4步
git checkout --orphan develop
git rm -rf .  # 这一步可选，如果你真的想创建一个没有任何文件的分支
git add -A && git commit -m "提交" # 添加并提交，否则分支是隐藏的 （执行这一步之前需要注意当前工作区必须保留一个文件，否则无法提交）
git push --set-upstream origin develop # 推送到远程
```

### 删除分支

删除分支不能删除当前分支，先切换到其他分支再删除

```shell
# 删除本地分支
git branch -d <branchName>

# 大写 D 强制删除未完全合并的分支
# 等价 git branch --delete --force <branchName>
git branch -D <branchName>

# 删除远程分支
git push origin :<branchName>
git push origin --delete <branch-name>  # >= 1.7.0
```

### 重命名分支

```shell
# 重命名当前分支, 通常情况下需要执行3步
# 1、修改分支名称
# 2、删除远程旧分支
# 3、将重命名分支推送到远程
git branch -m <branchName>
git push origin :old_branch
git push -u origin new_branch


# 重命名指定分支
git branch -m old_branch new_branch
```

### 合并分支

分支合并前需要先切换到主分支

```shell
git checkout dev
```

```shell
# 合并上一分支
git merge -

# 安静模式合并, 将dev合并至当前分支不输出任何信息
git merge dev -q

# 合并不编辑信息, 跳过交互
git merge dev --no-edit

# 合并分支不进行提交
git merge dev --no-commit

# 退出合并, 恢复至合并之前的状态
git merge --abort
```

### 变基

变基 ( rebase )：合并分支

**原理**：

1. 发起变基时，git 会先找到两条分支的共同祖先
2. 对比当前分支相对祖先的历史提交
3. 将当前部分作为执行目标的**基底**

变基相对于 `merge` 来说，结果是一样的，变基的代码提交记录更简洁清晰

```shell
# 1. 切换分支dev
git switch dev

# 2. 将dev的基底变为main
git rebase main
# 没有冲突, 直接推送

# 3. 处理冲突->暂存->变基->推送
git add -A
git rebase --continue # 继续
git push -f # 强制推送
```

中断变基

```shell
git rebase --abort
```

## 远程

```shell
# 查看远程服务器
# origin: 默认远程库名称
git remote

# 查看当前远程库的地址
git remote -v

# 添加远程库 remote_name默认为origin
git remote add <remote_name> https://github.com/YasakaKanoko/git-tutorial.git

# 修改分支的名称为 main 
git branch -M main

# -u: --set-upstream的简写, 将本地与远程建立追踪关系, 之后只需执行 git pull/git push
git push -u origin main
```

### 推送

```shell
# 等价于 git push origin, 实际上推送到一个叫 origin 默认仓库名字
git push

# 推送到主分支 <分支名> 本地与远程分支名称一致
git push -u origin main

# 本地分支推送到指定远程分支 <本地分支>:<远程分支>
git push origin <branchName>:<branchName>

# 强制推送, --force 缩写
git push -f
```

### 克隆

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

克隆指定文件夹

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

### 管理仓库

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

# 先确保远程库与本地库版本一致, fetch从远程库下载所有代码, 但不合并
git fetch
```

### tag

当头指针没有指向某分支的头部时，这种状态称为 **分离头指针**

分离头指针时，不要操作仓库

```shell
# 分离头指针
git switch aab508 --detach
```

执政并没有指向任何分支，操作仓库代码没有意义，正确做法是先创建一个新分支再将头指针指向

```shell
# 在记录为aab508上新建分支
git switch -c <branch_name> aab508
```

可以为提交记录设置标签，通过标签辨别不同的开发节点

```shell
# 当前分支上的<tag>是v1.0
git tag v1.0

# 1. 提交id为aab508的分支设置<tag>为v2.0
git tag v2.0 aab508

# 2. 为aab508新建分支并指向, 如果不新建分支会出现分离头指针问题
git switch -c test v2.0

# 3. 推送指定标签至远程库
git push origin v1.0

# 删除本地标签
git tag -d <tag_name>

# 删除远程标签
git tag <remote_name> --delete <tag_name>
```

### SSH_Key

```shell
# 1. 生成SSH_Key
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
# Enter passphrase (empty for no passphrase):    # 直接回车
# Enter same passphrase again:                   # 直接回车

# 2. 在用户目录: C:\Users\YasakaKanoko\.ssh
# id_rsa: 私钥
# id_rsa.pub: 公钥

# 3. 在GitHub的Settings -> SSH and GPG keys -> New SSH key
# Title 命名
# Key: id_rsa.pub公钥的内容
# Add SSH key

# 4. 验证
ssh -T git@github.com
# Hi YasakaKanoko! You've successfully authenticated, but GitHub does not provide shell access.
```

### gitignore

默认情况下，git 会监视所有内容，但有些内容不希望被监视 ，如：node_modules 的内容

设置 `.gitignore` 内容需要 git 忽略的文件

```pseudocode
# 忽略的内容
node_modules
yarn.lock
*.log
```

## gh-pages

在 GitHub 中，可以将静态页面部署到 GitHub 中

**要求**：

- 方式一：分支名必须为：`gh-pages`

  ```shell
  # 1. 添加远程库
  git remote add origin https://github.com/YasakaKanoko/git-tutorial.git
  
  # 2. 修改分支名为 gh-pages
  git branch -M gh-pages
  
  # 3. 推送分支
  git push -u origin gh-pages
  
  # 4. 通过xxx.github.io访问
  ```

- 方式二：新建仓库时，命名为 `xxx.github.io` 也可

### [Docusaurus](https://docusaurus.io/)

FB 推出的开源静态内容管理系统，快速部署一个静态网站

- 安装

  ```shell
  npx create-docusaurus@latest my-website classic
  ```

- 启动项目

  ```shell
  npm start
  ```

- 配置项目：`docusaurus.config.js` 项目配置文件

  ```javascript
  const config = {
      title: 'xxx', // 标题栏
      tagline: 'xxx', // 副标题
      url: 'https://xxx.github.io', // 网站根目录
      baseUrl: '/',
      onBrokenLinks: 'throw',
      onBrokenMarkdownLinks: 'warn',
      favicon: 'img/favicon.ico',
      organizationName: 'xxx', // 用户名
      projectName: 'xxx.github.io', // 仓库地址
      // 国际化: internalization
      i18n: {
          defaultLocale: 'zh',
          locales: ['zh']
      }
  };
  ```

- 部署：`npm run build`

  ```shell
  npm deploy
  ```

- 配置 `deploymentBranch` 指定分支

  ```javascript
  deploymentBranch: 'gh-pages'
  ```

- 配置环境变量：`GIT_USER` : `username`

