## jira开发任务管理

- JIRA是一款优秀的问题跟踪及管理工具,JIRA采用J2EE技术,能够跨平台部署. 被广泛运用于缺陷跟踪,客户服务,需求收集,流程审批,任务跟踪,项目跟踪和敏捷管理等工作领域.

- JIRA项目敏捷流程:epic项目计划->Userstory需求->Task任务->Bug缺陷

![图片1](https://i.loli.net/2018/05/16/5afba9a8646f1.png)



#### JIRA简介

- JIRA 不支持代码管理功能，Story开发创建代码分支是通过集成**Bitbucket**（采用Mercurial和Git作为分布式版本控制系统）实现。

- JIRA不支持测试计划、用例管理功能，需要通过**TestLink**工具实现

![图片2](https://i.loli.net/2018/05/16/5afbd19d872db.png)

#### TestLink简介

**TestLink**是一款开源的测试管理工具，主要用于进行测试过程的管理，通过使用TestLink提供的功能，可以将测试过程从测试需求、测试设计、到测试执行完整的管理起来，同时，它还提供了好多种测试结果的统计和分析，使我们能够简单的开始测试工作和分析测试结果。


### 使用流程

记得使用IE打开,不然会出现服务器拒绝的问题.

##### 1.JIRA-用户创建

用户创建有两种方式有用户注册、系统管理员创建，推荐使用注册方式。

![图片3](https://i.loli.net/2018/05/16/5afbd41c202b6.png)

![图片4](https://i.loli.net/2018/05/16/5afbd4468671b.png)


##### 2.Bitbucket-添加用户

![图片5](https://i.loli.net/2018/05/16/5afbd4f53ae56.png)


##### 3.JIRA-开发任务跟踪-Story&任务认领
- **开发人员自行认领Story或子任务，将Story或子任务分配给自己**
- **开发经理将Story或子任务分配给开发人员**

![图片6](https://i.loli.net/2018/05/16/5afbd8bb575c0.png)

##### 4.JIRA-开发任务跟踪-登记工作日志

- 开发人员开发过程中或开发完成,填写工作日志,更新耗费时间,并预估剩余工时

![图片7](https://i.loli.net/2018/05/16/5afbde7f3684d.png)


![图片8](https://i.loli.net/2018/05/16/5afbdf6433f16.png)


##### 5.JIRA-缺陷(故障)提交

- 测试人员/开发人员执行测试用例发现BUG后,在JIRA中提交故障
- 开发人员自测发现BUG后,在JIRA中提交故障

![图片9](https://i.loli.net/2018/05/16/5afbe1b472f25.png)

![图片10](https://i.loli.net/2018/05/16/5afbe1c625ac6.png)

![图片11](https://i.loli.net/2018/05/16/5afbe1e8d5d63.png)

![图片12](https://i.loli.net/2018/05/16/5afbe21084fe9.png)



###### Bitbucket-新建存储库

```
你有一个空的存储库
To get started you will need to run these commands in your terminal.
第一次使用Git？ 学习基本的Git命令

第一次配置Git
git config --global user.name "聂腾飞"
git config --global user.email "18565889307@163.com"

使用您的存储库
我只想克隆这个存储库
如果要简单地克隆此空存储库，请在终端中运行此命令。

git clone http://%E8%81%82%E8%85%BE%E9%A3%9E@172.56.2.105:8090/scm/test/demo.git

我的代码已经准备好推送
如果你代码已经准备好推送到仓库，请在终端中执行该命令
cd existing-project
git init
git add --all
git commit -m "Initial Commit"
git remote add origin http://%E8%81%82%E8%85%BE%E9%A3%9E@172.56.2.105:8090/scm/test/demo.git
git push -u origin master

我的代码已经由Git跟踪
如果你的代码已经由Git跟踪，然后设置这个仓库作为你的“origin”推送。
cd existing-project
git remote set-url origin http://%E8%81%82%E8%85%BE%E9%A3%9E@172.56.2.105:8090/scm/test/demo.git
git push -u origin master
```


#### 总结JIRA + TestLink使用总结

![图片13](https://i.loli.net/2018/05/16/5afbe402928a6.png)

![图片14](https://i.loli.net/2018/05/16/5afbe4426ac61.png)


1. 开发人员认领story或者任务(在仪表板中)
2. 任务开始时,将任务状态更新为处理中
3. 编写代码,将代码提交到相应的**代码分支**,登记工作日志
4. 代码编写完成后,完成自测试,更新任务状态为等待测试
5. 开发经理管控story开发进度,合并需送测的代码分支,做好送检准备,通知测试人员测试
6. 测试人员在JIRA提交BUG,将BUG与测试用例关联
7. 开发人员修改BUG,更改BUG状态
8. 测试人员回归验证BUG,更改BUG状态,标记验证结果,更新任务状态

> story或任务完成后,要填写实际工时
> story或任务要分配给相应的人员后开始处理
> 只处理分配给自己的问题(包括story,任务,故障)

