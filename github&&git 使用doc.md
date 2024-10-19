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

git status 查看状态

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



---



## 使用GUI工具 



---



## SSH配置



---



## Gitee以及Gitlab的使用







---



## vscode使用git





---



## vscode 使用文档 

**shift + alt + F 一键格式化代码**

shift +alt +上下箭头 快速复制
