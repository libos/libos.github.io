---
layout: post
title: "nginx tcp proxy"
date: 2016-01-09 15:48:43
comments: true
description: "nginx proxy"
keywords: "nginx,proxy,tcp"
categories: tech

tags:
- nginx
- proxy
- network

---

使用的是这个module，https://github.com/yaoweibin/nginx_tcp_proxy_module.

{% highlight bash %}
$ wget 'http://nginx.org/download/nginx-1.2.1.tar.gz'
$ tar -xzvf nginx-1.2.1.tar.gz
$ cd nginx-1.2.1/
$ patch -p1 &lt; /path/to/nginx_tcp_proxy_module/tcp.patch
$ ./configure --add-module=/path/to/nginx_tcp_proxy_module
$ make
$ make install
{% endhighlight %}
然后再nginx.conf里面：

{% highlight nginx %}
http{}
mail{}
tcp {
        upstream tcp_socket {
              server localhost:8751;
              check interval=3000 rise=2 fall=5 timeout=1000;
        } 
        server {
              listen 8750;
              proxy_pass tcp_socket;
        }
}
{% endhighlight %}

然后`nginx -s reload`
这样就可以了。然后启动本地的某个tcp程序，监听端口8751。用测试程序发起一个8750的连接请求，测试通过。而且不影响http的代理。
但是这个也有副作用，当服务端关闭连接的时候，客户端不可能立刻发觉连接已经被关闭，需要等到：
当nginx在执行check规则时认为服务端链接关闭，nginx会关闭与客户端的连接。