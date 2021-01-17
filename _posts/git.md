---
layout: post
title: template page
categories: [cate1, cate2]
description: some word here
keywords: keyword1, keyword2
topmost: true

---



## Git的入门级操作

​		**Created by Hanyz@2021/1/15**



**Git架构图：**

![image-20210115195352931](image-20210115195352931.png)



**设置代理：**

```bash
git config --global http.proxy socks5://127.0.0.1:1080
git config --global https.proxy socks5://127.0.0.1:1080
```

也可以通过编辑config文件：

```bash
vi ~/.gitconfig
```

**取消代理：**

```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```



**别的加速方案：**

> 只需要将链接的www.github.com/改为www.github.com.cnpmjs.org/就可以实现一键式加速



在创建一个新的文件夹后，得设置当前路径为master

```bash
git init
```





**下载代码步骤：**

下载工程文件，在当前目录下下载：

```bash
git clone http/ssh
```

下载后，与云端更新同步，即把云端文件拉到本地：

```bash
git pull origin master
```

如直接 `git pull`，则将所有云端分支都下载 



**clone工程下的单个文件夹**

1、新建仓库并进入文件夹

```bash
git init file_name && cd file_name 
```

2、设置允许克隆子目录

```bash
git config core.sparsecheckout true
```

3、设置要克隆的仓库的子目录路径，注意 ***** 和 **空格**

```bash
echo '文件夹/.../.../...*' >> .git/info/sparse-checkout
```

4、连接远程的工程

```bash
git remote add origin git@github.com:XXXXXXX.git
```

5、下载

```bash
git pull origin master
```



**上传代码步骤：**

1、对文件进行修改

2、查看文件更改情况，红色字体代表进行了更改但还未上传更新

```bash
git status
```

3、将文件送入暂存区

```bash
git add 文件名/文件夹
```

4、提交记录至本地仓库，添加提交解释

```bash
git commit -m "解释"
```

5、上传云端更新

```bash
git push origin branch_name
```

如直接 `git push`，则将所有分支的修改内容都上传 



**删除本地文件并更新云端：**

1、删除文件（鼠标或命令行删不删都行，下面的代码自动进行删除操作了）

```bash
git rm 文件名
```

2、提交并解释

```bash
git commit -m "XXX"
```

3、上传云端更新

```bash
git push origin master
```



**在上传更新前恢复本地误删的文件(分三步)：**

```bash
git status //查看本地对改动的暂存记录
git reset HEAD [ 被删除的文件或文件夹 ] 
git checkout  [ 被删除的文件或文件夹 ]
```





**分支操作：**

查看分支（绿色\* 号代表当前的分支）：

```bash
git branch
```

查看分支详细信息：

```bash
git branch -r //本地的分支信息
git branch -a //云端的分支信息
git branch -v //查看各个分支的提交信息
```

创建分支：

```bash
git branch name
```

删除分支（本地和服务器）：

```bash
git branch -d name // -d是删除干净的分支，-D是强制删除，不管有没有未合并的提交内容
git push origin :name // (分支名前的冒号代表删除)
```

分支的恢复：

```bash
git reflog
git branch <branch_name> <hash_val/commit_id>
```

重命名分支：

```bash
git branch -m <branch_name> newname
```

切换到分支以及切回主分支：

```bash
git checkout name
git checkout master
```

提交分支到服务器（也需要先add和commit操作）：

```bash
git push origin name
```

合并分支更新的内容到主分支（分支内容需要push后才操作）：

```bash
git checkout master
git merge name
```



> 注：在本地切换分支，若不同分支下内容不同，会发现本地的文件内容也会随之切换更改的。



若在云上修改了branch名字，在本地输入相关命令同步：

<img src="image-20210115202720627.png" alt="image-20210115202720627" style="zoom:50%;" />





**查看历史记录：**

```bash
git log
```

![image-20210115203836182](image-20210115203836182.png)

要注意，从上到下的第一个是当前版本，修改提示“文字”的下方才是对应版本的commit id

查看旧版本的代码：

```bash
git checkout commit_id 
```

回到当前的最新版本代码：

```bash
git checkout master
```

**本地回滚到之前的版本：**

```bash
git reset --hard commit_id
```

这时再用“git log”查看版本信息，此时本地的**HEAD**已经指向之前的版本

<img src="image-20210115204613174.png" alt="image-20210115204613174" style="zoom: 33%;" />

此时如果用“git push”去更新，会报错，因为我们本地库HEAD指向的版本比远程库的要旧

**故使用“git push -f”提交更改,强制推上云端，将云端也同步回滚：**

```bash
git push -f
```

