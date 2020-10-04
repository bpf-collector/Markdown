<!--
 * @Author       : bpf
 * @Date         : 2020-09-22 15:41:19
 * @Description  : 学习使用GitHub
 * @LastEditTime : 2020-10-04 16:14:05
-->

# <font face="微软雅黑" size=6> **[GitHub 使用](https://www.liaoxuefeng.com/wiki/896043488029600)** </font>

## 1. Git 安装

### 1.1 Linux

> Debian 或 Ubuntu: `sudo apt-get install git`

### 1.2 Mac OS

> + 法一：安装`homebrew`，再通过`homebrew`安装Git
> + 法二：从AppStore安装`Xcode`，其集成了Git，不过默认没有安装，你需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，选择“Command Line Tools”，点“Install”就可以完成安装了。

### 1.3 Windows

> 直接在Git官网下载安装

## 2. 初始化

``` bash
git config [--global] user.name "Your Name"
git config [--global] user.email "email@example.com"
```

> `--global`参数表示这台机器上所有的Git仓库都会使用这个配置

## 3. 创建版本库

### 3.1 创建空目录

``` bash
mkdir learngit
cd learngit
```

### 3.2 初始化为仓库

``` bash
git init
```

> + 在当前目录会多一个`.git`目录，这个目录是Git来`跟踪管理版本库`的
> + Git只能跟踪纯文本方式编写的文件，对于二进制文件无法跟踪，而Microsoft中`Word`文件就是二进制格式。
> + 强烈建议使用标准的`UTF-8`编码格式
> + Windows自带的`笔记本`编写的UTF-8编码文件，其在每个文件开添加了`0xefbbbf`(16进制)，因此常会遇到很多不可思议的问题。

### 3.3 添加文件

``` git
git add <file>
```

### 3.4 提交修改

``` git
git commit [-m <comment>]
```

### 3.5 查看结果

``` git
git status
```

### 3.6 查看修改的内容

``` git
git diff <file>
```

## 4. 版本回退

### 4.1 查看历史记录

``` git
git log [--pretty=oneline]
```

> + 参数说明
>
> > `--pretty=oneline`可以简略显示信息
> > `1094...`是版本号(commit id)
> > 版本号右侧的`HEAD表示当前为此版本
>
> + 例子
>
>> $ git log
>>
>> commit 1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master)
>>
>> Author: Michael Liao <askxuefeng@gmail.com>
>>
>> Date:   Fri May 18 21:06:15 2018 +0800
>>
>> append GPL

### 4.2 回退版本

``` git
git reset --hard <commit id>
```

> `commit id`为版本号，返回上一版本用`HEAD^`，上上版本用`HEAD^^`，前100个版本用`HEAD~100`。

### 4.3 查看历史命令

``` git
git reflog
```

## 5. 文件修改与删除

### 5.1 工作区、缓存区、版本库

![廖雪峰](https://www.liaoxuefeng.com/files/attachments/919020074026336/0)

![廖雪峰](https://www.liaoxuefeng.com/files/attachments/919020100829536/0)

### 5.2 查看工作区与版本库的区别

``` git
git diff HEAD -- <file>
```

### 5.3 撤销修改

``` git
git checkout -- <file>
```

> 此命令可丢弃工作区的修改，回到最近一次`git commit`或`git add`的状态。

### 5.4 删除文件

> + 删除文件
>
> > 工作区删除文件: `rm <file>`
> >
> > 版本库删除文件: `git rm <file>`
> >
> > 提交删除: `git commit`
>
> + 误删文件
>
> > 恢复文件: `git checkout -- <file>`

## 6. 远程仓库

### 6.1 创建SSH Key

> + 在用户主目录下，看看有没有`.ssh`目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），*创建SSH Key*：
>
> + `.ssh目录`中的`id_rsa`和`id_rsa.pub`两个文件是`SSH Key`的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

```git
ssh-keygen -t rsa -C "youremail@example.com"
```

### 6.2 登陆Git Hub

> 打开`Account settings`，`SSH Keys`页面，然后，点`Add SSH Key`，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容。
![廖雪峰](https://www.liaoxuefeng.com/files/attachments/919021379029408/0)

### 6.3 连接远程仓库

> + 创建仓库`learngit`
>
> + 本地仓库与远程仓库关联
>
> `git remote add origin git@github.com:<账户名>/learngit.git`
>
> > 关联后，`origin`就是远程库的名字
>
> 推送内容到远程库
>
> `git push -u origin master`
>
> > `-u`参数把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令
>
> 【**注意**】：
>
> > + 一台电脑上也是可以克隆多个版本库的，只要不在同一个目录下。
> >
> > + 本地Git仓库和GitHub仓库之间的传输是通过`SSH加密`的。

### 6.4 克隆仓库

``` git
git clone git@github.com:<账户名>/<仓库名>.git
```
