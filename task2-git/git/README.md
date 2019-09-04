# 任务2———开发辅助工具--Git

## 一、Git

参考：[廖雪峰老师的git教程](https://www.liaoxuefeng.com/wiki/896043488029600)  
[官方网站](https://git-scm.com/)  
[国外网友总结文献](https://gitee.com/liaoxuefeng/learn-java/raw/master/teach/git-cheatsheet.pdf)  
Git是最先进的分布式版本控制系统，可以实现文件命令管理、版本历史记录、远程协作合并等功能，相对于集中式，可以脱离中央服务器及网络，克隆到多个电脑，进行版本更迭；  
![git](https://github.com/lespric/practise/blob/master/task2-git/git/img/git.png)

* 让Git的命令显示不同颜色，可读性更高：`$ git config --global color.ui true`

### 版本库管理

#### 1.创建版本库

* **描述**：如目录，可以记录该目录内的所有文本文件的修改、删除，并且任何时刻都可以追踪历史，或者还原某个时刻修改过的版本，而图片、视频等二进制只能记录文件大小的变化，且最好用统一的编码方式：**UTF-8编码**without BOM，不用记事本记录；
* **step1：建立版本库目录**，注意显示目录的位置路径都不能包含中文，如建立一个名为learngit的版本库；
  * 建立目录：`$ mkdir learngit`
  * 回到上一级目录：`$ cd learngit`
  * 显示目录位置,一般显示在桌面：`$ pwd`

* **step2：目录转化为仓库**，会多一个.git的目录，用来追踪管理版本库，该目录下文件都不要手动修改；
  * 建立一个空仓库：`$ git init`

* **step3：添加文件到库**，手动把文件放在learngit的目录或其子目录下,如添加readme.txt到库：
  * 记录到暂存盘（index），可以反复使用，并可添加多个文件，空格隔开：`$ git add readme1.txt readme2.md`
  * 提交到仓库的主分支（repository-master），并在-m后添加注释：`$ git commit -m "wrote two readme file"`
  * 如添加文件夹，会把文件夹内所有文件都添加：`$ git add img/`

#### 2. 修改版本库

* **查看修改记录**：可以时刻掌握仓库当前的状态，并查看具体的修改内容；
  * 掌握仓库状态，得知是否有未提交的修改版本：`$ git status`
    * 有修改未提交：`Changes not staged for commit`
    * 有修改已提交：`Changes to be committed`
    * 没有任何修改：`nothing to commit, working tree clean`
    * 没有添加过：`Untracked files`
  * 查看具体修改内容，看首个字符：-为修改前，+为修改后：`$ git diff`
    * 也可以单独查看某一文件的修改内容：`$ git diff HEAD -- readme.txt`  
![git diff](https://github.com/lespric/practise/blob/master/task2-git/git/img/git%20diff.png)

* **重新提交到库**：确认无误后，先git add，再git commit -m "注释"，完成再次提交；

#### 3. 版本管理

* **版本回退**：每次修改提交后，git都会以commit这个快照形式进行储存，方便找回；  
![git log](https://github.com/lespric/practise/blob/master/task2-git/git/img/git%20log.png)
  * 查看历史记录，从上往下显示最近到最远，并以时间、注释形式区分版本：`$ git log`
    * 如觉得太多内容，可以只显示一行，版本号+注释：`$ git log --pretty=oneline`
    * 多个文件被修改，版本号也是看时间从最近到最远排序；
  * 返回历史版本，若返回上一个版本，成功会显示版本注释：`$ git reset --hard HEAD^或HEAD~1`
    * 用HEAD^或HEAD~1，其中^的数量或\~后的数字表示往上数第几个版本，HEAD为现所在的版本；
    * 也可以用版本号前七个字符代替HEAD^，可以快速返回任意版本:`$ git reset --hard 8fb8768`
    * 如返回旧版本后，想再返回最新版本，可以查看返回的操作记录来得知HEAD前面的版本号：`$ git reflog`

* **工作区和暂存区**
  * 工作区：workspace，即本地文件，可以看到并可以进行手动修改；
  * 暂存区：index，即.git隐藏目录里的重要内容，记录并暂存多个修改文件，用**git add**添加多个修改文件；
  * 版本库：repository，即git的全部存储内容，长期存储多个分支的最终稳定版本，用**git commit**提交暂存区里所有修改文件；

* **管理修改**：git追踪并管理的是修改即版本，而不是文件；
  * **git commit**只提交暂存区里所有修改文件，只要新修改文件没有用**git add**添加，都不会进入版本库；
  * 由此，先一次性添加所有修改文件到暂存区，再一次性提交所有修改文件到版本库，git其他命令才生效；

* **撤销修改**：将文件回退到上一个版本的内容；
  * 若readme.txt在工作区有修改，但未添加到暂存区：`git checkout -- readme.txt`
  * 若readme.txt在工作区有修改，并添加到暂存区：`git reset HEAD readme.txt`
  * 若readme.txt已把修改提交到版本库：`git reset --hard HEAD^`
  * 若readme.txt已推送到远程仓库，那就需要在返回到上个版本后，重新推送到远程仓库覆盖:`$ git push -u origin master`

* **删除文件**：删除命令与add不同，直接在版本库删除，删除还是先手动删除；
  * 工作区删除，直接手动删除本地文件；
  * 版本库删除，已确定删除文件无误：`git rm readme.txt`
  * 手动删除本地文件有误，要还原工作区文件，在版本库下载最近一次提交的版本：`$ git checkout -- readme.txt`
  * 只能恢复存储库还有存储的版本，未添加或已从版本库删除都不能恢复，且会丢失最近一次在工作区修改的内容；

#### 4. 远程仓库--GitHub

* **加密远程仓库**：为使只有自己的电脑或特定电脑才能修改，git本地仓库与GitHub远程仓库要通过**SSH加密**传输；
![SSH](https://github.com/lespric/practise/blob/master/task2-git/git/img/SSH.png)
  * step1：创建SSH key，无需设置密码，一路回车，默认生成在Users里：`$ ssh-keygen -t rsa -C "youremail@example.com"`
  * step2：复制**id_rsa.pub**文件里所有内容，在生成的路径里，找到id_rsa和id_rsa.pub两个文件，前者是密钥不可泄露，后者是公钥可以复制；
  * step3：在Github部署SSH key，在**setting**里，点击**Deploy keys**中的绿色按钮，标题随便填，复制内容输入到文本框后，点击**add key**即可；
  * step4：第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告，输入**yes**回车通过验证即可，后续不会再出现警告；
  ![Deploy SSH](https://github.com/lespric/practise/blob/master/task2-git/git/img/Deploy%20keys.png)
* **同步远程仓库**：使git本地仓库与GitHub远程仓库(origin)进行远程同步，即可备份本地仓库，又可方便他人查看来协作修改；
  * step1：关联远程仓库：`$ git remote add origin git@github.com:账号名/仓库名.git`
    * 查看远程库信息，即git协议：`git remote -v`
    * 如需更换关联，先删除已关联的远程仓库：`git remote rm origin`
    * 如需关联多个远程库，即关联GitHub又关联码云，要各自命名远程库，则  
    `$ git remote add github git@github.com:账号名/仓库名.git` `$ git remote add gitee git@gitee.com:账号名/仓库名.git`
  * step2：推送本地仓库,关联master分支：`$ git push -u origin master`
  * step3：后续修改再推送：`$ git push origin master`
    * 推送可以指定不同远程库的不同分支，如推送给码云的dev分支：`$ git push gitee dev`

* **下载远程仓库**：把GitHub远程仓库的内容下载到本地，从而在本地修改再推送回去存储；
  * step1：关联远程仓库：`$ git config --global user.name '账号名'` `$ git config --global user.email '注册邮箱'`
  * step2：下载仓库内容：`$ git clone '仓库链接' 或者 $ git clone git@github.com:账号名/仓库名.git`
  * step3：返回上一级目录，方便后续管理操作：`$ git cd 文件夹名`
  * Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快且无需再输入密码,但SSH不能同时在多个库使用；

#### 5. VSCode的辅助

参考：[VSCode使用git](https://www.imooc.com/video/18983)

* **同步到VSCode**：在VSCode打开已下载的仓库内容文件夹，即在左侧显示文件夹内容的目录；
* **修改文件夹内容**：在左侧**PRACTISE**，新增文件或修改文件，每次改动，左侧工具栏第三个图标会显示修改文件的个数；
![VSCode content](https://github.com/lespric/practise/blob/master/task2-git/git/img/VScode%20content.png)
* **添加到暂存盘**：点击第三个图标，按Shift键选择全部修改文件，点+号一次性添加全部；
![VSCode add](https://github.com/lespric/practise/blob/master/task2-git/git/img/VSCode%20add.png)
* **提交到本地仓库**：在**STAGED CHANGES**，按Shift键选择全部修改文件，点击√号，弹出命令面板，再输入**Commit message**回车即可全部提交；
![VSCode commit](https://github.com/lespric/practise/blob/master/task2-git/git/img/VSCode%20commit.png)
* **推送到远程仓库**：在√号旁边的···号，点击**推送**，即可全部推送到远程仓库里，生成文件夹会与本地路径相一致，且会覆盖同名文件；
![VSCode upload](https://github.com/lespric/practise/blob/master/task2-git/git/img/VSCode%20upload.png)

#### 6. 分支管理

* **分支管理过程**
  * HEAD作为指针，指向当前分支，一般为master，且master也有指针，指向当前版本；
  * 当创建新分支，即克隆master的版本到新分支，master的指针保留，HEAD指针指向新分支的版本，其后任何修改都提交到新分支；
  * 直到新分支合并到master，即master的落后指针移到新分支当前版本，删除新分支的指针，HEAD指针回到master即完成；
  * 主分支master作为稳定版本，一般不在其上面工作，则是在新分支dev上工作，并每个成员在dev上再有新分支工作，先合并到dev，再合并到master；
  ![branch](https://github.com/lespric/practise/blob/master/task2-git/git/img/branch.png)

* **创建及合并分支**
  * **创建新分支**，加上-b表示创建并切换：`$ git checkout -b dev`
  * **查看分支**，会列出所有分支，分支前面有 * 号表示所处的分支：`$ git branch`
  * **切换分支**，当新分支的文件修改并提交完后，切回主分支：`$ git checkout master`
  * **合并分支**，把新分支提交的内容，合并指定分支到当前分支：`$ git merge dev`
    * 一般为**Fast forward**模式快速合并，会丢失新分支的信息；
    * 如要保留新分支的信息即合并历史，以便在git status查看合并路线情况：`$ git merge --no-ff -m "注释" dev`
    ![branch merge](https://github.com/lespric/practise/blob/master/task2-git/git/img/branch%20merge.png)
  * **删除分支**，把已合并的分支删除：`$ git branch -d dev`
    * 若dev分支未合并，需要**强行删除**：`$ git branch -D dev`
  * switch也可以代替checkout，如$ git switch -c dev，但输入显示不属于git命令；

* **解决冲突**
  * **查看冲突**，当主分支和新分支都修改文件，合并时产生冲突，可以查看冲突文件：`$ git status`
  * **手动解决**，手动把合并失败的文件，打开编辑为想要的内容，再重新提交；
  * **查看路线**，可以查看合并路线情况，证明合并是否成功：`$ git log --graph --pretty=oneline --abbrev-commit`
    * 注：路线中，(HEAD -> master)指的是本地仓库的指针，(origin/master)指的是远程仓库的指针，皆表示仓库当前所在的版本；
    * 若历史分支的分叉过多，且本地的分叉提交已修改如pull新内容并合并，且**未推送**，想直观地查看线性情况：`$ git rebase`

* **解决bug**
  * **隐藏工作区**，如master出现bug，现有dev分支已修改未提交，则需先隐藏dev分支的工作：`$ git stash`
  * **修复bug**，切回到master，在master新建分支，在bug分支进行编辑修复并提交，合并到master并删除bug分支：`$ git checkout -b issue-101`
  * **查看隐藏工作区**，查看之前隐藏起来的dev工作区在哪：`$ git stash list`
  * **恢复隐藏工作区**，如有多次隐藏，想恢复指定的工作区，则在git stash list显示的：号前的编码，为指定工作区的记录；
    * 恢复，但不删除隐藏工作区信息：`$ git stash apply`
    * 删除stash的内容：`$ git stash drop`
    * 恢复指定工作区，同时删除隐藏工作区信息：`$ git stash pop stash@{0}`
  * **再次提交修复**，翻上面记录查看提交bug修复信息中[]号里面字符值如4c805e2，复制其字符值；
    * 用git checkout切回dev分支，在dev分支重新提交修复：`$ git cherry-pick 4c805e2`

* **多人协作**
  * **下载远程仓库**，在git remote -v中查看远程仓库的git协议后，克隆到本地：`$ git remote add origin git@github.com:账号名/仓库名.git`
  * **修改分支**，在本地仓库新建分支dev，同步远程仓库dev分支，分支名称应一致：`$ git checkout -b dev origin/dev`
  * **推送分支**，修改完后，把本地仓库dev推送到远程仓库dev：`$ git push origin dev`
    * 推送失败，即同样文件有冲突，先设置本地仓库dev与远程仓库dev链接：`$ git branch --set-upstream-to=origin/dev dev`
    * 再抓取远程仓库dev中最新的提交内容，并自动与本地仓库dev合并：`$ git pull`
    * 若合并有冲突，则如解决冲突的过程一样，手动修改解决，再重新提交，最后再推送到远程仓库dev；
      * master分支是主分支，因此要时刻与远程同步；
      * dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
      * bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
      * feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

#### 7. 标签管理

标签(tag)：属于指向commit的指针，用来绑定commit，标签可以用特定名字表示，如"tag v 1.2"，从而找到所绑定的commit；

* **创建标签**，默认打在当前分支的最新提交的commit上，即`$ git tag 版本号 或者 $ git tag -a 版本号 -m "注释"`
  * 如需打在历史版本的commit上，则先查看路线，在路线找到历史commit的编号如f52c633标记为v0.9标签：`$ git tag v0.9 f52c633`
  * 查看标签数量：`$ git tag`
  * 查看v0.9标签的具体信息，是否绑定到正确时间的commit：`$ git show v0.9`
* **推送标签**，推送标签到远程仓库:`$ git push origin v1.0`
  * 一次性推送全部未推送的标签：`$ git push origin --tags`
* **删除标签**，标签默认打在本地仓库，不会自动推送到远程仓库，删除v0.1标签：`$ git tag -d v0.1`
  * 若错误标签已推送到远程仓库，则先删除本地错误标签，再推送删除命令到远程仓库：`$ git push origin :refs/tags/v0.1`

#### 8. 配置Git

* **忽略特殊文件**，在Git工作区的根目录下创建一个特殊的[.gitignore配置文件](https://github.com/github/gitignore)，而.gitignore文件需在文本编辑器另存为来生成，然后把要忽略的文件名填进去，再提交该文件到版本库，Git就会自动忽略这些文件；
![gitignore](https://github.com/lespric/practise/blob/master/task2-git/git/img/gitignore.png)
  * 如想强行添加已忽略的文件App.class：`$ git add -f App.class`
  * 如想查看App.class的名字在.gitignore文件中的位置：`$ git check-ignore -v App.class`
    * 忽略操作系统自动生成的文件，比如缩略图等；
    * 忽略编译生成的中间文件、可执行文件等，比如Java编译产生的.class文件；
    * 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件;

* **配置别名**，一些命令可以用简写来代替，方便以后操作，如把status简写为st：`$ git config --global alias.st status`
  * --global为全局参数，不加则只对当前库有效；
  * 还有别的命令可以简写，很多人都用co表示checkout，ci表示commit，br表示branch；
  * 也可以把unstage代替撤销删除操作：`$ git config --global alias.unstage 'reset HEAD'`
  * 配置一个git last，让其显示最后一次提交信息:`$ git config --global alias.last 'log -1'`
  * 可以把lg代替查看路线操作：`git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"`

* **查看配置文件**，可以查看配置文件生效情况，关联远程库情况，以及配置命令简写：`$ cat .git/config`
  * 配置文件都放在.git文件夹的config文件中，可以记事本打开进行手动修改即可；

* **搭建git服务器**，如想搭建私有库性质的Git远程仓库，需要准备一台运行Linux的机器，强烈推荐用Ubuntu或Debian；
  * step1：注册拥有sudo权限的用户账号；
  * step2：安装git，`$ sudo apt-get install git`
  * step3：创建一个git用户，`$ sudo adduser git`
  * step4：创建证书登录，收集所有需要登录的用户的公钥，即id_rsa.pub文件，把所有公钥导入到/home/git/.ssh/authorized_keys文件里，一行一个；
  * step5：初始化git仓库，先选定一个目录作为Git仓库，假定是/srv/sample.git，在/srv目录下输入命令：`$ sudo git init --bare sample.git`
  * step6：把owner改为git，服务器的git仓库只为共享，没有工作区，`$ sudo chown -R git:git sample.git`
  * step7：禁用Shell登录，通过编辑/etc/passwd文件完成，把git:x:1001:1001:,,,:/home/git:/bin/bash 改为 `git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell`
  * step8：克隆远程仓库，在各自电脑运行，`$ git clone git@server:/srv/sample.git`
  * **管理公钥**：小团队的公钥都放在/home/git/.ssh/authorized_keys文件里，大团队则用Gitosis管理权限；
