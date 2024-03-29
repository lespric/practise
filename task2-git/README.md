# 任务2-开发辅助工具--GitHub

GitHub是一个免费代码托管平台，可以实现代码储存、想法收集、分支管理、项目看板、网站部署等团队远程协作和项目管理的功能。

## 一、代码储存（Repository）

[GitHub入门基础使用](https://baijiahao.baidu.com/s?id=1608871531156986161&wfr=spider&for=pc)

### 1. 创建存储库

* 在头像旁边点击**十号**，下拉菜单中**New Repository**，进入新的存储库创建页面；
* 在创建页面，输入**存储库名称**、**简要说明**，选择**库的类型**：公开/私有；
* 最后在“使用README初始化此存储库”**打勾**，点击“创建存储库”按钮即可；

### 2. 使用存储库

* **库描述**：在库描述部分，点击**Edit**，可以关联线上展示网站，在其下，点开**主题管理**，可以添加标签方便寻找；  
![库描述](https://github.com/lespric/practise/blob/master/task2-git/img/Edit.png)
* **新建文件**：点击**Create new file**，进入文件编辑页面；  
![新建文件](https://github.com/lespric/practise/blob/master/task2-git/img/create%20new%20file.png)
  * **创建文件夹**：在**Name your file**内，如本地文件夹的路径一样，写入文件夹名后，输入"/"，即可建立文件夹，再输入文件名，包括后缀：  
  **库名/一级文件夹名/二级文件夹名/文件名.后缀**
  * **编辑文件**：在文件主要文本框，写入或复制代码或md文本；
  * **提交文件**：在页面最下面，输入修改的行为及修改的注释，方便查看记录，再选择提交在本主体或新建分支，点击**Commit new file**按钮即可；
* **上传文件**：点击**Upload files**，进入文件上传页面，可以拖动**多个文件**或选择多个文件上传，上传加载完后，再提交文件即可；
  * 注：因无法选择文件夹，建议在新建文件中，新建文件夹时随便建个子文件（库的文件夹没有子文件会消失），再上传本地文件并删除无用子文件；
* **寻找文件**：点击**Find File**，进入文件寻找页面，可以输入文件名或后缀名寻找，用上下方向键加Enter或鼠标打开即可；
* **克隆或下载文件**：点击**Clone or download**，弹出克隆或下载弹窗，选择克隆到桌面版GitHub或下载zip压缩文件到本地，下载的是整个库所有文件；

## 二、团队协作

[Github使用方法(完整版)](https://www.jianshu.com/p/68b9e463333f)

### 1. 建立分支（branch）

* 为了不影响主体内容，需要另外建立分支进行编辑、验证，如同副本文件，方便给团队查看修改情况及修改记录；  
![分支](https://github.com/lespric/practise/blob/master/task2-git/img/branch.png)

* **新建分支**：在存储库页面，点击**branch:master**按钮，弹出下列菜单，在文本框输入分支名字，再点击**Create branch**，即可新建分支；
  * 新建分支后，会把主体的内容克隆进入到分支页面；  
![新建分支](https://github.com/lespric/practise/blob/master/task2-git/img/create%20branch.png)
* **修改分支**：同样点击**branch:master**按钮，弹出的下列菜单有已建分支，点击分支即可进入该分支页面，与使用存储库的操作一样进行修改、新增或删除；

### 2.拉取请求

* 完成分支的编辑后，向团队提出[拉取请求](http://www.sohu.com/a/333116319_100034897)，团队才能查看修改情况，验证通过后，才可以合并到主体内容，从而完成分布式协作；

* **提出请求**：在分支旁边，点击**New pull request**,可以提出新的拉取请求，进入分支与主体或其他分支的比较页面，拉到最下面查看修改内容，绿色表示添加，红色表示删减，确认无误后，在文本框输入修改注释，点击**Create pull request**，即可提出申请；  
![提出请求](https://github.com/lespric/practise/blob/master/task2-git/img/pull%20request.png)
* **查看请求**：可以在分支旁点击**view**，或者在次级导航栏中点击**Pull requests**，再点击对应的请求名称进入查看请求页面，便可以查看谈话、提交、检查、修改情况；
* **合并请求**：在查看请求页面最下面，点击**Merge pull request**，输入合并注释，确认并单击**Confirm merge**，即可完成合并；  
![合并请求](https://github.com/lespric/practise/blob/master/task2-git/img/view%20request.png)
* **删除分支**：同样拉到最下面，点击**Delete branch**，即可删除已合并的分支，也可以恢复删除的分支；  
![删除分支](https://github.com/lespric/practise/blob/master/task2-git/img/delete%20branch.png)

### 3. 想法收集（issue）

* [issue](https://blog.csdn.net/qq_41556318/article/details/86515525)可以用来追踪和收集各种想法如头脑风暴、任务组织、bug问题、测试情况等，尤其开放后可以收集用户的反馈，还可以关联拉取请求进行讨论；

* **创建issue**：在次级导航栏的**Issues**，点击**New issue**，即可进入想法编辑页面；  
![想法](https://github.com/lespric/practise/blob/master/task2-git/img/issue.png)

* **编辑issue**：在文本框输入想法标题、想法描述，还可以在**右侧操作区**中，进行分配给参与者、打上标签、添加到项目、关联到里程碑等操作；
  * **责任人**：Assignees，可以分配给团队成员进行负责，负责在任何指定时间内解决相应的问题；
  * **标签**：labels，给各种不同类型的问题单进行分类，方便筛选和统筹，分出轻重缓急；
  * **项目**：Projects，关联某一项目进程的看板，方便对问题进行可视化进度管理；
  * **里程碑**：Milestones,关联到对应于项目、功能或时间段的问题组，方便把问题集中放在该问题组里面，进行统一解决；
    * **发布测试**：Beta Launch，在你发布项目的 Beta 版之前，包含你需要修复的 bug 文件。这样可以确保你不会漏掉什么；
    * **十月冲刺**：October Sprint，记录你在十月份应该做的问题单文件。相当于一个工作清单，时刻提醒你应该重点完成哪些工作；
    * **重新设计**：Redesign，记录与重新设计项目的问题单文件。可以通过头脑风暴来收集灵感；

* **讨论issue**：通过使用 Issues 的 @memtions 和 references 功能，你可以通知其他的 GitHub 用户和团队，还可以与其他问题单相互连接；
  * **通知**：Notifications,可以设置为web+email，通过浏览别人发的通知来保持issue为最新状态，标注各类通知为已读或屏蔽来快速筛选重要通知；
  * **提及**：@memtions，通过提及某人或某团队所有成员来发送通知，语法为：**/cc @用户名1 @用户名2 或者 /cc @组织名/团队名**，或者直接@；
  * **参考**：References，用来关联其他issue或其他库，通过在其他issue中输入 #issue编号 或者 存储库名#issue编号 来引用相关问题，也可以以 "Fixes"，"Fixed"，"Fix"，"Closes"，"Closed" 或者 "Close" 开头+#issue编号提交来关联分支，分支合并后，这些开头的issue都会关闭；

### 4. 搜索复刻

* **搜索**：在搜索命令输入：**stars:>1000 fork:>1000 html**，可以搜索出点赞数大于1000，复刻数大于1000的html优秀存储库；
* **复刻**：点进他人存储库内，在页面右上角，点击**fork**图标，即可把整个库复刻到自己账号内，如需对其做贡献，以建立分支、拉取请求完成；

## 三、项目看板

[使用Github 的看板功能进行敏捷管理](https://www.xttblog.com/?p=1940)

* **创建新项目**：在次级导航栏的**Projects**，点击**New Project**，进入项目新建页面，输入标题、描述和选择模板即可新建一个项目；
* **使用看板**：基本看板模板为Todo、In progress、Done，即要做的、正在做的、已完成的这三种状态，也可以添加新的列即新的状态，将各个任务或issue进行分类管理；
* **管理卡片**：点击加号可以添加任务卡片，如便利贴写上任务要点，也可以导入issue，在issue页面中关联项目，再在项目中**Add cards**搜索issue卡片，从搜索列表中拖动issue卡片到某一列即可；  
![项目](https://github.com/lespric/practise/blob/master/task2-git/img/project.png)

## 四、网站部署

[在github上发布静态网页](https://www.cnblogs.com/yzkk/p/6360592.html)

* **新建库**：新建一个只放置一个网站的存储库，名字为网站名字；
* **导入文件**：导入index.html等本地文件，不用建立文件夹，都放在主体内；
* **设置网站**：在存储库，次级导航栏的**settings**，找到**GitHub Pages**，在Source的下拉列表选择**master branch**（主体内容），在选择个**theme**（主题），生成的蓝色链接即是部署好的网站链接；
* 注：适用于简单的静态网站，一个存储库只能生成一个网站，生成时只有识别到主体内容有index.html才有内容显示。  
![网站部署](https://github.com/lespric/practise/blob/master/task2-git/img/web.png)
