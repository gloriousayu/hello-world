[config]
git config --global user.name "Scott Chacon"
git config --global user.email "schacon@gmail.com"
ssh-keygen -t ra -C "schacon@gmail.com"

[clone]
git clone git@github.com:gloriousayu/git-tutorial.git git-tutorial
git clone git://git.kernel.org/pub/scm/git/git.git
git clone http://www.kernel.org/pub/scm/git/git.git			在默认情况下，Git会把"Git URL"里目录名的'.git'的后辍去掉,做为新克隆(clone)项目的目录名

[CRUD]
git init								初始化一个新的仓库
git status								查看状态
git add file1 file2 file3				修改文件，将它们更新的内容添加到索引中
git add -i								交互式添加
git commit
git commit -a							自动把所有内容被修改的文件(不包括新创建的文件)都添加到索引中，并且同时把它们提交
git commit -m 'commit message'
git commit -am 'commit message'
git commit --amend						修改上一条提交信息

git revert HEAD							撤消最近的一个提交
git revert HEAD^						撤消“上上次”(next-to-last)的提交
git revert 其实不会直接创建一个提交(commit), 把撤消后的文件内容放到索引(index)里

git reset --hard						让仓库的HEAD、暂存区、工作目录回溯到某指定状态（默认为HEAD）
git reset --hard HEAD					等同于git reset --hard
git reset --hard ORIG_HEAD				你已经把合并后的代码提交，但还是想把它们撒销
git checkout -- hello.rb				只是要恢复一个文件,如"hello.rb",

[branch]
git branch experimental					创建一个新分支
git branch								得到当前仓库中存在的所有分支列表
git branch -a 							同时显示本地仓库和远程仓库的分支
git branch -d experimental				只能删除那些已经被当前分支的合并的分支
git branch -D crazy-idea				强制删除某个分支
git checkout experimental				切换到新分支
git checkout -b experimental			创建并切换到新分支
git checkout -b feature origin/feature	基于远程分支，创建一个本地仓库的分支，后面是获取来源的分支名称
git checkout -							切换回上一个分支
git merge experimental					合并“experimental”到当前分支
git merge --no-ff experimental			为了在历史记录中明确记录下本次分支合并，需要创建合并提交
git merge --abort						退出合并

[diff]
git diff 是一个难以置信的有用的工具，可以找出你项目上任意两点间 的改动，或是用来查看别人提交进来的新分支
git diff master..test					显示两个分支间的差异
git diff								工作目录和本地索引(暂存区)之间的差异
git diff --cached						本地索引和最新提交之间的差异
git diff HEAD							工作目录与最新提交之间的差异，但不包括新增的文件(可能是前两者之和)
git diff test							查看当前的工作目录与另外一个分支的差别
git diff HEAD -- ./lib 					加上路径限定符，来只 比较某一个文件或目录(另外一个分支)
git diff --stat							不是查看每个文件的详细差别，而是统计一下有哪些文件被改动，有多少行被改 动

[rebase]	更改历史
git rebase origin
git rebase -i HEAD~2					合并当前分支中最近两个历史记录
git rebase --continue
git rebase --abort

[pull/push]
git pull命令执行两个操作: 它从远程分支抓取修改 的内容，然后把它合并进当前的分支
git remote add bob /home/bob/myrepo		要经常操作远程分支(remote branch)，你可以定义它们的缩写.
git pull
git pull /home/bob/myrepo master		把Bob的主(master)分支合并到了Alice的当前分支里了
git pull origin feature-D				将本地的feature-D分支更新到最新状态
git push
git push -u origin master				当前分支的内容推送给远程仓库origin的master分支，-u将origin仓库的master分支设置为本地仓库当前分支的upstream，免去将来pull命令再设置参数

git fetch bob							"git pull"前半部分的工作，并不合并
git merge bob/master					检查完修改后,Alice就可以把修改合并到她的主分支中

[log]
git log
git log -p
git log --pretty=short
git log --graph
git log README.md

[stash]
当你正在做一项复杂的工作时, 发现了一个和当前工作不相关但是又很讨厌的bug. 你这时想先修复bug再做手头的工作, 
那么就可以用 git stash 来保存当前的工作状态, 等你修复完bug后,执行'反储藏'(unstash)操作就可以回到之前的工作里
git stash save 'work in progress'		保存'储藏'
git stash pop							弹出'储藏'
git stash list							查看保存的'储藏'

[others]
在大的仓库中, git靠压缩历史信息来节约磁盘和内存空间
git gc									缩操作比较耗时, 最好是在没有其它工作的时候，
git fsck 								运行一些仓库的一致性检查











