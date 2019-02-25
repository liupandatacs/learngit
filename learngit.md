# GIT学习笔记 by 廖雪峰

[](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

## 第一页

### 创建版本库

* 创建空目录

  ```
  //创建空目录
  mkdir learngit
  cd learngit
  // 目录路径
  pwd
  ```

* 通过**git init** 把目录变成GIT可以管理的仓库：

  ```
  $ git init
  Initialized empty Git repository in D:/GIThub/test/learngit/.git/
  ```

  > 在当前目录下会生成<font color=#FF0000> **.git** </font> 的目录，这个目录是**Git**来跟踪管理版本库的,如果没有看到<font color=#FF0000> **.git** </font> 目录，用**ls -ah**就可以了。

* ```markdown
  // 添加文件到仓库
  $ git add learngit.md
  // 把文件提交到仓库**-m**后面输入的是本次交的说明
  $ git commit -m "learn git first"
  [master (root-commit) 998faa6] learn git first
   1 file changed, 29 insertions(+)
   create mode 100644 learngit.md
  ```

  > git commit 成功后：
  >
  > **1 file changed**: 1个文件被改动；
  >
  > **29 insertions**：插入了29行内容

### 小结

* 初始化一个Git仓库，使用git init命令
* 添加文件到Git仓库，分两步：
  * 1. git add <file>,可以反复使用，添加多个文件；
    2. 使用git commit -m <message>,完成。

## 第二页

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   learngit.md

no changes added to commit (use "git add" and/or "git commit -a")

```

* git status可以让我们时刻掌握仓库当前的状态，上面的命令说明文档被修改过，但还没有提交

```
$ git diff
```

* git diff 说明了文档做的修改

### 小结

* 要随时掌握工作区的状态，使用git status 
* 如果git status 告诉你文件被修改过，用git diff可以查看修改内容

# 第三页

```
git log [--pretty=oneline] ：该命令可以查看从最近到最远的记录
commit 1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master)
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:06:15 2018 +0800
//回退到上一版本
git reset --hard HEAD^
HEAD is now at e475afc add distributed

Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交1094adb...（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

git reflog: 提交的历史记录
git reset --hard <commit id> 重新回到当前记录
```

### 小结

- `HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。
- 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。
- 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

* 你又理解了Git是如何跟踪修改的，每次修改，如果不用`git add`到暂存区，那就不会加入到`commit`中。

* git checkout -- file: 把file文件在工作区的修改全部撤销，这里有两种情况：

  总之就是让文件回到最近一次git commit或git add时的状态

  场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

  场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。

  场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考[版本回退](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013744142037508cf42e51debf49668810645e02887691000)一节，不过前提是没有推送到远程库。

  ## 提交到远程库

* **最后一步，就是提交到远程，终于要来了！！要关联一个远程库，使用下面命令**

  ```
  git remote add origin git@username/learngit.git
  关联后，使用命令 git push -u origin master 第一次推送master分支的所有内容；
  此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改
  ```

  # # 命令总结

  ```
  上文主要讲了先创建本地库，然后再建远程库，关联远程库的过程。主要命令：
  //初始化本地库
  git init 
  // 将本地文件添加到暂存区
  $ git add learngit.md
  //观察库的状态。如果状态显示没有更新或修改，则不会commit
  git status
  // 把文件提交到仓库**-m**后面输入的是本次交的说明
  $ git commit -m "learn git first"
  //关联远程仓库
  git remote add origin git@username/learngit.git
  //第一次推送master分支的所有内容；
   git push -u origin master
   //此后，每次本地提交后，只要有必要，就可以使用下面命令推送最新修改
   git push origin master
  ```

  ### 移除本地仓库和远程仓库的关联

  如果**远程仓库**作废或者添加了错误的**远程仓库地址**，可以用下面的命令移除掉。

  注意：origin后面的内容需要和关联远程仓库时填写的内容一致才可以。

  ```
  git remote rm origin //path.git
  ```

  ### 推送本地修改到远程

  推送前一定要先拉取最新代码，并且每次修改前及时拉取最新代码是非常好的习惯。

  ```markdown
  // 拉取最新代码,该命令用于从另一个存储库或本地分支获取并集成（整合）
  //主要作用是取回远程主机某个分支的更新，再与本地的指定分支合并
  git pull origin master
  // 查看本地仓库状态
  git status
  //将所有修改更新至暂存区
  git add .
  //提交暂存区更改 并写上明确的注释说明
  git commit -m "注释内容"
  // 提交修改至主分支
  git push origin master
  ```

  至此就可以完成从仓库初始化到文件提交的完整过程了。

  如果是参与已经存在的项目，即远程仓库已经存在并且已有项目文件在了，下面介绍如何参与已有项目。

## 从远程库关联

* 先在远程中新建一个仓库，远程仓库准备好后，使用下面命令克隆一个本地库

```
//首先需要clone远程仓库到本地，然后拉取新代码就可以了
git clone git@path/file.git
// 查看远程仓库版本
git remote -v
// 拉取远程仓库更新，git fetch:相当于从远程获取最新版本到本地，不会自动合并。
git fetch origin master
```

> 注意：git pull 与git fetch的区别
>
> ```
> // 从远程的origin的master主分支下载
> git fetch origin master:tmp
> //比较本地的master 分支和origin/master分支的差别
> git diff temp
> //最后进行合并
> git merge tmp
> 
> git pull:相当于从远程获取最新版本并merge到本地
> git pull origin master
> 其实就相当于，git fetch 和git merge,在实际应用中，git fetch 更安全一些，因为在merge前，可以查看新情况，然后再决定是否合并。
> ```
>
> 

## 强制覆盖本地文件

有时候临时在**本地仓库**做了修改，但是不想保留，再拉取更新的时候要强制覆盖本地文件，可以用如下命令

```
git fetch --all
git reset --hard origin/master
git pull
```



### 小结

要克隆一个仓库，首先必须知道仓库的地址，然后使用`git clone`命令克隆

Git 支持多种协议，包括`https`，但通过`ssh`支持的原生`git`协议速度最快

