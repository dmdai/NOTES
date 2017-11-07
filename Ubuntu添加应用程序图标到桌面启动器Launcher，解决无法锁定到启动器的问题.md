---
title: Ubuntu添加应用程序图标到桌面启动器Launcher，解决无法锁定到启动器的问题
tags: Ubuntu
grammar_cjkRuby: true
---



Linux下有些绿色软件，不需要安装就可以启动（一般都是在终端输入```./XXX.sh```），但有些程序在打开后直接在 Launcher 中右键选择**锁定到启动器**会使用一些默认图标（如linux下的**福昕阅读器**），有些软件即使锁定到启动器中，单击后闪了一阵什么都不会发生（如Sublime Text），有些软件甚至是不能锁定到启动器（如我们今天要说的软件**小书匠**）。

现在我们就讲一种针对上述问题的通用办法，**修改/添加软件的desktop启动文件！！！**

> 下面以上述最复杂情况的“小书匠”软件为例：

找到desktop文件位置
-
在终端输入：
`cd /usr/share/applications/`
`ls`
此时会看到很多desktop文件，这些便是可以在启动器中单击启动并配有漂亮图标的程序配置文件

![Desktop Entry.png](http://upload-images.jianshu.io/upload_images/3970488-f0a121e0e1ad352c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

创建小书匠的desktop文件
-
  既然知道了所有能在启动器单击启动的软件都有一个配置好的desktop文件，所以我们现在给小书匠配置desktop文件（因为小书匠属于不能添加到启动器的那种，当然也可能只是我电脑的问题！），方法如下：
1. 终端输入以下指令（请先确认当前目录是在/usr/share/applications）：
`sudo gedit XXX.desktop(这里的XXX随自己定)`
2. 在文本编辑器里输入大致如下图所示信息（英文系统可忽略带有[zh_CN]的部分）：
```python
[Desktop Entry]
Encoding=UTF-8
Version=4.0
Type=Application
Name=storywriter
Icon=/home/dai/文档/StoryWriter/Story-writer.png
Exec=/home/dai/文档/StoryWriter/Story-writer %F
Comment=The MarkDown Editor
Icon[zh_CN]=/home/dai/文档/StoryWriter/Story-writer.png
Name[zh_CN]=storywriter
Comment[zh_CN]=The Markdown Editor
Categories=Application;
Terminal=false
```
其中**Name**为想要显示在**Launcher**中的名称，**Icon**为图标所在路径，**Exec**是启动文件的路径（也即是之前```./XXX```的文件所在目录），**Comment** 为自己添加的说明。**“%F”**是能够让这个程序显示在"以其它方式启动"的列表中的意思！
可以看出此处的路径需全部使用**决定路径**，不可以使用环境变量。

配置好上述文件之后，我们再采用“笨方法”打开小书匠软件，右击“锁定到启动器”，会发现这时候就可以成功锁定了，并且以后可以在启动器直接单击启动了！！！