Git is a version control system.
Git is free software.
Git is free software distributed under GPL.
Git has a mutable index called stage
Git tracks not file but changes that is why the Git better than other version control system.

1.init :git init
2.add: git add <file>
3.commit: git commit -m <message>
4.show the workspace's status: git status
5.show something it was changed: git diff
6.log: git log <--pretty=oneline>
7.reset : git reset --hard HEAD^< or HEAD^^ or HEAD~100 or commit version number> 
8.log your ever command< it cound found your lastest commit version>: git reflog
9.to show the distinguiash between workspace and reporsitory: git diff HEAD -- <file name>
10.removed changes<命令git checkout -- readme.txt意思就是:
    把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
    一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
    一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
    总之，就是让这个文件回到最近一次git commit或git add时的状态。>: git checkout -- <file name>
    <命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到git checkout命令。>
11.unstage lastest changes<git reset命令既可以回退版本，
也可以把暂存区的修改回退到工作区。>: git reset HEAD <file name>
12.notice：
    场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
	git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。
	注意：从来没有被添加到版本库就被删除的文件，是无法恢复的！
	场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，
        第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。
	场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。
13.delete file in stage: rm <file name>
14.delete file in workspace<命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，
但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。>: 1)git rm <file name> 2)git commit
15.…or create a new repository on the command line
    echo "# learningGit" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git remote add origin git@github.com:Pendlerer/learningGit.git
    git push -u origin master
  …or push an existing repository from the command line
    git remote add origin git@github.com:Pendlerer/learningGit.git
    git push -u origin master
  …or import code from another repository
    You can initialize this repository with code from a Subversion, Mercurial, or TFS project.
	要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；
	关联后，使用命令git push -u origin master第一次推送master分支的所有内容；
	此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；


