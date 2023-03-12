# git

Git 是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。

Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。

Git 与常用的版本控制工具 CVS, Subversion 等不同，它采用了分布式版本库的方式，不必服务器端软件支持。

## 目录

- [git](#git)
  - [目录](#目录)
  - [工作区](#工作区)
    - [工作区](#工作区-1)
    - [暂存区](#暂存区)
    - [版本库](#版本库)
  - [文件状态](#文件状态)
  - [常用命令](#常用命令)
    - [git 全局设置](#git-全局设置)
    - [获取git仓库](#获取git仓库)
      - [在本地初始化git仓库](#在本地初始化git仓库)
      - [从远程仓库克隆](#从远程仓库克隆)
    - [查看文件状态](#查看文件状态)
    - [将文件的修改加入暂存区](#将文件的修改加入暂存区)
    - [将暂存区的文件取消暂存或者是切换到指定版本](#将暂存区的文件取消暂存或者是切换到指定版本)
    - [将暂存区的文件修改提交到版本库](#将暂存区的文件修改提交到版本库)
    - [查看日志](#查看日志)
    - [查看远程仓库](#查看远程仓库)
    - [添加远程仓库](#添加远程仓库)
    - [从远程仓库克隆](#从远程仓库克隆-1)
    - [从远程仓库拉取](#从远程仓库拉取)
    - [推送到远程仓库](#推送到远程仓库)
  - [分支操作](#分支操作)
    - [查看分支](#查看分支)
    - [创建分支](#创建分支)
    - [切换分支](#切换分支)
    - [推送至远程仓库分支](#推送至远程仓库分支)
    - [合并分支](#合并分支)
  - [标签操作](#标签操作)
    - [列出已有的标签](#列出已有的标签)
    - [创建标签](#创建标签)
    - [将标签推送至远程仓库](#将标签推送至远程仓库)
    - [检出标签](#检出标签)
  - [cherry-pick](#cherry-pick)
    - [概述](#概述)
    - [用法](#用法)
  - [Git Flow](#git-flow)
    - [概念](#概念)
    - [优势](#优势)
  - [**GitFlow**基本分支](#gitflow基本分支)
    - [master](#master)
    - [develop](#develop)
    - [feature](#feature)
    - [release](#release)
    - [hotfix](#hotfix)


---

## 工作区

![1673337703685](1673337703685.png)

### 工作区

包含 .git 文件夹的目录就是工作区，也称为工作目录，主要用于存放开发的代码。

### 暂存区

.git 文件夹中有很多文件，其中有一个 index 文件就是暂存区，也可以叫做 stage。暂存区是一个临时保存修改文件的地方。

### 版本库

.git 隐藏文件夹就是版本库，版本库中储存了很多配置信息、日志文件和文件版本信息等。

## 文件状态

git工作区中文件存在两种状态：

* untracked 未跟踪（未被纳入版本控制）
* tracked 已跟踪（被纳入版本控制）
  1. Unmodified 未修改状态
  2. Modified 已修改状态
  3. Staged 已暂存状态

## 常用命令

### git 全局设置

* 设置用户信息

  ```powershell
  git config --global user.name "ZFined"
  git config --global user.email "1749895520@qq.com"
  ```
* 查看配置信息

  ```powershell
  git config --list
  ```

### 获取git仓库

#### 在本地初始化git仓库

* 执行命令

  ```powershell
  git init
  ```

#### 从远程仓库克隆

* 执行命令

  ```powershell
  git clone [远程git仓库地址]
  ```

### 查看文件状态

* 执行命令

  ```powershell
  git status
  ```

### 将文件的修改加入暂存区

* 执行命令
  ```powershell
  git add ./
  ```

### 将暂存区的文件取消暂存或者是切换到指定版本

* 执行命令

  ```powershell
  git reset [文件名] # 将文件取消暂存
  git reset --hard [提交记录的编号] # 切换到指定版本
  ```

### 将暂存区的文件修改提交到版本库

* 执行命令
  ```powershell
  git commit
  ```

### 查看日志

* 执行命名
  ```powershell
  git log
  ```

### 查看远程仓库

* 执行命令
  ```powershell
  git remote
  git remote -v # 查看远程仓库详细地址
  ```

### 添加远程仓库

* 执行命令
  ```powershell
  git remote add [自定义远程仓库名称（建议使用origin）] [远程仓库地址]
  ```

### 从远程仓库克隆

* 执行命令
  ```powershell
  git clone [远程仓库地址]
  ```

### 从远程仓库拉取

* 执行命令

  ```powershell
  git pull [远程仓库名称（默认是origin）] [分支名称（主分支默认为master）]
  ```

  如果当前本地仓库不是从远程仓库克隆的，而是本地创建的仓库，并且仓库中存在文件，此时从远程仓库拉取文件的时候会报错。
* 解决此问题可以通过在 git pull 命令后加入参数 --allow-unrelated-histories

### 推送到远程仓库

* 执行命令
  ```powershell
  git push [远程仓库名称（默认是origin）] [分支名称（主分支默认为master）]
  ```

## 分支操作

分支操作是 git 使用过程中非常重要的概念。使用分支意味着你可以把工作从开发主线上分离开来，以免影响开发主线。

同一个仓库可以有多个分支，每个分支相互独立，互不干扰。

通过 git init 命令创建本地仓库时默认会创建一个 master 分支。

### 查看分支

* 执行命令
  ```powershell
  git branch	# 列出所有本地分支
  git branch -r	# 列出所有远程分支
  git branch -a	# 列出所有本地分支和远程分支
  ```

### 创建分支

* 执行命令
  ```powershell
  git branch [分支名称]
  ```

### 切换分支

* 执行命令
  ```powershell
  git checkout [分支名称]
  ```

### 推送至远程仓库分支

* 执行命令
  ```powershell
  git push [远程仓库名称] [分支名称]
  ```

### 合并分支

* 执行命令

  ```powershell
  git merge [分支名称]
  ```
* 如果存在分支，会在文件中显示冲突的内容，需要自行修改后再提交（push）一次才能解决冲突

## 标签操作

git 中的标签，指的是某个分支某个特定时间点的状态。通过标签，可以很方便的切换到标记时的状态。

### 列出已有的标签

* 执行命令
  ```powershell
  git tag
  ```

### 创建标签

* 执行命令
  ```powershell
  git tag [标签名称]
  ```

### 将标签推送至远程仓库

* 执行命令
  ```powershell
  git push [远程仓库名称] [标签名称]
  ```

### 检出标签

* 执行命令

  ```powershell
  git checkout -b [分支名称] [标签名称]
  ```

## cherry-pick

来自 [Git cherry-pick 这个命令你会经常用到！ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/90816644)

### 概述

`git cherry-pick`可以理解为”挑拣”提交，它会获取某一个分支的单笔提交，并作为一个新的提交引入到你当前分支上。当我们需要在本地合入其他分支的提交时，如果我们不想对整个分支进行合并，而是只想将某一次提交合入到本地当前分支上，那么就要使用 `git cherry-pick`了。

### 用法

```powershell
git cherry-pick [options] [commit]
# 常用的 options
#	--quit		退出当前的 cherry-pick 序列
#	--continue	继续当前的 cherry-pick 序列
#	--abort		取消当前的 cherry-pick 序列，恢复当前分支
#	-n，--no-commit	不自动提交
#	-e，--edit	编辑提交信息
```

## Git Flow

来自 [Git Flow详细介绍和使用 - 简书 (jianshu.com)](https://www.jianshu.com/p/9d1c997b7613)

### 概念

Git Flow定义了一个项目发布的分支模型，为管理具有预定发布周期的大型项目提供了一个健壮的框架，是由 Vincent Driessen 提出的一个 git 操作流程标准、解决当分支过多时 , 如何有效快速管理这些分支。

### 优势

**并行开发** ：GitFlow可以很方便的实现并行开发。每个新功能都会建立一个新的 feature 分支，从而和已经完成的功能隔离开来，而且只有在新功能完成开发的情况下，其对应的feature分支才会合并到主开发分支上（也就是我们经常说的develop分支）。另外，如果你正在开发某个功能，同时又有一个新的功能需要开发，你只需要提交当前 feature 的代码，然后创建另外一个feature 分支并完成新功能开发。然后再切回之前的 feature 分支即可继续完成之前功能的开发。

**协作开发** ：GitFlow 还支持多人协同开发，因为每个 feature 分支上改动的代码都只是为了让某个新的 feature 可以独立运行。同时我们也很容易知道每个人都在干啥。

**阶段式发布** ：当一个新 feature 开发完成的时候，它会被合并到 develop 分支，这个分支主要用来暂时保存那些还没有发布的内容，所以如果需要再开发新的 feature，我们只需要从 develop 分支创建新分支，即可包含所有已经完成的 feature 。

**支持紧急修复** ：GitFlow 还包含了 hotfix 分支。这种类型的分支是从master上创建出来并做一个紧急的修复，而且这个紧急修复只影响这个已经发布的 tag，而不会影响到你正在开发的新 feature。

## **GitFlow**基本分支

### master

master 分支存放所有正式发布的版本，可以作为项目历史版本记录分支，不直接提交代码。仅用于保持一个对应线上运行代码的code base。

### develop

develop 分支为主开发分支，不直接提交代码

### feature

feature 分支为新功能分支，feature分支都是基于develop创建的，开发完成后会合并到develop分支上。同时存在多个

### release

release 分支基于最新develop分支创建，当新功能足够发布一个新版本(或者接近新版本发布的截止日期)，从develop分支创建一个release分支作为新版本的起点，用于测试，所有的测试bug在这个分支改。测试完成后合并到master并打上版本号，同时也合并到develop，更新最新开发分支。(一旦打了release分支之后不要从develop分支上合并新的改动到release分支)，同一时间只有一个，生命周期很短，只是为了发布。

### hotfix

hotfix 分支基于master分支创建，对线上版本的bug进行修复，完成后直接合并到master分支和develop分支，如果当前还有新功能release分支，也同步到release分支上。同一时间只有1个，生命周期较短
