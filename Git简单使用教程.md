# Git使用记录

**1.配置远程仓库**

流程如下：

```
1.在github中注册账号，并且建立一个账户，然后拿到克隆地址
2.在本地生成公钥，导入到个人github账户中
3.在本地中执行git clone url，会在当前文件夹克隆远程仓库
```

**2.常用命令**

```
1.git clone url //克隆远程地址
2.git fetch //拉取master最新代码
3.git fetch origin branch1:branch2 
//拉取远程的branch1分支，用这种方式会在本地仓库新建本地分支branch2，但是并不会自动切换到新建的本地分支branch2
4.git reset xxx
	-- hard:代码恢复到之前的状态，暂存区也没有了
	-- mixed:就将头恢复掉，已经add的暂存区也会丢失掉，工作空间的代码什么的是不变的。
	-- soft:就仅仅将头指针恢复，已经add的暂存区以及工作空间的所有东西都不变。

5.git status //查看git状态，是否有修改文件，未提交文件
6.git add xxx //添加到缓冲区,修改的文件或者新添加的文件
8.git restore file //指定文件撤销修改，回到上一次add状态
7.git branch -r //查看远程地址
8.checkout 通常用来切换分支
9.git checkout -- file //在git restore file之后使用，文件会成为add之前状态
9.1 git checkout -b dev //创建dev分支，并且切换进去 
9.1.1等价于 git branch dev git checkout dev
10.git log file//查看这个文件提交过几个版本，或者能提交几次
11.git reset id file //回退该文件，到id这个版本
12.git reflog //查看提交历史，包括回退
13.git push -u origin master //推送代码到远程分支
14. git pull origin xxx:xxxlocal // 拉去远程分支并且合并
15.git rm -r -n  --cached "*/Makefile" //展示要删除索引的文件
16.git rm -r --cached "*/Makefile" //删除所有为Makefile名的索引
```

git忽略未被跟踪和以被跟踪文件http://t.zoukankan.com/huanghongbo-p-8883094.html

**3.git拉取不了最新代码原因分析**

- 已经拉取过最新代码，然后在与其他分支合并，部分文件冲突然后导致的回退。这样工作区代码不是最新，但是分支的版本已经最新。

- 解决方案：

- ```
  1.回退到合并之前
  ```


**4.协同开发流程**

1. 克隆远程代码
2. 以远程分支为基创建本地分支
3. 开发基于你本地的分支，每次开发时需要pull origin master最新分支，避免落后主分支太远（目前不需要）
4. pull xxx可能会出现文件冲突问题，这个需要挨个文件解决，如果不解决合并会出问题，可以提前备份分支（新建分支）
5. 上传时上传到远程自己的分支，.pro    .pri    .ui     .h    .cpp    .dll文件需要上传，其他文件酌情上传
6. 如果origin master是最新经过合并的，可以直接以master形成新分支

**5.vscode 进行版本控制**

1. 安装插件Git History，Git Graph
2. ![image-20221101180459001](C:/Users/DoYou/AppData/Roaming/Typora/typora-user-images/image-20221101180459001.png)

```
图片中两个文件是存在工作区，点击加号会放在缓存区，需要上传更新的文件就可以放在缓存区，然后可以提交(Commit)到版本区，然后点击同步就会上传到对应的远程分支（与本地分支相同）。图中saDataProcDebug.csv是由程序生成的无用文件，我们可以抛弃它，不添加到缓存区
```

------

![image-20221101181036733](C:/Users/DoYou/AppData/Roaming/Typora/typora-user-images/image-20221101181036733.png)

```
暂存的更改就代表了存入到缓存区，如果都存入到了暂存，这个时候就可以提交了
```

![image-20221101181227735](C:/Users/DoYou/AppData/Roaming/Typora/typora-user-images/image-20221101181227735.png)

```
提交时需要填写这个文本文件，说明做了什么修改，关闭掉这个窗口就会提交成功
```

![image-20221101181334583](C:/Users/DoYou/AppData/Roaming/Typora/typora-user-images/image-20221101181334583.png)

```
点击同步更改，就会上传到远程分支（请确认代码无问题），其中右下角就表明了当前分支和上传到远程分支
```

![image-20221101181509893](C:/Users/DoYou/AppData/Roaming/Typora/typora-user-images/image-20221101181509893.png)

```
graph插件可以清晰看到不同分支，不同用户提交记录，点击可以查看文件修改记录，回退右键点击也比较容易
```

