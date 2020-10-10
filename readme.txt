这是学习git的教程，摘录廖雪峰博客

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