### Git Flow  

#### 常用的分支
- production 分支
也就是我们经常使用的master分支,是发布在生产环境的代码.,release(发布)版本,这个分支只能从其他分支合并,**不能**在这个分支**直接修改**

- develop分支
主开发分支,包含所有要发布到下一个版本的代码,这个主要合并与其他分支,比如Feature(功能)分支

- feature分支
这个分支主要是用来开发一个新功能,一旦开发完成,合并回develop分支进入下一个版本

- release分支
当你需要发布一个新release发布版本时,我们基于develop分支创建一个release分支,完成release后,合并到master和develop分支

- hotfix分支
当我们在production发现新的bug时候,需要创建一个hotfix分支,完成hotfix后,我们合并回master和develop分支

![微信截图_20180515174545](https://i.loli.net/2018/05/15/5afaac50db397.png)

协作项目构建流程:
- 首先创建远程库
- 本地clone项目
- 如果项目为空,需要创建项目文件并提交,形成master分支的初始文件,项目为空则没有任何分支
- 此时只有本地master分支和与其对应的remote/master分支(远程库分支)
- 基于master分支,新建develop(开发)分支,在开发分支上新建开发文件并提交,创建remote/develop分支(远程develop分支)
- 基于develop分支,新建feature(功能)分支,在功能分支上开发功能文件并提交,创建remote/feature分支(远程feature分支)
- ...类似分支同上
- 后续开发因为各个分支已经与远程库链接,只需要切换到不同分支,然后进行开发.如切换到feature分支,然后开发完成后merge合并到devlop分支即可.

**综上: 
除了首次构建项目需要gitpush构建远程分支,平时开发只需要切换到不同分支,开发结束后,合并到开发分支再由管理员推送到远程端**

![微信截图_20180515180602](https://i.loli.net/2018/05/15/5afab0ffa1337.png)



### Git Flow如何工作?
###1. master分支 

所有在Master分支上的commit应该tag
打标签参考: https://jingyan.baidu.com/article/5d6edee2f611fa99eadeec01.html

打完标签,记得push时勾选**包括标签**,一起push到服务器
![](https://images.cnblogs.com/cnblogs_com/cnblogsfans/771108/o_git-workflow-release-cycle-1historical.png)

###2. feature分支

feature分支做完后,必须合并到develop分支.
![](https://images.cnblogs.com/cnblogs_com/cnblogsfans/771108/o_git-workflow-release-cycle-2feature.png)

###3. release分支

基于**develop**分支创建,我们可以在这个release分支上测试,修改bug等(**一旦打了release分支之后不要在develop分支上合并新的改动到release分支**)

发布release分支时,合并release到master和develop,同时在master分支上打上tag记住release版本号,然后就可以删除release分支了.

![](https://images.cnblogs.com/cnblogs_com/cnblogsfans/771108/o_git-workflow-release-cycle-3release.png)

###4. 维护分支hotfix

hotfix分支基于**master**分支创建,开发完后需要合并回master和develop分支,同时在master上打一个tag.

![](https://images.cnblogs.com/cnblogs_com/cnblogsfans/771108/o_git-workflow-release-cycle-4maintenance.png)