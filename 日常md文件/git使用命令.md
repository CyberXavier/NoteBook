# git使用命令



## 介绍

* github
* gitee
* 搭建自己的gitlab服务器



## 目录

* [OpenSSL SSL_read: Connection was reset, errno 10054](# errno 10054问题解决)



### （1）系统配置文件与全局用户文件

> ***查看系统配置文件***
>
> ~~~bash
> #linux配置文件在etc目录
> git config --system --list
> ~~~
>
> ***全局用户文件配置***
>
> ~~~bash
> #默认在用户目录下的.gitconfig文件
> git config --global --list
> git config --global user.name "CyberXavier"
> git config --global user.email "1307948605@qq.com"
> ~~~
>
> 



### （2）git常用命令

>~~~bash
>#设置git文件
>git init
>#查看文件提交状态
>git status
>#添加到暂存区
>git add .
>#repository
>git commit -m #-m "Message"
>#上传到远程服务器
>git push
>#带上分支
>git push origin master
>
>~~~
>
>



### （3）忽略文件

~~~bash
#为注释
#在项目主目录下新建".gitignore"文件
*.txt	#忽略所有.txt文件，这样上传就不会被选中
！lab.txt	#！代表除什么以外（除lab.txt以外其他都忽略）
/temp	#代表往上一级忽略，即temp父目录下全部忽略，但不包括temp文件
build/	#忽略build/目录下的所有文件
doc*.txt	#例如：会忽略doc/notes.txt，但不包括doc/server/arch.txt
~~~



### （4）Gitee码云ssh配置

1、设置本机绑定SSH公钥，实现免密码登录！

~~~bash
#打开gitbush 并进入：C:\User\liukun\.ssh
# 生成公钥
ssh-keygen
# 公钥加密算法
ssh-keygen -t rsa
#公钥
ssh-keygen -t rsa -C “your email”
#测试
ssh -T git@github.com
~~~

2.将公钥信息public key添加到码云账户

* 在.ssh文件中找到`id_rsa_pub`打开之后复制并粘贴到账户SSH公钥中

3.使用码云创建自己的账户



### （5）IDE中集成git

1.新建项目，绑定git

* 首先在码云中建一个仓库
* 其次克隆到本地（文件A）
* 在IDE中新建一个项目
* 打开文件A并复制里面的内容粘贴到IDE新建项目下并刷新

2.修改文件，使用IDE操作git

* 添加到暂存区
* commit提交到本地仓库
* push到远程仓库



### （6）说明Git分支

~~~bash
# 列出所有本地分支
git branch

#列出所有远程仓库分支
git branch -r

#新建一个分支，但仍然停留在当前分支
git branch [branch-name]

#新建一个分支，并切换到当前分支
git checkout -b [branch]

#合并指定分支到当前分支
git merge [branch]	
#如果同一个文件在合并分支时都被修改了则会引起冲突：修改冲突后文件重新提交（选择保留谁的代码）

#删除分支
git branch -d [branch-name]

#删除远程分支
git push origin --delete [branch-name]
git branch -dr [remote/branch]
~~~



### errno 10054问题解决

**Solution1: （原因）自己配置的用户名，邮箱可能输入错误了。**
查看用户名，邮箱

```bash
git config user.name
git config user.email</code>
```

修改，用户名，邮箱

```bash
git config --global user.name "xxx"
git config --global user.email "xxx"
```

移除仓库，重新添加

```bash
git remote rm origin
git remote add origin https://github.com/XXX
```

**Solution2: 修改解除SSL认证。**
在Git Bash中输入以下命令：

```bash
git config --global http.sslVerify "false"
```

**Solution3: （原因）文件太大了。**
改为500MB，在Git Bash中输入以下命令：

```bash
git config http.postBuffer 5242880003
```

**Solution4: （原因）更新DNS缓存。**
在cmd中输入以下命令：

```bash
ipconfig /flushdns
```

