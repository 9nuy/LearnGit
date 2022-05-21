Git 分布式版本控制软件

版本控制：文件 -> 本地 -> 集中式 -> 分布式

# Git 三大区域

* 工作区：就是你在电脑里能看到的目录。
* 暂存区：英文叫 stage 或 index。一般存放在 `.git/index` 中，所以暂存区也叫作索引（index）。
* 版本库：工作区有一个隐藏目录 `.git` ，这个不算工作区，而是 Git 的版本库。

 ![](https://www.runoob.com/wp-content/uploads/2015/02/1352126739_7909.jpg)

# Git 基本操作

 ![](https://www.runoob.com/wp-content/uploads/2015/02/git-command.jpg)

## 创建仓库

### git init

```
git init  # 当前目录初始化仓库
git init newrepo  # 指定目录初始化仓库
```

### git clone

```
git clone repo  # 克隆仓库
git clone repo directory  # 指定本地目录
```

## 提交与修改

### git status

```
git status  # 查看仓库当前的状态，显示有变更的文件
git status -s
```

### git add

```
git add file1 file2  # 添加文件到暂存区
git add dir  # 添加指定目录到暂存区
git add *.html  # 添加某个文件类型到暂存区
git add .  # 添加当前目录下的所有文件到暂存区
```

### git commit

```
# 设置提交的用户信息
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

```
git commit -m [message] # 提交暂存区到本地仓库
git commit file1 file 2-m [message] # 提交暂存区的指定文件到本地仓库
```

### git reset

```
git reset [--soft | --mixed | --hard] [HEAD]
git reset HEAD^  # 回退所有内容到上一个版本  
git reset HEAD^ hello.php  # 回hello.php文件到上一个版本  
git reset 052e  # 回退到指定版本
```

* `--mixed` 为默认，重置暂存区的文件，工作区文件内容保持不变 （`git reset HEAD` 可以把暂存区的修改撤销掉）
* `--soft` 回退到某个版本，**仅移动版本库 `HEAD` 指针**，暂存区、工作区不会重置
* `--hard` 撤销工作区中所有未提交的修改内容，将暂存区与工作区都回到上一次版本

* > `HEAD` 、`HEAD~0` 表示当前版本
  >
  > `HEAD^` 、`HEAD~1` 上一个版本
  >
  > `HEAD^^` 、`HEAD~2` 上上一个版本

### git checkout

```
git checkout -- file
```

* 文件自修改后还没有被放到暂存区，撤销修改就回到和版本库一样的状态
* 文件已经添加到暂存区后，又作了修改，撤销修改就回到添加到暂存区后的状态

### git diff

```
git diff  # 比较文件的不同，即暂存区和工作区的差异
```

### git log

```
git log  # 查看历史提交记录
git log --oneline
git reflog
```

# Git 分支管理

## git branch

```
git branch  # 列出分支
git branch (branchname)  # 创建分支
git branch -d (branchname)  # 删除分支
```

## git checkout

```
git checkout (branchname)  # 切换分支
```

## git merge

```
git checkout master
git merge (branchname)  # 合并分支
```

## 合并冲突

```
git branch dev  # 开发功能
git add.
git commit -m ...
git branch master
```

```
git branch bug  # 修复bug
git add.
git commit -m ...
git branch master
git merge bug
git branch -d bug
```

```
git merge dev
# CONFLICT (content): Merge conflict in ...
```

* 需要手动修改并重新 `git add`

# Github

## git remote

```
git remote  # 查看当前的远程仓库
git remote add [shortname] [url]  # 添加远程仓库
git remote rm [别名]  # 删除远程仓库
```

### 免密码登录

* URL实现

```
git remote add origin https://github.com/...
git remote add origin https://用户名:密码@github.com/...
```

* SSH实现

```
# 生成公钥和私钥：默认放在~/.ssh目录下，id_rsa.pub为公钥，id_rsa为私钥
ssh-keygen -t rsa -C "youremail@example.com"  #  Github的注册邮箱
# 拷贝公钥的内容，并设置到Github
ssh -T git@github.com  # 验证是否成功
git remote add origin git@github.com:...  # 配置SSH地址
```

## git push

```
git push <远程主机名> <本地分支名>:<远程分支名>
git push <远程主机名> <本地分支名>  # 如果本地分支名与远程分支名相同，冒号后面可以省略
```

```
git push -u origin master  # 将本地的master分支推送到origin主机，同时指定origin为默认主机
```

## git pull

```
git pull <远程主机名> <远程分支名>:<本地分支名>
git pull origin master:brantest
git pull origin master  # 如果远程分支是与当前分支合并，冒号后面可以省略
```

* `git pull` 其实就是 `git fetch` 和 `git merge FETCH_HEAD` 的简写

### 保留本地修改

```
git stash  # 保存当前工作进度到堆栈中
git pull origin master 
git stash pop  # 恢复最新的进度到工作区
```

