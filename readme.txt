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
	场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，
        第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。
	场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。
13.