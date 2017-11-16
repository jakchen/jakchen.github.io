---
layout: post
title:  "sublime text 3使用介绍"
categories: sublime
tags: sublime
author: jakchen
---
* content
{:toc}
## sublime 编辑器的特点

 1.无学习难度<br/>
 2.支持多点编辑，按`Ctrl`<br/>
 3.package control：强大的包的管理功能<br/>
 4.闪电般的操作：查找字符串<br/>
 5.深度可定制<br/>
 6.快速文件切换；`Ctrl+P+文件名`<br/>
 7.命名面板：`Ctrl+Shift+P`<br/>
 8.社区活跃<br/>




**多使用快捷键：ps快捷键搜索<br/>
key bindings-default：快捷键默认设置<br/>
key bindings-user：快捷键用户设置**

## 1.汉化

下载一下 Sublime 的汉化包。并将我们的汉化包直接拖进 `Installed Packages` 文件夹即可。
### 用户配置：
```
{
"font_size": 12,
//字体大小
"highlight_line": true,
//高亮编辑中的那一行
"ignored_packages":
[
"Vintage"
],
//忽视vim模式
//"word_wrap": false,
//自动换行
"bold_folder_labels": true,
//加粗文件夹名称
"save_on_focus_lost": true,
//焦点丢失后自动保存
"tab_size": 2,
"translate_tabs_to_spaces": true,
//Tab转换
"trim_trailing_white_space_on_save": true,
//保存时去掉每一行文本最后面的空格
//"theme": "Seti_orig.sublime-theme",
//使用seti_ui
}
```
### 快捷键设置：
```
[
  { "keys": ["ctrl+shift+`"], "command": "show_panel", "args": {"panel": "console", "toggle": true} },
  //对齐
    //{ "keys": ["f5"], "command": "open_in_browser" },
    //在默认浏览器中打开文件
   {"keys": ["ctrl+shift+i"],"command": "htmlprettify"},

   {  "keys": ["f5"],
    "command": "side_bar_files_open_with", "args": {"application": "D:\\Program Files\\SogouExplorer\\SogouExplorer.exe", "extensions": ".*", "paths": []}
   },
   //在搜狗浏览器中打开
   {  "keys": ["f4"],
    "command": "side_bar_files_open_with", "args": {"application": "C:\\Program Files\\Mozilla Firefox\\firefox.exe", "extensions": ".*", "paths": []}
   },
   //在火狐中打开
    {  "keys": ["f3"],
    "command": "side_bar_files_open_with", "args": {"application": "C:\\Program Files\\Google\\Chrome\\Application\\chrome.exe", "extensions": ".*", "paths": []}
   },
   //在谷歌中打开
   {  "keys": ["f1"],
    "command": "side_bar_files_open_with", "args": {"application": "C:\\Program Files\\Internet Explorer\\iexplore.exe", "extensions": ".*", "paths": []}
   },
   //在IE中打开
]
```

## 2.插件安装

关于 Sublime Text 的插件安装基本上分为两种方法：
 1. 第一种是直接找到 Sublime Text 的插件目录，之后将自己的插件直接拖进去即可。
 2. 第二种方法则是去通过安装插件的方式来安装。而安装插件之前，我们首先需要来安装一个插件管理工具 **Package Control**。

### 安装 Package Control 插件管理工具
 首先打开我们 Sublime Text 的控制台。快捷键 `ctrl +shift+ ~`
 之后我们需要将对应的版本输入进我们的控制台。
#### 安装代码
 ````
import urllib.request,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
````
将其输入进控制台，并单击回车。
等待安装完成后，完全退出 Sublime Text 并重新打开。

这时候我们打开控制面板。
window ： `ctrl + shift + p`
这时候输入 `install` 去呼出插件安装面板。

### 插件备份
只需将`Packages`（Preferences > Browse Packages）中内容拷贝一份，同步云端即可；每有所需只要下载下来，替换掉原Packages下内容就好。

### 插件卸载
打开命令面板，输入`remove package`，下面会有提示，直接点击或者输入后回车。

## 3.插件推荐
### Emmet
 - 功能：编码快捷键，前端必备
 - 简介：Emmet作为zen coding的升级版，对于前端来说，可是必备插件，如果你对它还不太熟悉，可以在其官网上看下具体的演示视频。
[使用教程](http://bubkoo.com/2014/01/04/emmet-a-toolkit-for-improving-html-css-workflow/)

### html-css-jsprettify
 - 功能：对Html，css，js文件进行格式化
 - 简介：代替了JsFormat 和 CSSFormat
 - 使用：快捷键Windows: ctrl+shift+i
 - 快捷键配置：在Preferences / Key Bindings – User加上代码（数组内）
{"keys": ["ctrl+shift+i"],"command": "htmlprettify"},

### CSSComb
 - 功能：用来给CSS属性进行排序的格式化（处女座必备）
 - 简介：按一定的顺序排列
 - 使用：到https://github.com/csscomb/sublime-csscomb下载插件包，放到sublime text文件夹的\Data\Packages\User目录里
 - 快捷键：ctrl+shift+c

### ColorHighlighter
 - 功能：方便调色
 - 简介：它可以展示你所选择的颜色代码（像“#FFFFFF”, “rgb(255,255,255)”, “white”）的真正颜色。同时它还包含一个颜色选择器让你可以方便地更改颜色。
 - 使用：快捷键Windows: ctrl+shift+w
 - 快捷键配置：在Preferences / Key Bindings – User加上代码（数组内）
{ "keys": ["ctrl+shift+w"],"command": "color_picker","context": [{"key": "color_highlighter.color_picker"}]},

### Trailing spaces
 - 功能：检测并一键去除代码中多余的空格
 - 简介：还在纠结代码中有多余的空格而显得代码不规范？或是有处女座情节？次插件帮你实现发现多余空格、一键删除空格、保存时自动删除多余空格，让你的代码规范清爽起来
 - 使用：安装插件并重启，即可自动提示多余空格。一键删除多余空格：CTRL+SHITF+T（需配置），更多配置请点击标题。
 - 快捷键配置：在Preferences / Key Bindings – User加上代码（数组内）{ "keys": ["ctrl+shift+t"], "command": "delete_trailing_spaces" },

### auto-save
 - 功能：自动保存文件
 - 简介：为保存提供了方便
 - 使用：默认是不会自动保存，按快捷键Ctrl+Shift+S开启。
 - 快捷键配置方法：首选项-快捷键设置，在数组内添加{ "keys": ["ctrl+shift+s"], "command": "auto_save" },如需自动启用，首选项-插件-auto-save---settings-usre粘帖一下配置
{
"auto_save_on_modified": true,
"auto_save_delay_in_seconds": 10,
"auto_save_all_files": true,
"auto_save_current_file": "",
"auto_save_backup": false,
"auto_save_backup_suffix": "autosave"
}

### view in browser
 - 功能：通过默认浏览器打开文件
 - 简介：方便打开浏览器检查编译效果
 - 使用：快捷键配置方法：首选项-快捷键设置，在数组内添加快捷键：F12{ "keys": ["f12"], "command": "open_in_browser" },

### autoprefixer(下载超慢)
 - 功能：CSS添加私有前缀
 - 简介：CSS还未标准化，所以要给各大浏览器一个前缀以解决兼容问题
 - 使用：快捷键配置方法：首选项-快捷键设置，在数组内添加{ "keys": ["ctrl+shift+enter"], "command": "autoprefixer" },
 - 快捷键：ctrl+shift+enter

### CSS Extended Completions：
 - 功能：关联CSS文件，智能提示css文件中的类名，非常好用

### JavaScript Completions
 - 功能：支持javascript原生语法提示，妈妈再也不用担心我输入document.getElementById(id)

### jQuery
 - 功能：jQ函数提示
 - 简介：快捷输入jQ函数，是偷懒的好方法

### AutoFileName
 - 功能：快捷输入文件名
 - 简介：自动完成文件名的输入，如图片选取
 - 使用：输入”/”即可看到相对于本项目文件夹的其他文件

### SublimeLinter
 - 功能：代码检查
 - 简介：支持JavaScript、CSS、HTML、Java、PHP、Python、Ruby等十多种开发语言
 - 使用：需要配置相应语言的环境，要检查JavaScript代码需要安装node.js，检查PHP代码需要安装PHP并配置环境等。

### SideBarEnhancements
 - 功能：扩充边栏菜单的功能
 - 简介：包括在当前工程文件夹中新建文件，移动文件或文件夹，产生文件或文件夹的副本，在新窗口或浏览器中打开，刷新等。

### Bracket Highlighter
- 功能：代码匹配
- 简介：可匹配[], (), {}, “”, ”, <tag></tag>，高亮标记，便于查看起始和结束标记

### Monokai Extended
- 功能：主题
- 简介：如果你喜欢 Soda Dark 和 Monokai，我建议你使用 Monokai Extended
- 使用：首选项-> 配色方案 -> User -> Monokai Extended

### SublimeTmpl 快速生成文件模板
SublimeTmpl 能新建 html、css、javascript、php、python、ruby 六种类型的文件模板，所有的文件模板都在插件目录的templates文件夹里，可以自定义编辑文件模板。
SublimeTmpl默认的快捷键：
ctrl+alt+h → html
ctrl+alt+j → javascript
ctrl+alt+c → css
ctrl+alt+p → php
ctrl+alt+r → ruby
ctrl+alt+shift+p → python
如果想要新建其他类型的文件模板的话，先自定义文件模板方在 templates 文件夹里，再分别打开 Default (Windows).sublime-keymap、Default.sublime-commands、Main.sublime-menu、SublimeTmpl.sublime-settings 这四个文件照着里面的格式自定义想要新建的类型~

插件下载：https://github.com/kairyou/SublimeTmpl
### AllAutocomplete
Sublime Tex中的经典自动补全，只适用于当前文件。AllAutocomplete在当前窗口的所有打开文件中搜索可以大大简化开发过程。还有CodeIntel，具体化了IDE的功能，并为若干语言带来了“代码智能”，这些语言包括：JavaScript，Mason，XBL，XUL，RHTML，SCSS，Python，HTML，Ruby，Python3，XML，Sass，XSLT，Django，HTML5，Perl，CSS，Twig，Less，Smarty，Node.js，Tcl，TemplateToolkit，PHP。
## Sublime Text快捷键：
```
Ctrl+Shift+P：打开命令面板
Ctrl+P：搜索项目中的文件
Ctrl+G：跳转到第几行
Ctrl+W：关闭当前打开文件
Ctrl+Shift+W：关闭所有打开文件
Ctrl+Shift+V：粘贴并格式化
Ctrl+D：选择单词，重复可增加选择下一个相同的单词
Ctrl+L：选择行，重复可依次增加选择下一行
Ctrl+Shift+L：选择多行
Ctrl+Shift+Enter：在当前行前插入新行
Ctrl+X：删除当前行
Ctrl+M：跳转到对应括号
Ctrl+U：软撤销，撤销光标位置
Ctrl+J：选择标签内容
Ctrl+F：查找内容
Ctrl+Shift+F：查找并替换
Ctrl+H：替换
Ctrl+R：前往 method
Ctrl+N：新建窗口
Ctrl+K+B：开关侧栏
Ctrl+Shift+M：选中当前括号内容，重复可选着括号本身
Ctrl+F2：设置/删除标记
Ctrl+/：注释当前行
Ctrl+Shift+/：当前位置插入注释
Ctrl+Alt+/：块注释，并Focus到首行，写注释说明用的
Ctrl+Shift+A：选择当前标签前后，修改标签用的
F11：全屏
Shift+F11：全屏免打扰模式，只编辑当前文件
Alt+F3：选择所有相同的词
Alt+.：闭合标签
Alt+Shift+数字：分屏显示
Alt+数字：切换打开第N个文件
Shift+右键拖动：光标多不，用来更改或插入列内容
鼠标的前进后退键可切换Tab文件
按Ctrl，依次点击或选取，可需要编辑的多个位置
按Ctrl+Shift+上下键，可替换行
```