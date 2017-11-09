---
layout: post
title:  "window本地搭建Jekyll "
date:   2017-11-04 20:26:02 +0800
categories: jekyll
tags: jekyll
author: jakchen
---
* content
{:toc}
## 事先准备

安装Jekyll很简单，但你得先做好一些准备工作，确保你的系统里有如下配置：




### 1.Ruby<br/>
Ruby是一种纯粹的面向对象编程语言。<br/>
安装Jekyll需要电脑上安装Ruby，安装步骤如下：<br/>
 - Window 系统下，我们可以使用 RailsInstaller 来安装 Ruby 环境，下载地址为：[点击进入下载页面][1]
- 下载 RailsInstaller 之后，双击 railsinstaller-3.2.0 文件，启动 Ruby 安装向导
- 点击 Next，继续向导，记得勾选 Add Ruby executables to your PATH，直到 Ruby 安装程序完成 Ruby 安装为止
- 安装后，通过在命令行中输入  ruby -v 命令来确保一切工作正常（ps：window打开命令行工具:按window键+R键,输入"cmd"后，回车）
- 如果一切工作正常，将会输出所安装的 Ruby 解释器的版本。如果您安装了其他版本，则会显示其他不同的版本。<br/>
安装成功示例：
![安装成功示例]({{ site.url }}/assets/img1.jpg)

### 2. RubyGems

用RubyInstaller安装Ruby之后都附带有Gems，如有需要可以从[这里][2]单独下载RubyGems。

## 使用gem安装Jekyll

打开cmd命令行程序，输入以下命令：<br/>
```ruby
gem install jekyll
```
所有Jekyll的gem依赖包都会被自动安装。
![安装成功示例]({{ site.url }}/assets/img2.jpg)
![安装成功示例]({{ site.url }}/assets/img3.jpg)
检测jekyll是否安装成功，打开cmd命令行程序，输入以下命令：
```ruby
jekyll -v
```
截图如下：
![检测是否安装成功]({{ site.url }}/assets/img4.jpg)
如果需要卸载,输入以下命令：
```ruby
gem uninstall jekyll
```
截图如下：
![卸载jekyll]({{ site.url }}/assets/img5.jpg)

## 使用Jekyll创建博客站点
先进入你想创建博客的目录下，比如我要在D盘创建一个博客，就在命令行输入：
```ruby
D:
#然后回车
```
截图如下：
![进入D盘]({{ site.url }}/assets/img6.jpg)
要进入D盘下的其他盘，如blog文件夹，输入CD--空格--到达的路径(blog)--回车
![卸载jekyll]({{ site.url }}/assets/img.jpg)
然后输入创建博客的命令：
```ruby
jekyll new blog
# 创建一个新的站点
```
这里是将博客创建在了D盘之下，截图如下：
![卸载jekyll]({{ site.url }}/assets/img8.jpg)
控制台可以看见（创建的地址有所不同）New jekyll site installed in D:/blog. 的提示。

## 开启Jekyll 内置服务器
命令行下输入：
```ruby
cd blog
# 然后回车，一定要进入创建的对应blog目录，否则服务无法开启
# 然后再输入下面命令：
jekyll serve
# 然后回车，启动一个地址为http://localhost:4000/的服务器
```
截图如下：
![开启Jekyll 内置服务器]({{ site.url }}/assets/img10.jpg)
Jekyll服务器默认端口是4000，所以打开浏览器输入：[http://localhost:4000][3] 就可以看到生成的博客页面。
截图如下：
![jekyll静态博客页面]({{ site.url }}/assets/img11.jpg)

## 停止Jekyll 内置服务器
关闭命令行窗口，可以停止Jekyll 内置服务器。<br/>或者在命令行窗口输入"Ctrl+C",选择YES然后回车，也可以可以停止Jekyll 内置服务器。

  [1]: http://railsinstaller.org/en
  [2]: https://rubygems.org/pages/download
  [3]:http://localhost:4000
