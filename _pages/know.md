---
title: Knowledge
date: 2017-05-02
---

Knowledge | 知识
================

## `1497159733`{.tzx-timestamp} 知识的诅咒

奇普·希思与丹·希思合著的《粘住》一书中提到一种现象，叫“知识的诅咒”，说的是：
如果我们很熟悉某个对象的话，那么我们会很难想象，在不了解的人的眼中，这个对
象是什么样子的。

## `1497152154`{.tzx-timestamp} JQuery 的坑

JQuery
:   * 乱用选择器

        ```js
        //错误的写法
        $("#button").click(function(){
            $('#list li').addClass('strong');
            $('#list li').css('color', 'red');
        });
        //正确的写法
        $("#button").click(function(){
            $lis = $('#list li');
            $lis.addClass('strong');
            $lis.css('color', 'red');
        });
        //更好的写法
        $("#button").click(function(){
            $('#list li').addClass('strong').css('color', 'red');
        });
        ```
    * 全局选择效率低

        ```js
        //错误的写法
        $(".active").method();
        //正确的写法
        var ul = $("#myList");
        $(".active",ul).method();
        ```
    * 复制匿名函数

        ```js
        //错误的写法
        $('#myDiv').click( function(){
           //一些操作
        });
        //正确的写法
        function divClickFn(){
           //一些操作   
        }
        $('#myDiv').click(function(){
            divClickFn();
        });
        ```
    * 误用ajax 的 complete

        ```js
        //错误的写法
        $.ajax({
          url: "http://tools.42du.cn/jsonp/student/all",
        }).complete(function( data ) {
            //一些操作  
        });
        //正确的写法
        $.ajax({
          url: "http://tools.42du.cn/jsonp/student/all",
        }).success(function( data ) {
            //一些操作  
        });
        ```

    * 链式调用的误用

        ```js
        //错误的写法
        $("#myDiv").click(function(e) {
          $(this).fadeOut("slow").remove();
        });
        //正确的写法
        $("myDiv").click(function(e){
          $(this).fadeOut("slow", function(){
            $(this).remove();
          });
        });
        ```

    * 事件多次绑定

        ```js
        //避免响应多次执行
        $("myDiv").unbind("click").bind("click");
        ```

    * 错误使用 this 指示符
        + this 指示符存在上下文中，当 this 指向不同的对象。想调用原上下文的 this ，需缓存原 this 对象 ($that = $(this))。

        ```js
        //错误的写法
        $( "#myList").click( function() {
           $(this).method(); 
           $("#myList li").each( function() {
              //this并不指向myList
              $(this).method2(); 
           })
        });
        ```

Ref
:   * [简书](http://www.jianshu.com/p/1999872efdb3)

## `1496919234`{.tzx-timestamp} 马太效应

凡有的，还要加倍给他叫他多余；没有的，连他所有的也要夺过来。

## `1496239077`{.tzx-timestamp} Install travis
```sh
root@lotsd:~# gem install travis
Building native extensions.  This could take a while...
ERROR:  Error installing travis:
        ERROR: Failed to build gem native extension.

    current directory: /var/lib/gems/2.3.0/gems/ffi-1.9.18/ext/ffi_c
/usr/bin/ruby2.3 -r ./siteconf20170531-34-nj8hk7.rb extconf.rb
mkmf.rb can't find header files for ruby at /usr/lib/ruby/include/ruby.h

extconf failed, exit code 1

Gem files will remain installed in /var/lib/gems/2.3.0/gems/ffi-1.9.18 for inspection.
Results logged to /var/lib/gems/2.3.0/extensions/x86_64-linux/2.3.0/ffi-1.9.18/gem_make.out

root@lotsd:~# apt-get install ruby-dev # It can fix
```

## `1496230157`{.tzx-timestamp} Github pages DNS
```sh
$ dig YOUT-USERNAME.github.io +noall +answer
> YOUR-USERNAME.github.io 3600    IN  A  199.27.XX.XXX
```
添加 A 记录解析，主机纪录 www 记录值 199.27.XX.XXX

## `1496135688`{.tzx-timestamp} Time Zoon

Time Standards

:   * **GMT** >> Greenwich Mean Time
    * **UTC** >> Coordinated Universal Time
    * **DST** >> Daylight Saving Time (br. Summer Time)
    * **CST**
        + Central Standard Time (USA) UT-6:00
        + Central Standard Time (Australia) UT+9:30
        + China Standard Time UT+8:00
        + Cuba Standard Time UT-4:00

## `1494849129`{.tzx-timestamp} Unix timestramp

```sh
order: date +%s
out: 1494723178
order: date '+%Y-%m-%d %H:%M:%S'
out: 2017-05-14 08:52:58
order: date -d@"2017-05-14 08:52:58" '+%s'
out: 1494723178
order: date -d@1494723178 '+%Y-%m-%d %H:%M:%S'
out: 2017-05-14 08:52:58
```

## `1494723178`{.tzx-timestamp} Windows 端口

```sh
C:>netstat -aon|findstr "80"
C:>tasklist|findstr "2004"
C:>taskkill /im javaw.exe
C:>netstat -nat|grep 80|wc -l # 统计 80 端口连接数
C:>netstat -na|grep ESTABLISHED|wc -l #建立的连接数

```
Taskkill

```sh
TASKKILL /IM notepad.exe
TASKKILL /PID 1230 /PID 1241 /PID 1253 /T
TASKKILL /F /IM cmd.exe /T
TASKKILL /F /FI "PID ge 1000" /FI "WINDOWTITLE ne untitle*"
TASKKILL /F /FI "USERNAME eq NT AUTHORITY\SYSTEM" /IM notepad.exe
TASKKILL /S system /U 域\用户名 /FI "用户名 ne NT*" /IM *
TASKKILL /S system /U username /P password /FI "IMAGENAME eq note*" 
```

## `1494713178`{.tzx-timestamp} P2P

Peer-to-peer computing: 网络的参与者共享他们所拥有的一部分硬件资源（处理能力
、存储能力、网络连接能力、打印机等），这些共享资源通过网络提供服务和内容，能
被其它对等节点（Peer）直接访问而无需经过中间实体。在此网络中的参与者既是资源
、服务和内容的提供者（Server），又是资源、服务和内容的获取者（Client）

![p2p](http://doin.lotsdoin.me/image/p2p.jpg)
