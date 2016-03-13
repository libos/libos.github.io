---
layout: post
title: "OSX How to Disable System Integrity Protection"
date: 2016-03-13 23:11:34
comments: true
description: "OSX How to Disable System Integrity Protection"
keywords: "OSX,Python,cannot,uninstall,pip,new package,sudo,does not work"
categories: python

tags:
- Python
- OSX
---

如果想更新Mac OSX中的Python，那么需要关掉系统级的权限保护，否则会导致无法更新，无法安装新的Python包。即便使用Homebrew也是错误连连。

因为在OSX中，如果System Integrity Protection是enable的，

{% highlight bash %}
/System
/sbin
/usr (除了/usr/local之外)
{% endhighlight %}

是被锁住的。即便在Terminal中使用sudo，也是不能修改其中的数据的。

如何关掉System Integrity Protection呢？

- 重启，按住Command+R键，指导选择启动项
- 选择Recovery Mode
- Utilities->Terminal
- 然后输入
{% highlight bash %}
csrutil disable
{% endhighlight %}
- 重启即可


如果想恢复输入命令，重启，进recovery，然后输入

{% highlight bash %}
csrutil enable
{% endhighlight %}

即可



hope save your day~


==
13 March 2016 23:33 Update

过年回来之后就开始懒了，虽然在学习Deep Learning，不过还得加油~
