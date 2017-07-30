---
title: Knowledge
date: 2017-05-02
---

Knowledge | 知识
================

## `1500207047`{.tzx-timestamp} Dia 中文
```bash
$ sudo vim /usr/bin/dia
# change
# dia-normal --integrated "$@"
dia-normal "$@"
```

## `1500099669`{.tzx-timestamp} 公式
The *Gamma function* satisfying $\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N$ is via the Euler integral

$$
\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.
$$

## `1499830713`{.tzx-timestamp} Linux sublime-text 中文输入
系统: ubuntu 16.04 LTS
fcitx version: 4.2.9.1
Sublime Text: Stable Channel,Build 3126
1. 保存以下代码为 sublime-imfix.c
```cpp
/*
sublime-imfix.c
Use LD_PRELOAD to interpose some function to fix sublime input method support for linux.
By Cjacker Huang

gcc -shared -o libsublime-imfix.so sublime-imfix.c `pkg-config --libs --cflags gtk+-2.0` -fPIC
LD_PRELOAD=./libsublime-imfix.so subl
*/
#include <gtk/gtk.h>
#include <gdk/gdkx.h>
typedef GdkSegment GdkRegionBox;

struct _GdkRegion
{
  long size;
  long numRects;
  GdkRegionBox *rects;
  GdkRegionBox extents;
};

GtkIMContext *local_context;

void
gdk_region_get_clipbox (const GdkRegion *region,
            GdkRectangle    *rectangle)
{
  g_return_if_fail (region != NULL);
  g_return_if_fail (rectangle != NULL);

  rectangle->x = region->extents.x1;
  rectangle->y = region->extents.y1;
  rectangle->width = region->extents.x2 - region->extents.x1;
  rectangle->height = region->extents.y2 - region->extents.y1;
  GdkRectangle rect;
  rect.x = rectangle->x;
  rect.y = rectangle->y;
  rect.width = 0;
  rect.height = rectangle->height;
  //The caret width is 2;
  //Maybe sometimes we will make a mistake, but for most of the time, it should be the caret.
  if(rectangle->width == 2 && GTK_IS_IM_CONTEXT(local_context)) {
        gtk_im_context_set_cursor_location(local_context, rectangle);
  }
}

//this is needed, for example, if you input something in file dialog and return back the edit area
//context will lost, so here we set it again.

static GdkFilterReturn event_filter (GdkXEvent *xevent, GdkEvent *event, gpointer im_context)
{
    XEvent *xev = (XEvent *)xevent;
    if(xev->type == KeyRelease && GTK_IS_IM_CONTEXT(im_context)) {
       GdkWindow * win = g_object_get_data(G_OBJECT(im_context),"window");
       if(GDK_IS_WINDOW(win))
         gtk_im_context_set_client_window(im_context, win);
    }
    return GDK_FILTER_CONTINUE;
}

void gtk_im_context_set_client_window (GtkIMContext *context,
          GdkWindow    *window)
{
  GtkIMContextClass *klass;
  g_return_if_fail (GTK_IS_IM_CONTEXT (context));
  klass = GTK_IM_CONTEXT_GET_CLASS (context);
  if (klass->set_client_window)
    klass->set_client_window (context, window);

  if(!GDK_IS_WINDOW (window))
    return;
  g_object_set_data(G_OBJECT(context),"window",window);
  int width = gdk_window_get_width(window);
  int height = gdk_window_get_height(window);
  if(width != 0 && height !=0) {
    gtk_im_context_focus_in(context);
    local_context = context;
  }
  gdk_window_add_filter (window, event_filter, context);
}
```
2. 安装编译环境
```bash
sudo apt-get install build-essential
sudo apt-get install libgtk2.0-dev
```
3. 编译共享库
```bash
gcc -shared -o libsublime-imfix.so sublime-imfix.c `pkg-config --libs --cflags gtk+-2.0` -fPIC
```
4. 设置 LD_PRELOAD 并启动 Sublime Text
```bash
LD_PRELOAD=./libsublime-imfix.so subl
```
5. 修改 /usr/share/applications/sublime-text.desktop

```txt
[Desktop Entry]
[...]
Exec=env LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so /opt/sublime_text/sublime_text %F
[...]

[Desktop Action Window]
[...]
Exec=env LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so /opt/sublime_text/sublime_text -n
[...]

[Desktop Action Document]
[...]
Exec=env LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so /opt/sublime_text/sublime_text --command new_file
[...]
```
6. 将 libsublime-imfix.so 放到 /opt/sublime_text/
7. 修改 /usr/bin/subl

```bash
#!/bin/sh
export LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so
exec /opt/sublime_text/sublime_text "$@"
```
8. Reboot your computer.

ref
:   * [SinoSky](https://www.sinosky.org/linux-sublime-text-fcitx.html)

## `1499650590`{.tzx-timestamp} Install youdao-dict in ubuntu
```bash
$ wget http://codown.youdao.com/cidian/linux/youdao-dict_1.1.0-0-ubuntu_amd64.deb
$ sudo dkpg -i youdao-dict_1.1.0-0-ubuntu_amd64.deb
$ sudo apt-get install python3-pyqt5
$ sudo apt-get -f install
$ sudo apt-get install tesseract-ocr
# warning: gstreamer0.10-plugins-ugly you have not install
$ dpkg -X ./youdao-dict_1.1.0-0-ubuntu_amd64.deb youdao
$ dpkg -e ./youdao-dict_1.1.0-0-ubuntu_amd64.deb youdao/DEBIAN
$ cd youdao/DEBIAN
$ vim control # remove gstreamer0.10-plugins-ugly
$ dpkg-deb -b youdao youdao.deb # rebuild package
$ sudo dpkg -i youdao.deb
# from http://blog.csdn.net/brad1994/article/details/56484634
```

## `1499594613`{.tzx-timestamp} Ubuntu XTerm 中文
```bash
$ sudo vim /etc/X11/app-defaults/XTerm
add

!Add in [17:09:19@2017:07:09] from http://huanglianjing0.blog.163.com/blog/static/733932222013101811225548/

Xft.dpi:96     
    xpdf.title: PDF     
    XTerm*faceSize: 10     
    XTerm*faceSize1: 10     
    XTerm*faceSize2: 10     
    XTerm*faceSize3: 10     
    XTerm*faceSize4: 10     
    XTerm*faceSize5: 10     
    XTerm*faceSize6: 10     
    XTerm*jumpScroll: true     
        
    xterm.termName: xterm-256color    
    xterm.geometry: 80x24    
    xterm*scrollBar: false    
    xterm*rightScrollBar: true    
    xterm*loginshell: true    
    xterm*cursorBlink: true    
    xterm*background:   black    
    xterm*foreground:   gray    
    xterm.borderLess: true    
    xterm.cursorBlink: true    
    xterm*colorUL: yellow    
    xterm*colorBD: white    
         
    !fix alt key input    
    xterm*eightBitInput: false    
    xterm*altSendsEscape: true   
      
    !mouse selecting to copy, ctrl-v to paste    
    !Ctrl p to print screen content to file    
    XTerm*VT100.Translations: #override \    
          Ctrl <KeyPress> V: insert-selection(CLIPBOARD,PRIMARY,CUT_BUFFER0) \n\    
          <BtnUp>: select-end(CLIPBOARD,PRIMARY,CUT_BUFFER0) \n\    
          Ctrl <KeyPress> P: print() \n    
        
    !font and locale    
    !xterm*locale: true    
    !xterm.utf8: true    
    !xterm*utf8Title: true  
    xterm*fontMenu*fontdefault*Label: Default    
    xterm*faceName:Monaco:antialias=True:pixelsize=12
    !xterm*faceName: Monaco:antialias=True:pixelsize=12
    xter*boldFont: Monaco:style=Bold:pixelsize=12
    !SimHei 是中文字体
    xterm*faceNameDoublesize:SimHei:antialias=True:pixelsize=12
    xterm*xftAntialias: true    
    xterm.cjkWidth:true    
    !输入法设置 fcitx
    XTerm*inputMethod: fcitx   
    XTerm*preeditType: Root
```


## `1499361728`{.tzx-timestamp} Windows Sysinternals update
[Windows Sysinternals](https://technet.microsoft.com/en-us/sysinternals/bb795535.aspx)包含了很多微软提供的实用工具，
单独升级麻烦。

```powershell
function Update-SysinternalsHTTP ($ToolsLocalDir = "c:\temp\sys")  
{ 
    if (Test-Path $ToolsLocalDir){ 
        cd $ToolsLocalDir
        $DebugPreference = "SilentlyContinue"
        $wc = new-object System.Net.WebClient
        $userAgent = "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.2;)"
        $wc.Headers.Add("user-agent", $userAgent)
        $ToolsUrl = "http://live.sysinternals.com/tools"
        $toolsBlock="<pre>.*</pre>"
        $WebPageCulture = New-Object System.Globalization.CultureInfo("en-us")
        $Tools = @{}
        $ToolsPage = $wc.DownloadString($ToolsUrl)
        $matches=[string] $ToolsPage |select-string -pattern  "$ToolsBlock" -AllMatches
        foreach($match in $matches.Matches) {   
            $txt = ( ($match.Value  -replace "</A><br>", "`r`n") -replace  "<[^>]*?>","")
            foreach($lines in $txt.Split("`r`n")){
                $line=$lines|select-string  -NotMatch -Pattern "To Parent|^$|&lt;dir&gt;"
                if ($line -ne $null){
                    $date=(([string]$line).substring(0,38)).trimstart(" ") -replace "  "," "
                    $file=([string]$line).substring(52,(([string]$line).length-52))
                    $Tools["$file"]= [datetime]::ParseExact($date,"f",$WebPageCulture)
                }
            }
        }
        $Tools.keys|
        ForEach-Object {
            $NeedUpdate=$false
            if (Test-Path $_)
            {
                $SubtractSeconds = New-Object System.TimeSpan 0, 0, 0, ((dir $_).lastWriteTime).second, 0
                $LocalFileDate= ( (dir $_).lastWriteTime ).Subtract( $SubtractSeconds )
                $needupdate=(($tools[$_]).touniversaltime() -lt $LocalFileDate.touniversaltime())
            } else {$NeedUpdate=$true}
            if ( $NeedUpdate ) 
            {
                Try {
                        $wc.DownloadFile("$ToolsUrl/$_","$ToolsLocalDir\$_" )
                        $f=dir "$ToolsLocalDir\$_"
                        $f.lastWriteTime=($tools[$_])
                        "Updated $_"
                    }
                catch { Write-debug "发生错误: $_" }
            } 
        } 
    }
}
cls
"更新开始..."
Update-Sysinternalshttp -ToolsLocalDir "D:\Tools"
"更新结束"
```
将脚本保存为`.psl`后缀的文件，使用 PowerShell 运行。注意路径`D:\Tools`,代码其实是到
[live.sysinternals](http://live.sysinternals.com/tools) 比对文件信息进行更新。

ref
:   * [www.mycode.net.cn](http://www.mycode.net.cn/tools/1629.html)

## `1499333837`{.tzx-timestamp} 管理源码安装

```bash
$ sudo make install
# change it to follow order
$ sudo checkinstall
```

## `1499310329`{.tzx-timestamp} Git push no input password

Git SSH
:   * Normal nothing cached, every time you should enter your password.
    * "cache" mode, remember password in memery by 15 minutes.
        + `git config --global credential.helper cache`
    * "store" mode, remember plaintext password in home directory, it is dangerous.
        + `git config --global credential.helper store --file ~/.my-credentials`

```bash
$ sudo vim ~/.git-credentials
add follow things but no {}
https://{username}:{password}@github.com
$ sudo git config --global credential.helper store
then ~/.gitconfig will add
helper = store
```

## `1499309008`{.tzx-timestamp} Close the startup voice

```bash
终端中打
$ sudo gsettings set com.canonical.unity-greeter play-ready-sound false
想要开启声音：
$ gsettings set com.canonical.unity-greeter play-ready-sound true

# 作者：林位廉
# 链接：https://www.zhihu.com/question/37105834/answer/105061752
# 来源：知乎
# 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

# 以上试验了不行
$ cd /usr/share/sounds/ubuntu/stereo/
$ mv system-ready.ogg system-ready.bak.ogg
$ touch system-ready.ogg
```

## `1499280503`{.tzx-timestamp} Ubuntu install problem
```bash
dpkg: 处理软件包 pandoc (--configure)时出错：
 现在尚不能配置软件包 pandoc
 不能配置(目前状态为 half-installed )
在处理时有错误发生：
 pandoc
E: Sub-process /usr/bin/dpkg returned an error code (1)

$ sudo apt-get install --reinstall pandoc #stop install when install pandoc,as to cause it.
```

## `1498107710`{.tzx-timestamp} Git config

#. /etc/gitconfig 文件：包含了适用于系统所有用户和所有库的值。如果你传递参数选项 ’--system’ 给 git config，它将明确的读和写这个文件。  
#. ~/.gitconfig 文件 ：具体到你的用户。你可以通过传递 --global 选项使 Git 读或写这个特定的文件。
#. 位于 git 目录的 config 文件 (也就是 .git/config) ：无论你当前在用的库是什么，特定指向该单一的库。每个级别重写前一个级别的值。因此，在 .git/config 中的值覆盖了在 /etc/gitconfig 中的同一个值。
#. 在 Windows 中, .gitconfig 在 $HOME 中找到。

```bash
[user]
	name = lotsdoin
	email = lotsdoin@gmail.com
[alias]
	lg = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
    st = status
    ci = commit
    br = branch
    g = git
    co = checkout
    spacemacs='cd ~/AppData/Roaming/.emacs.d/'
    cnpm="npm --registry=https://registry.npm.taobao.org \
    --cache=$HOME/.npm/.cache/cnpm \
    --disturl=https://npm.taobao.org/dist \
    --userconfig=$HOME/.cnpmrc"
    pantzx="pandoc -S -s -c http://tangzx.qiniudn.com/main.css --ascii --toc \
    --highlight-style pygments -f markdown+abbreviations+pandoc_title_block+east_asian_line_breaks+emoji --mathjax"

    pan="pandoc -S -s -c _static/main.css --ascii --toc --highlight-style pygments -f markdown+abbreviations+pandoc_title_block+east_asian_line_breaks+emoji --template _static/template.htm --mathjax"
    #date="date '+%Y-%m-%d %H:%M:%S'"
    lxss="cd ~/AppData/Local/lxss"

```

## `1497845458`{.tzx-timestamp} 视角
蔡崇达的《皮囊》中：“肉体是拿来用的。”，将肉体和意识独立出来理解，对于这句话的理解，仁者见仁智者见智。每个人都可以是布道者，
或者是受众。

## `1497581447`{.tzx-timestamp} RubyGems SSL

下载 [Rails Installer](http://railsinstaller.org/), 将 [cacert.pem](http://curl.haxx.se/ca/cacert.pem)
放到 Rails Installer 安装目录下, 添加 cacert.pem 到系统环境变量，设变量名为 SSL_CERT_FILE ，例如我的
![cacert](http://doin.lotsdoin.me/image/RubyGem.png)

Ref
:   * [Github](https://gist.github.com/fnichol/867550)

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
```bash
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
```bash
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

```bash
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

```bash
C:>netstat -aon|findstr "80"
C:>tasklist|findstr "2004"
C:>taskkill /im javaw.exe
C:>netstat -nat|grep 80|wc -l # 统计 80 端口连接数
C:>netstat -na|grep ESTABLISHED|wc -l #建立的连接数

```
Taskkill

```bash
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
