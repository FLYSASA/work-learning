# 开发流程

### 1 Git commit提交规范

格式:
```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```
示例:
```
fix: 系统设置初始密码优化

1. 添加眼镜图标,可以切换密码明文的展示和隐藏
2. 添加空格的验证规则,密码字符串中不允许出现空格

BUG地址: http//172.56.4.34:81/zentao/bug-view-740.html
```

`<type>(<scope>): <subject>`: 第一行是commit类型,及提交的标题.

几种常用的type:
1. feat: 新增功能
2. fix: 修复bug
3. docs: 仅修改文档,如READEME等
4. style: 在不改变代码逻辑的情况下,仅仅修改空格,格式缩进,逗号等
5. refactor: 代码重构,没有加新功能或修复bug
6. pref: 优化相关,比如提升性能,体验
7. test: 测试用例,包括单元测试,集成测试等
8. chore: 改变构建流程,或者增加依赖库,工具等
9. revert: 回滚到上一个版本



## 2 基本开发流程
核心流程： 从远端仓库git clone到本地，再在本地开发(commit,add等)，最后push代码至远程仓库。

####多人协作模式具体步骤：
1. 选择一个本地目录新建项目文件夹
![微信截图_20180514160701](https://i.loli.net/2018/05/14/5af943c1453f1.png)

2. 将本地项目文件夹变成本地仓库
git bash进入文件夹目录，使用`git init`指令初始化
![微信截图_20180514160903](https://i.loli.net/2018/05/14/5af944181f183.png)


3. 将本地仓库与远程仓库关联起来（前提远程仓库已经存在，若不存在需要先创建）
![微信图片_20180514161147](https://i.loli.net/2018/05/14/5af944d4b1efb.png)

命令行输入：
```
git remote add origin git@bitbucket.org:nietengfei/demo.git
```

4. 如果不使用默认的master分支开发，则要新建分支（例如dev分支），并且该新建的分支要和远程库的相对应的分支建立关联（因为本地库到最后要和远程库同步）
```
git checkout -b dev origin/dev    //新建本地库dev分支对应
远程库dev分支
```
（如果报错，则使用命令`git fetch origin`，然后再次输入`git checkout -b dev origin/dev`）

5. 上面成功以后，此时已经在dev分支上，克隆远程库里的内容
```
git clone git@bitbucket.org:nietengfei/demo.git
```
![微信截图_20180514164408](https://i.loli.net/2018/05/14/5af94c50347d7.png)

克隆完后本地项目文件夹出现远程库文件

6. 对文件进行操作，然后将修改了的文件从工作区添加到本地库的暂存区
`git add .`

7. 将暂存区的文件提交到本地库
`git commit -am '注释'`

8. 将本地库的分支推送到远程库对应的分支，实现同步（注意要把SSH Key添加到GitHub或者bitbucket）
`git push origin dev`

9. 如果push遇到冲突，则将远程库的新内容pull到本地，再修改完冲突后，重做6-8步

10. 如果pull出错no tracking information，则说明本地分支和远程分支的链接关系没有创建，输入如下命令解决，然后再pull就可以了
`git branch --set-upstream-to=origin/dev dev`


### 总结多人协作工作模式要点：
1. 首先，可以试图用`git push origin branch-name`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并
3. 如果合并有冲突，则解决冲突，并在本地提交
4. 没有冲突或者解决掉冲突后，再用`git push origin branch-name`推送就能成功
如果`git pull`提示`“no tracking information”`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream branch-name origin/branch-name`。

![微信截图_20180514174228](https://i.loli.net/2018/05/14/5af95a065ca78.png)
> 
> 常用指令：
git remote -v               //查看远程库信息
git checkout branch-name    //切换分支



### 分支操作实战案例：

1. 在本地创建项目文件夹,并`git init`初始化

![QQ截图20180514222453](https://i.loli.net/2018/05/14/5af99c3f141b3.png)

![QQ截图20180514222535](https://i.loli.net/2018/05/14/5af99c5fa5073.png)

2. 关联远程仓库
```
git remote add origin git@bitbucket.org:nietengfei/test-demo.git
```

3. 仓库账号加入开发者本地公钥账号(方便push等操作)
```
//命令行输入
ssh-keygen

//一路回车,进入.ssh文件夹
cd ~/.ssh

//复制公钥
cat id_rsa.pub

```
![QQ截图20180514225221](https://i.loli.net/2018/05/14/5af9a2a46637d.png)

4.  clone项目到本地
```
git clone git@bitbucket.org:nietengfei/why.git
```

5. 创建本地库dev分支
```
git branch dev
```

6. 切换到dev分支
```
git checkout dev
```

7. 进行项目文件操作(文件修改等)并将dev分支上传至远程库
```
git add .
git commit -am 'ss'
git push origin dev
```
8. 合并分支操作
```
git checkout master    //切换回master分支
git merge dev          //合并dev分支
```

9. 发布上线
```
git push origin master
```


### 冲突
当自己和别人同时改同一个文件的同一个地方,在执行`git pull`时更新本地合并时会出现冲突
解决办法:
1. 修改冲突文件
2. 重新提交
**当提交时,需要`git pull origin 分支名`,来更新本地文件,然后提交更新**

### 常用git指令
1.
``` 
git remote -v  //查看绑定的远程库,以及权限(fetch push等)
```
![QQ截图20180515092847](https://i.loli.net/2018/05/15/5afa37c271267.png)

2.
```
git branch -a  //查看分支
```
![微信截图_20180515093518](https://i.loli.net/2018/05/15/5afa39bf4bd56.png)

3.新建分支后,记得一定要push到远程库
```
git branch branch-name    //新建分支
```
![微信截图_20180515093708](https://i.loli.net/2018/05/15/5afa3a32bfd39.png)

4.
```
git checkout branch-name  //切换分支
```
![QQ截图20180515094059](https://i.loli.net/2018/05/15/5afa3a9de2d51.png)

5. 推送本地分支到远程库
```
git add .
git commit -am ' 注释 '
git push origin branch-name
```
![微信截图_20180515094505](https://i.loli.net/2018/05/15/5afa3b96ebc81.png)

6. 合并分支到主分支
```
git checkout master  //切换到master分支
git merge dev2       //合并分支
```
![QQ截图20180515094921](https://i.loli.net/2018/05/15/5afa3c91f2bec.png)
**合并前记得切换到主分支**

7. 冲突解决,发布
```
git pull  //更新本地分支
git push origin dev
```


8. 删除分支
##### 删除本地分支:
```
//如果需要删除的分支不是当前正在打开的分支，使用branch -d直接删除

git branch -d <branch_name>  

// 如果我们在试图删除一个分支时自己还没转移到另外的分支上，Git就会给出一个警告，并拒绝该删除操作。
如果坚持要删除该分支的话，就需要在命令中使用-D选项。

git branch -D <branch_name>
```

![QQ截图20180515100157](https://i.loli.net/2018/05/15/5afa3ff7c9171.png)

##### 删除远程分支
```
 git push origin --delete dev3
```

![QQ截图20180515102651](https://i.loli.net/2018/05/15/5afa455e3ce7a.png)



### git tortoise使用流程

1. 新建本地项目文件夹

![微信截图_20180515141257](https://i.loli.net/2018/05/15/5afa7a66a5e7b.png)

2. 克隆远程库文件,复制远程库的ssh到url

![微信截图_20180515144438](https://i.loli.net/2018/05/15/5afa81d70f1c8.png)

**克隆文件过程中自动新建了一个本地库**

3. 分支操作


![QQ截图20180515144658](https://i.loli.net/2018/05/15/5afa841e7afc9.png)

切换分支 创建分支操作:

![微信截图_20180515145623](https://i.loli.net/2018/05/15/5afa87e9cd5be.png)


4. 在新分支完成文件变更(修改或者添加功能等),需要commit提交
提交之后才能确定修改文件属于新分支,而不是别的分支,提交之后,切换分支,将看不到新修改的文件.

5. 删除分支

![2](https://i.loli.net/2018/05/15/5afa8b4da81e8.png)

![QQ截图20180515152722](https://i.loli.net/2018/05/15/5afa8bca494f4.png)

6. 合并分支
**前提先切换到主分支,然后实行合并操作**

![QQ截图20180515153512](https://i.loli.net/2018/05/15/5afa8da3eb1bc.png)

![QQ截图20180515153612](https://i.loli.net/2018/05/15/5afa8ddb88f36.png)

选择要合并的分支
![QQ截图20180515153658](https://i.loli.net/2018/05/15/5afa8e10843d3.png)

7. 审查日志,查看代码差异
![QQ截图20180515154829](https://i.loli.net/2018/05/15/5afa90bb4eec3.png)

8. 回滚到某个版本
![QQ截图20180515155941](https://i.loli.net/2018/05/15/5afa935f2db5c.png)

**回滚到某个版本后,拉取远程一下,然后commit即可**


### 注意
> 首次创建仓库,如果仓库是空的,将没有任何分支. 需要**新建项目代码文件提交**以创建初始master分支. 然后完成后续新建分支操作