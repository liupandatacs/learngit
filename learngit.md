# GIT学习笔记 by 廖雪峰

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

* 要关联一个远程库，使用命令

  ```
  git remote add origin git@username/file.git
  关联后，使用命令 git push -u origin master 第一次推送master分支的所有内容；
  此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改
  ```

  

