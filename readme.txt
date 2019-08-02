Git is a version control system.
Git is free software.
Git is free software distributed under GPL.
Git has a mutable index called stage
Git tracks not file but changes that is why the Git better than other version control system.
/************创建版本库*************/
0.创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录：
$ mkdir learngit
$ cd learngit
$ pwd    /*pwd命令用于显示当前目录*/
/Users/michael/learngit
1.init :git init
/**************文件管理*********************/
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
/********************远程仓库***************************/
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
16.clone from the origin: git clone git@github.com:<your github account name>/<your repository name>.git
    如果有多个人协作开发，那么每个人各自从远程克隆一份就可以了。你也许还注意到，GitHub给出的地址不止一个，
	还可以用https://github.com/michaelliao/gitskills.git这样的地址。Git支持多种协议，默认的git://使用ssh，但也可以使用https等其他协议。
	使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。
	要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。
	Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。<使用http协议时git 命令最后不需要.git>
/**************************分支管理*************************************/
17.build a branch: git checkout -b <branch name>
    git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
	$ git branch dev
	$ git checkout dev
	Switched to branch 'dev'
18.show branch: git branch
19.Switched to branch 'master': git checkout master
20.合并指定分支到当前分支: git merge <待合并分支名>
21.delete branch: git branch -d <branch name>
    Git鼓励大量使用分支：
	查看分支：git branch
	创建分支：git branch <name>
	切换分支：git checkout <name>
	创建+切换分支：git checkout -b <name>
	合并某分支到当前分支：git merge <name>
	删除分支：git branch -d <name>
22.当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
   解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。
   用git log --graph命令可以看到分支合并图。
23.merge with --no-ff: git merge --no-ff -m "merge with no-ff" dev
    分支策略:在实际开发中，我们应该按照几个基本原则进行分支管理：
	首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
	那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，
	比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
	你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。
	Git分支十分强大，在团队开发中应该充分应用。
	合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，
	而fast forward合并就看不出来曾经做过合并。
24.save workspace: git stash
25.show stash； git stash list
26.recovery workspace but not dalete stash: git stash apply
    你可以多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash，
    用命令：git stash apply stash@{0}
27.delete stash: git stash drop
28.recovery workspace and dele stash: git stash pop
29.开发一个新feature，最好新建一个分支；如果要丢弃一个没有被合并过的分支，
    可以通过git branch -D <name>强行删除。
30.show remote repository name: git remote< or git remote -v>
31.push branch: git push origin master< branch name that wait to be pushed>
    但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？
	    master分支是主分支，因此要时刻与远程同步； 
		dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
		bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
		feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。
	总之，就是在Git中，分支完全可以在本地自己藏着玩，是否推送，视你的心情而定！
32.创建远程origin的dev分支到本地: git checkout -b dev origin/dev
34.因此，多人协作的工作模式通常是这样：
    首先，可以试图用git push origin <branch-name>推送自己的修改；
    如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
    如果合并有冲突，则解决冲突，并在本地提交；
    没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
    如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，
	用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。
    这就是多人协作的工作模式，一旦熟悉了，就非常简单。
    小结
    查看远程库信息，使用git remote -v；
    本地新建的分支如果不推送到远程，对其他人就是不可见的；
    从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
    在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
    建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
    从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。
35.rebase操作可以把本地未push的分叉提交历史整理成直线: git rebase
    rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。
	作者这个教程中,省略了一堆操作,前面至少要有一个人先提交同一个文件,
	造成此时要操作的本地git库与远程不符,再在本地git进行提交操作.
	并且,重要的是作者并没有写出git rebase处理过程,使用git rebase之后,
	只是返回冲突出现的提交处的commit,之后要在这个commit中进行解决冲突;
	再使用git add操作添加好要解决冲突后的文件,之后还要再执行一次git rebase --continu,
	到此git rebase衍合过程才真正结束;
36.命令git tag <tagname>用于新建一个标签，默认为HEAD，也可以指定一个commit id；
    命令git tag -a <tagname> -m "blablabla..."可以指定标签信息；
	命令git tag可以查看所有标签。
	可以用git show <tagname>查看标签信息
37.delete tag: git tag -d <tag name>
   push tag: git push origin <tagname>
   push all unpushed tags: git push origin --tags
   delete tag on origin:1)delete local tag:git tag -d <tagname>;2)delete origin tag:git push origin :refs/tags/<tagname>
38.在GitHub上，可以任意Fork开源仓库；
    己拥有Fork后的仓库的读写权限；
	可以推送pull request给官方仓库来贡献代码。
39.忽略某些文件时，需要编写.gitignore；
    .gitignore文件本身要放到版本库里，并且可以对.gitignore做版本管理！

