---
layout: post
title:  "[教程]github for windows"
date:   2017-11-09 20:26:02 +0800
categories: github
tags: github
author: jakchen
---
* content
{:toc}
GitHub 是一个共享虚拟主机服务，用于存放使用Git版本控制的软件代码和内容项目。

GitHub同时提供付费账户和为开源项目提供的免费账户。




除了允许个人和组织创建和访问代码库以外，它也提供了一些方便社会化软件开发的功能，包括允许用户跟踪其他用户、组织、软件库的动态，对软件代码的改动和 bug 提出评论等。

GitHub也提供了图表功能，用于显示开发者们怎样在代码库上工作以及软件的开发活跃程度。

GitHub也提供一个粘贴箱风格的站点Gist，供软件代码库使用的Wiki，以及通过git版本库进行编辑和管理的网页托管功能。

## 一.注册github
登录到[https://github.com][1]，
![注册github]({{ site.url }}/assets/signup.jpg)<br/>
填写相关信息后，点击绿色按钮"sign up for github"注册github账号。

## 二．修改用户名
有时我们需要修改用户名（用户名很重要），登陆https://github.com/，点击右上角头像下面的"Settings"进入设置页面。<br/>
![github设置]({{ site.url }}/assets/settings.jpg)<br/>
点击"Account",点击Change username修改用户名。
![修改用户名]({{ site.url }}/assets/changepassword.jpg)<br/>
注意：修改你的用户名将引起意外结果。所以，请谨慎使用！

## 三．安装GitHub for Windows
下载[GitHub for Windows][2],并安装。

## 四．新建repository，托管代码到GitHub上
一个repository（仓库）可以放一个项目。我们用GitHub for Windows软件新建本地仓库。<br/>

### 1.认识软件
1.在新建之前我们先认识软件。打开GitHub for Windows，登陆自己注册的账号，最左侧是本地仓库，中间是每次更新的Commit(版本)评论，最右侧是仓库的代码，可以查看每次的修改和添加。红色区域代表删除的部分，绿色区域代表添加的区域。
![github for windows]({{ site.url }}/assets/githubforwindow.jpg)<br/>

### 2.软件设置
2.我们点击右上侧的"Opisions"，先对软件进行设置<br/>
![Opions]({{ site.url }}/assets/options.jpg)<br/>
打开Options，根据自己的情况设置Clone path(克隆路径)，也是新建repository(仓库)的本地仓库的默认位置，以后我们建的仓库都会在位置的文件夹里。也可设置Congfigure git，其他默认,然后点击"Save"进行保存。如下图：
![Options]({{ site.url }}/assets/options2.jpg)<br/>

### 3.新建本地repository
3.回到主界面，点击软件上方的"+"，新建一个repository
![新建仓库]({{ site.url }}/assets/ceshi.jpg)<br/>
我们可以看到，新建的仓库是在默认位置的文件夹里并以仓库名为文件夹。<br/>
注：
  - Name不允许单词有空格，建议用“-”连接。<br/>
  - Local path是你默认地址+Name；当然我们也可以点击Browse，选择本地仓库位置。<br/>
  - Git ignore忽略某些文件，项目中经常会生成一些Git系统不需要追踪(track)的文件。典型的是在编译生成过程中产生的文件或是编程器生成的临时备份文件。一般默认。

点击Create respository，我们可以看到如下界面：
![新建仓库]({{ site.url }}/assets/ceshi2.jpg)<br/>
.gitattibutes和.gitignore是默认生成的。本地仓库已建成功。<br/>

### 4.同步到远程仓库
我们点击右上面的Publish Respository，将本地仓库同步到远程仓库。
![发布仓库]({{ site.url }}/assets/publish.jpg)<br/>

添加Description，对仓库的描述。

发布成功后，Publish Respository图标会变成Sync，代表已经同步。

若是新建的仓库位置无代码，我们要把代码复制进来，右击ceshi仓库，
![右击仓库]({{ site.url }}/assets/rightclick.jpg)<br/>
注：
- View on GitHub，是打开网页，即ceshi的远程仓库。
- Open in Exploer，在资源管理器打开仓库
- Open in GIt Shell，是打开命令。可以学习git命令，本文暂不介绍git命令。
- Remove，是将本地仓库移除。但远程仓库并不影响，只是本地有改动不再更新远程库。

点击Open in Explore，进入ceshi本地仓库文件夹，然后将项目代码复制到本地仓库里。（当然若是选择的代码位置作为仓库，那就不需要复制代码了。）<br/>
我们再回到Windows for GitHub里，可以看到中间栏出现了changes，以后每一次本地代码更新都会产生一个changes，
![changes]({{ site.url }}/assets/changes.jpg)<br/>
我们需要评论，提交Commit(版本)，才能将本地仓库的改动同步到远程仓库。具体做法：
1. 填写Summary（更新内容总结）
2. 填写Description（更新的具体描述）
3. 最后点击Commit to master（master是主分支，一般默认），就可以将更新同步至远程仓库了。

### 5.README.md编辑
最后，我们还要为仓库项目添加README.md，用来说明项目或程序。
  两种添加方式：
  1. 一登陆[https://github.com/][1]，选择要添加README.md的仓库，在远程仓库添加README.md，且在线编辑可预览效果；
  2. 二利用编辑器（如sublime）在本地添加README.md，再同步到远程仓库。

若已经有README.md，我们可以在远程仓库文件目录中点击，然后选择进行修改。
README.md并不是随便编写的，它有特定的语法。


 [1]:https://github.com
 [2]:https://desktop.github.com/
