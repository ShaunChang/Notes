# 1 git和subversion的区别。最详细易懂！！！！！！！！！！！




# 2 git config --global

    -git config --global user.name "<Your-Full-Name>"：
    git config --global user.email "<your-eamil-address>"
    -为什么要配置用户名和邮箱
    -最后那个是指定默认编辑器 code就是vstudiocode的命令

# 3 查看现在的config
    -git config --global --list
    -git config --local --list：
    -如果不写local 和global 就会列出所有的config：local+global

# 4 编辑config
    -git config --edit

# 5 如何使用多个git cofig
    -在对应文件下使用上面命令即可 只对这个project生效 注意不能写--global

# 6 git init
    -初始化本地仓库 :隐藏的.git文件夹

# 7 git add
    -使用后就进入git管理范围 等于告诉git这几个文件要被记录 就是说下一步commit
    阶段会snapshot这几个文件 

# 8 git commit
    -记录到自己的版本哭
    -记录后晴空stage

# 9 git rm --cached 文件名：把文件从stage取出

# 10 git stash :把目前修改的所有都暂时存起来 然后距离上次提交写过的东西都会删除 但是内容不在暂存区！！！
    怎么存
    git stash save 'stash name'
    怎么查看
    git stash list
    怎么取出来
    git stash apply stash编号（不会删stash里的文件）
    git stash pop（会删除stash里最后一个文件）
    -查看stash list：git stash list

# 11 撤销命令
    -git checkout . 撤销所有改变：
    -git clean --force 清理所有文件夹：
    -git revert 版本号 用一个新的commit对某次历史记录进行回滚：
    和git checkout .的区别是che会将指针移动到上次那个提交点 revert会创建新提交
    -git reset 版本id  直接删除id以前的所有版本号  不会有记录


# 12 branch
    -不同branch内容完全独立 commit也完全独立
    -创建branch   git checkout -b name 
    -切换branch   git checkout name
    -删除branch  git branch -d name
    -branch 命名规范：<type>/<ticket-number>-<title>
    eg: feat(干嘛的branch)/JR-101-create-header-for-home
    -git merge branchname 合并branch: 
    -创建branch git branch xxx
    -branch创建后需要publish才能在remote显示: 
    创建本地分支且同步远程总体步骤:
    git branch xx
    git checkout xx
    git push --set--upstream xx
    -branch改名： git branch -m master main
    git branch 失效怎么办
    必须使用git init命令创建仓库，执行git add . 和git commit（提交成功后）,再使用git branch命令，才显示出本地分支。


# 13 log图形化界面
    git lon --all --decorate --online --graph


# 14 merge 
    -merge分本地和远程merge：本地就是merge 完全看个人随便取舍   远程是pr 要经过很多审查
    -冲突：手动修改或不解决（选择一个）


# 15 连接远程仓库
    -如果是clone的就会自动建立remote链接



# 16 your branch is ahead of 'origin/main' by 1 commit: 代表可以push了
    你的本地仓库比远程多一个提交 此处的origin值得就是远程仓库


# 17 fetch
    -拿到远程仓库信息，但是不做pull或push

# 18 your branch is behind of 'origin/main' by 1 commit: 代表可以pull了

# 19 rebase在实际开发中取代mege  因为最后的图形化界面是一根线 用法完全一样  缺点：看不出来提交先后顺序

    注意
    不要在公共分支上用rebase  正常用法应该是
    1.你先checkout到master分支  
    2. 你pull最新的master代码  因为主分支是所有人都提交维护的一个分支 会变嘛 你自己的分支你自己写 不会变嘛 
    3 你更新后在切到你的分支 
    4 你在你的分支上rebase主分支 eg：git rebase master 这个时候你的分支上就会有完整的master最新代码加你自己的代码（就是把自己的代码加到了最新最去的master分支上）
    5 你回到主分支
    6 你在主分支上吧你分支merge过来

# 20 .gitIgnore：自己创建
    -里面的文件都不需要追踪



# 21 push
    -force push可以用在自己的branch'上 不怕冲突 直接用自己的branch覆盖重写远程的相应 的branch



# 22 git flow
    -master 和 development分支保持稳定
    -develop 在development分支创建新的临时分支 弄好后合并到deve和master
    -hotfix在msster分支创建新的分支 弄好后合并号deve和master
    -release在development分支创建release分支 弄好后合并到deve和master


# 23 git remote
    -git remote add origin [url]
    -git remote rm origin
    -git remote origin set-url [url]


# 24 删除分支 git branch -d    【branchname】  
    -如果提示没有merge完 不能删除 不行就用D 一定能删除


#  25 切换分支 git checkout [branchname]
    -每天第一件事就是去dev pull代码  看有没有更新

# 25 本地分支关联远程分支
    -git fetch 吧分支拉下来
    -git branch –set-upstream 本地新建分支名 origin/远程分支名

# 26 git log 日志
    -git log: 查看所有commits
    -git reflog: 查看包括版本回退的所有commits

# 27 git reset
    -git reset HEAD^ 回退所有内容到上一个版本，内容回到工作区 保留最后一个commit
    -git rest soft HEAD^1 回退所有内容到上一个版本，内容回到暂存区  保留最后一个commit
    -git reset --hard HEAD^1 回退内容到上一个版本  最后一个commit也消失 这个与前两个的区别是前两个用完后无论你回到暂存区还是工作区 你刚新加的代码都在 hard用了后所有的东西都不复存在 包括提交
    -git reaset commid 会退到指定版本


# 28 本地远程关联
    -查看关联的远程仓库   
    git remote -v
    -关联远程仓库 
    $ git remote add <自定义仓库名> <仓库地址>
    -拉取远程仓库分支信息
    git fetch <仓库名>
    或者
    $ git remote update // 更新所有仓库，后面可以跟 --prune，表示清理本地仓库中失效的远程分支，注意，不是本地自己创建的分支
    -关联远程分支 这一步弄完后直接可以pull push
    git branch --set-upstream-to=<仓库名>/<分支名>
    -查看分支关联情况
    git branch -vv
    -没有关联远程分支
    $ git push --set-upstream <仓库名> <本地分支名>
    或者
    $ git push <仓库名> <本地分支名>:<想要创建的远程分支名> // 如果要删除远程分支，删除冒号前面的分支名即可：git push <仓库名> :<想要删除的远程分支名>


# 29 rebase 

    为什么在主分支不能用rebase
    因为在主分支用rebase就等于你原本要把人家新的提交合并过来，新的嘛，肯定要放在前面，你一个rebase，线是直了，你把人家原本是新的东西压在下面了。别人看到的就纯粹是错误记录
    为什么rebase完了后要切换到主分支上再merge一次？？
    你在开发分支上rebase相当于把没用的创建分支（就是从主分支上拉出来的那个杠杠）和commit节点删除 留下干货嫁接在master分支上。此时你的开发分支什么都没变。只不过基地变了。你以前在土地上，现在脚下踩着master而已。
    rebase前：

    rebase后。此时你的开发分支享有整个commit。你是最亮的宝宝


    为什么切换到主分支还要再merge一次呢？看灰色的那个小箭头！！因为终归还是要让主分支要最新最全的。此时吧主分支也更新到和你的开发分支一样新一样全（其实就是一个线）。让主分支也成为最美的宝宝。

    如果在主分支用rebase会这样？会jb颠倒顺序，这时你用merge的意思是你的master要把开发分支作为基地了！！！把人家新的踩脚底下，你小子冲前面冒充新人！

# 30 git如何使用reset删除远程仓库的提交
    1. 使用git log查看提交记录，记住需要删除的commit id，
    2. 使用git reset --hard <commit_id> 来回滚到指定的commit，并删除commit之后的所有改动，
    3. 使用git push origin <branch_name> -f 将本地仓库的改动强制推送到远程仓库，以覆盖远程仓库的改动。