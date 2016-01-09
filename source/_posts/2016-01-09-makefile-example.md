---
layout: post
title: "Makefile Example"
date: 2016-01-09 15:41:34
comments: true
description: "Makefile example"
keywords: "Makefile,example"
categories: cpp

tags:
- Cpp
---

Most simple and explicit example of makefile.

{% highlight cpp %}
#编译分为两步 Compile 和 Link
#CC是编译器
CC = gcc
#LD 是Link driver
LD = gcc
#CFLAGS是Compile的时候参数。-g是带上debug代码，-Wall是多平台的错误监测，-O1是第一级代码优化，0~4（一般到4，可以更大），越大优化程度越高，有得有失
CFLAGS = -g -Wall -O1
#编译用到的库 参数有-L(后面加库可能在的地方，例如当前目录"-L.")和-l(后面加库名例如，"-lutil")
LDFLAGS = 
#必须要写出全部path，如果只写rm，有些用户可能把rm alias到了rm -i，使用全路径防止alias的影响
RM = /bin/rm -f
#源文件
SRCS = ./core/watcher.c ./core/wth_config.h
#两个不同的OBJS
OBJS = ./core/watcher.o
OBJS_TEST = ./test/test.o
#也可以这么写
# $(SRCS:.c=.o)
#多个目标
TARGETS = watcher client
 
 
all: $(TARGETS)
#要分这些，不知道合起来怎么写，欢迎留言
watcher:$(OBJS)
                $(LD) $(LDFLAGS) $(OBJS) -o watcher
 
client:$(OBJS_TEST)
        $(LD) $(LDFLAGS) $(OBJS_TEST) -o client
#这个可以一个一个的.o逐个写，也可以用通配符
# watcher.o: $(SRCS)
#                 $(CC) $(CFLAGS) -c $(SRC)
 
%.o: %.c %.h
 
                $(CC) $(CFLAGS) -c $<
#make clean 的时候，删除东东
clean:
                $(RM) $(TARGETS) $(OBJS) $(OBJS_TEST)
{% endhighlight%}