---
layout: post
title:  "Sublime安装Nodejs的方法和环境配置 —— Windows系统——未完成"
categories: sublime
tags: sublime
author: jakchen
---
* content
{:toc}

[参考链接](http://www.bbsxiaomi.com/software/sublime/33.html)

[参考链接2](http://blog.csdn.net/kafeidou1111/article/details/52522138)

提示：autoprefixer插件需要node.js的支持，所有使用前需要先安装node.js，安装方法请看：[Sublime安装Nodejs的方法和环境配置 —— Windows系统](http://www.bbsxiaomi.com/network/32.html)





步骤1：下载autoprefixer插件 [https://github.com/sindresorhus/sublime-autoprefixer](https://github.com/sindresorhus/sublime-autoprefixer)

步骤2：打开sublime ，选择菜单 Preferences > Browse Packages 将下载的压缩包解压到这里

步骤3：设置快捷键：选择菜单Preferences > Key Bindings – User，可自定义，也可直接ctrl+shift+p选择autoprefixer（如下图）

```
[
    { "keys": ["ctrl+alt+p"], "command": "autoprefixer" }
]
```

![autoprefixer]({{ site.url }}/assets/autofixper.png)

步骤4：设置成功，在css里面写transition:all 2s,会自动编译成 -webkit-transition:all 2s;transition:all 2s；

问题来了，为什么只有-webkit-的前缀呢？其他-moz-，-ms-的前缀呢？
原来sublime的插件autoprefixer默认是没有兼容IE、firefox和opera的，我们可以继续下面的步骤
步骤5：选择菜单：Preferences > Package Settings > Autoprefixer > Settings - User
步骤6：为浏览最新版本添加前缀，市场份额大于0.1%，美国份额>5%，ie6-ie8，火狐版本20以下(其他写法看下面表格)
