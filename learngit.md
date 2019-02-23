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