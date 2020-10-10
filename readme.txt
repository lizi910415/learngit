这是学习git的教程

在Windows上使用Git，可以从Git官网直接下载安装程序，然后按默认选项安装即可。

安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！

创建一个空目录，在当前目录 通过git init命令把这个目录变成Git可以管理的仓库：

成功后在当前目录有一个.git的目录

写个带内容的txt文件

通过git add txt文件名称.txt   把该文件添加到仓库（保存于暂存区）

通过 git commit -m "一段该文件的注释"   将文件提交到仓库

git status命令可以让我们时刻掌握仓库当前的状态

git diff顾名思义就是查看difference，显示的格式正是Unix通用的diff格式

git log命令显示从最近到最远的提交日志（git log --pretty=oneline在一行内输出）

Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^，
当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100

git reset --hard 1094a（1094a是某个版本的commitID，通过ID也可以将当前版本指定）

如果gitbash关闭，不知道之前的版本号，可以通过  git reflog查看操作日志，找到丢失的版本号

HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id

git checkout -- file可以丢弃工作区的修改：

rm test.txt 删除本地文件

git rm test.txt 删除版本库中的文件

如果误删本地文件，但是版本库有，可以通过git checkout -- test.txt恢复

git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

登陆GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：

要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；

关联后，使用命令git push -u origin master第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；

git checkout -b dev       git switch -c dev   创建并切换到最新分支

git branch dev  创建新分支

git checkout dev      git switch dev 切换分支

git branch -d dev  删除分支

git  merge dev 将用于合并指定分支到当前分支

Git鼓励大量使用分支：

查看分支：git branch

创建分支：git branch <name>

切换分支：git checkout <name>或者git switch <name>

创建+切换分支：git checkout -b <name>或者git switch -c <name>

合并某分支到当前分支：git merge <name>

删除分支：git branch -d <name>


文件存在冲突，必须手动解决冲突后再提交

git status也可以告诉我们冲突的文件：

Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容

当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

用git log --graph命令可以看到分支合并图。

当你在开发过程中遇到其他地方有bug需要紧急修复，而你当前的进度又未完成不能提交

Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作：

用git status查看工作区，就是干净的（除非有没有被Git管理的文件），因此可以放心地创建分支来修复bug。

工作区是干净的，刚才的工作现场存到哪去了？用git stash list命令看看：

工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：

一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；

另一种方式是用git stash pop，恢复的同时把stash内容也删了：

你可以多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash，用命令

git stash apply stash@{0}

在master分支上修复了bug后，我们要想一想，dev分支是早期从master分支分出来的，所以，这个bug其实在当前dev分支上也存在。

为了方便操作，Git专门提供了一个cherry-pick命令，让我们能复制一个特定的提交到当前分支

git cherry-pick COMMITID

修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场；

在master分支上修复的bug，想要合并到当前dev分支，可以用git cherry-pick <commit>命令，把bug提交的修改“复制”到当前分支，避免重复劳动。