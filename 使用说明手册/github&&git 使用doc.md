# **github&&git 使用doc**

![64142f240a0a52ee0b16b79b5ed8bcb](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/64142f240a0a52ee0b16b79b5ed8bcb.png)

## 初次上传

初始化一个git仓库 init （可以在某个目录下）

添加内容到这个仓库

提交 commit （提交这个修改）

将git默认主支名字改为main

将github远程仓库（url）添加到当前git库中 名字为origin 指向github上的仓库

将当前分支上的origin仓库 推送到github上的分支上，可以是mian

## 团队修改（二次上传）

![image-20241007144844199](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241007144844199.png)

![image-20241007144049194](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241007144049194.png)

首先先克隆这个仓库到本地（可以是某个目录下）

切换到新分支（和这个主枝克隆的一样）

在这个新分支上修改



![image-20241007144054332](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241007144054332.png)



提交（书写描述信息）

拉取github远程仓库中最新的main

也可以合并当本地主枝中或者分支中

![image-20241007144601663](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241007144601663.png)

然后再将当前origin仓库（分支上的）推送到远程仓库（任意分支（也可以是主枝））中\

![image-20241007145817229](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241007145817229.png)

![image-20241007145810048](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241007145810048.png)



## 工作流

![image-20241007151200835](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241007151200835.png)

## 问题就是如何回退版本呢







---



## vscode 替代命令行的图形化git技巧

## 常见错误

### 1.`refusing to merge unrelated histories


==解决方案==

![image-20241007154648775](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241007154648775.png)

### 2.

`To https://github.com/kasahuki/mdSets.git
! [rejected] main -> main (non-fast-forward)
error: failed to push some refs to 'https://github.com/kasahuki/mdSets.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. If you want to integrate the remote changes,
hint: use 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.`

==解决方案==

![image-20241007154806128](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241007154806128.png)

### 3.fatal: unable to access 'https://github.com/kasahuki/mdSets.git/': OpenSSL SSL_read: SSL_ERROR_SYSCALL, errno 0



**如果本地比线上落后是无法push到线上的 （本地一定要包含线上所有内容才行）**

**所以一定要先pull main分支** 

**pull有冲突的情况就是 线上的一个文件的一个区域修改了 同时本地这个同一个区域和这个不一样 pull的时候就会有冲突 所以 有三个选择** 

**留一个还是留两个（’树的左右‘）**

## git 配置用户信息 

username and useremail

应用在每次提交代码版本时表明自己的身份

## git 的三个区域

### 1.工作区

实际开发时操作的文件夹

### 2.暂存区

保存之前的准备区域（暂存改动的文件）

![image-20241019130912620](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241019130912620.png)

### 3.本地仓库（版本库）

提交并保存暂存区的内容，产生一个版本快照！

![image-20241019130926233](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241019130926233.png)

**git status 查看状态**

## 回退版本

git reset  三种模式

参数 ： --soft/--hard/--mixed（reset 的默认参数）

![4110112fab892439cb432d78d83bce2](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/4110112fab892439cb432d78d83bce2.jpg)

==**√ 表示保留当前区域的修改内容**==





## gitdiff 命令

**作用职能：查看三个区域之间的差别或者是不同分支的区别！**

git diff 比较 **工作区**  和 **暂存区** 

git diff head  **工作区**和 **版本库** 

git diff --cached 比较 **暂存区 **和 **版本库**

git diff  版本号1 版本号2 比较  **两个不同版本** 的区别

**对于上面所有 如果后面跟上 一个特定文件的话就是只比较这个文件！！！**

 head~表示上一个版本  head~2 表示后退两个版本比较

**注意：head 表示 指向当前分支的最新的提交结点**

## .gitignore

**忽略就表示不会添加到版本库中的**

![4afd7594879ef0d52899745e7c9a11f](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/4afd7594879ef0d52899745e7c9a11f.jpg)

可在该文件中编辑 内容可填写 特定文件名 正则表达式 e.g. *.log  还可忽略文件夹 xxx/temp/

**#后表示注释内容！！**

**但是如果在编写这个ignore文档之前就已经有不想要的文件添加到版本库中了就需要先删除**

## 删除 

git rm xxx 此为强制删除 

如果只想在 版本库中删除的话 git rm -cached xxx 

## 显示

![image-20241019132745434](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241019132745434.png)

---



![image-20241019132748622](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241019132748622.png)



**注意点：git是不会将空文件夹加入到版本库中的！**

## push/pull

**git push/pull -u origin(本地仓库name) main(本地仓库):main(远程仓库)**



## 关于分支 

**branch**

git branch 查看分支

git branch newBranch 仅创建新分支 不会切换

git checkout(可能会产生冲突)/ switch



## 合并（merge）与冲突

**与pull冲突类似 merge 也会有冲突！**

**合并时要切换到主支上然后 merge 想要的添加新功能的分支**

### 删除分支

git branch -d branch-name 已经合并的了

git branch -D branch-name  还未合并的（强制删除）

冲突 ：两个分支同时修改了同一个文件

合并时就不知道要保留谁的了

### 解决冲突

可使用 diff 或是 status来 查看冲突位置

然后手动修改 需要保留的地方或是 自己手动合并 

**然后重新add commit 就会自动合并了 （解决冲突）**

## Rebase

可在任意分支上进行rebase操作

类似指针的修改操作！！

![fddc0634f3f0e7cda823162283a160e](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/fddc0634f3f0e7cda823162283a160e.jpg)

## 最重要！ 分支管理和工作流模型



## 使用GUI工具 & IDE使用git

**在 GitHub 的 commit 差异视图中，以蓝色背景显示的数字（如 @@ -54,8 +71,7 @@）是称为"差异块头"（hunk header）的内容，用来表示代码更改的位置信息。**

**让我解释这个格式：**

- **@@ 是差异块的开始标记**
- **-54,8 表示原文件中的变更：从第54行开始，共8行**
- **+71,7 表示新文件中的变更：从第71行开始，共7行**
- **@@ 是差异块的结束标记**

**简单来说，这个标记告诉我们：**

- **在原始文件中，变更从第54行开始，涉及8行代码**
- **在新文件中，变更从第71行开始，涉及7行代码**

**这种标记方式帮助开发者快速定位代码变更的具体位置，是 git diff 输出的标准格式之一。**

![image-20241207140433159](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20241207140433159.png)

### 暂存区的作用（staged）



~~~tex
在 Git 中，暂存区（Staging Area，也称为索引区 Index）是一个非常重要的概念，主要用于在你正式提交（commit）之前，暂时存储和组织你想要提交的更改。它是工作区（Working Directory）和版本库（Repository）之间的缓冲地带。

暂存区的作用：
精确控制提交内容：
暂存区允许你将工作区的更改分批添加到提交中，而不是一次性提交所有更改。通过 git add，你可以选择性地将某些文件或某些部分的更改放入暂存区，然后再进行提交。
这在管理复杂项目时特别有用，尤其是当你同时在处理多个独立功能或修复问题时，可以确保每次提交的内容是独立且清晰的。
预览和组织提交：
在提交之前，你可以通过 git status 或 git diff --cached 查看暂存区的内容，确保提交的内容是正确的。
这为你提供了一个机会，在提交之前整理和核对更改。
提高提交的灵活性：
暂存区允许你分阶段提交工作。例如，你可以先提交一部分代码，然后继续修改未提交的部分，而不需要一次性提交所有更改。
支持部分文件提交：
Git 提供了一个非常强大的功能，允许你将文件中的部分更改添加到暂存区，而不是整个文件。通过 git add -p 或 git add -i，你可以交互式地选择哪些更改应该进入暂存区。这在代码审查或调整提交历史时非常有用。
中间缓冲区：
暂存区是工作区和版本库之间的缓冲区，所有的更改在进入版本库之前必须先进入暂存区。这种设计使得 Git 的操作更加灵活。
~~~

### commit和tag区别

​	

| **区别点**       | **Commit**                                 | **Tag**                              |
| :--------------- | :----------------------------------------- | :----------------------------------- |
| **作用**         | 提交代码更改，记录项目的开发历史           | 标记某个提交，通常用于版本标记       |
| **核心功能**     | 记录项目的快照和更改历史                   | 用于标记重要的提交点，便于查找和引用 |
| **创建频率**     | 开发过程中频繁创建                         | 通常在重要版本（如发布时）创建       |
| **是否可变**     | 提交不可更改（但可以修改历史）             | 标签是静态的，指向固定的提交         |
| **是否需要信息** | 每次提交需要附带提交信息（commit message） | 标签可以附注信息（Annotated Tag）    |
| **指向**         | 指向一个项目的快照                         | 指向某个提交（commit）               |

### stash





![52bac5116a6fd98cadb607acdaf3f20](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/52bac5116a6fd98cadb607acdaf3f20.jpg)



# 开放模式工作流

~~~tex
一轮开发流程通常如下：
	1.	拉取最新代码
从 GitHub 仓库拉取最新代码（git pull origin main 或其他默认分支），确保本地代码是最新的。
	2.	创建本地分支
基于主分支（如 main 或 develop）创建一个新的本地分支（git checkout -b feature/branch-name），用于独立开发新功能或修复问题。
	3.	在分支上开发
在本地分支上完成开发工作并进行测试，确保功能完整且代码质量达标。
	4.	推送分支到远程仓库
将本地分支推送到远程仓库（git push origin feature/branch-name），为创建 Pull Request 做准备。
	5.	创建 Pull Request
在 GitHub 上创建一个 Pull Request，请求将分支代码合并到主分支，并说明开发内容。
	6.	代码评审
团队成员对 Pull Request 进行代码评审（Code Review），提出修改建议或确认代码可以合并。
	7.	合并代码
通过评审后，将 Pull Request 合并到主分支（在 GitHub 上点击 “Merge”）。
	8.	删除分支
	•	删除远程分支：git push origin --delete feature/branch-name
	•	删除本地分支：git branch -d feature/branch-name
~~~

