---
layout: post
title:  "Android Studio与Genymotion"

---

记录下自己的一时兴起所导致的坑，正所谓自己挖的坑，就得自己填。。

### 1.

由于重装电脑，手残的把用户名设置为了中文，所以不管是在安装Android Studio还是在使用Genymotion时都遇到了一系列由于中文所导致的问题，如Android Studio无法打开，Genymotion安装模拟器并不能安装等等。。。





这种问题怎么解决呢，第一，如果你不想再次重装，那你就重开一个账户，用来装Android与Genymotion等

### 2.

若是碰到了无法启动模拟器的情况，我以我碰到的问题来说明一下

1.无法启动，提示BIOS中不允许，所以进入BIOS界面，将虚拟的选项设置为Enable

在这里不同的电脑，BIOS界面不同，不过大致相同

一般来讲在开机停顿界面按F2便能够进入BIOS界面，进入后便可设置

可参考[http://www.xyaz.cn/thread-35-1-1.html](http://www.xyaz.cn/thread-35-1-1.html)内的一些开启BIOS以及设置VT的东西

2.遇到`this kernel requires an x86-64 cpu but only detected an i686 cpu'`

这种错误时，应该是你的虚拟机设置为了32位，将其改为64位即可
操作→`1.选中虚拟机，2.点击设置，3.选中常规4.选中基本，接着调版本，注意，若是开始的时候无法更改，需要先关闭再更改，重新打开便应该能够正常打开虚拟机`



### 3.

关联Android与Genymotion

可参考[http://www.loverobots.cn/the-method-of-association-genymotion-in-studio-android.html](http://www.loverobots.cn/the-method-of-association-genymotion-in-studio-android.html)





### 4.

利用模拟器访问本地电脑服务器（如Apache）

开始我用10.0.2.2进行访问出现错误

然后我边用了ipv4的ip地址进行访问便成功了

ps：查看ipv4，打开命令行输入`ipconfig或者ipconfig /all`便可查看



### 5.

当android studio的adb.exe(5037)端口被Genymotion占用时，可以将Genymotion的SDK设置为本地，然后重新启动即可



