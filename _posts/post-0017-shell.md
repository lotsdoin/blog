---
title: Shell
date: 2017年06月20日 15:13:30
---

Shell
=====

Simple
----

```bash
!$                              # 代表上一个命令的最后一个字符串
sudo !!                         # 以 root 执行上一个命令
!xxx                            # 重复最近的一条命令
eg:
$ vim ~/lotsd/blog/conf.json
$ !vim or !vi                   # 取决于最近的首字母
cd -                            # 回到上一次目录
<Alt> . or ESC .                # 获得上次命令行参数
^x^y                            # 替换上一条命令里的部分字符串
eg:
$ echo 'wanderful'
$ ^a^o
man ascii                       # 显示 ASCII 表
date -d@1499350189              # 时间戳转时间
date +%s                        # 时间戳
wget --random-wait -r -p -e rebots=off -U mozilla http://www.example.com # 网络镜像
curl ifconfig.me                # 查看外网的 IP
convert input.png -gravity NorthWest -background transparent -extent 720x200 output.png # 改变图片大小
gs -dNOPAUSE -sDEVICE=pdfwrite -sOUTPUTFILE=output.pdf -dBATCH input1.pdf input2.pdf # 合并多个 pdf 到一个 pdf 文件
echo "ls -l" | at midnight      # 在特定时间运行命令
curl -u username -silent "https://mail.google.com/mail/feed/atom" | perl -ne 'print "\t" if /<name>/; print "$2\n" if /<(title|name)>(.*)<\/\1>/;' # 检查你的 gmail 未读邮件
python -m SimpleHTTPServer      # 一句话实现 HTTP 服务 http://localhost:8000
history | awk '{CMD[$2]++;count++;} END { for (a in CMD )print CMD[a] " " CMD[a]/count*100 "% " a }' | grep -v "./" | column -c3 -s " " -t | sort -nr | nl | head -n10 # 输出你最常用的十个命令
history|awk '{print $2}'|awk 'BEGIN {FS="|"} {print $1}'|sort|uniq -c|sort -rn|head -10 # 输出你最常用的十个命令
$ du -s * | sort -n | tail      # 列出当前目录里最大的10个文件
$ cp -av 原文件或原目录 新文件或新目录 # 复制文件或者目录
$  cat /etc/vsftpd.conf |grep -v ^#    # 不显示以＃开头的行
$ nl 文件名                     # 带行号显示文件的内容
$ cat -n 文件名                 # 带行号显示文件的内容
$ file filename                 # 查看文件类型
$ echo xxx.xxx.rmvb |sed 's/.*\(\..*$\)/\1/'  # 获得文件的后缀名
$ echo xxx.xxx.rmvb |sed 's/\(.*\)\..*$/\1/'  # 去除文件的后缀名
$ tail -6 xxx                   # 显示xxx文件倒数6行的内容
$ sed -n '5,10p' /var/log/apache2/access.log  # 查看文件中指定行范围的内容 如第五行（含）到第10行（含）：
$ ls -d */ 或 echo */           # 查看当前目录的子目录
$ find . -mmin +120 -mmin -480 -exec more {} \;   # 显示当前目录指定时间范围的文件如2小时到8小时之内：
$ cut -c 5- a.py                # 去除文件中的行号
$ grep -l -r 字符串 路径　#显示内容包含字符串的文件名
$ grep -L -r 字符串 路径　#显示内容不包含字符串的文件名
$ find . -path './cache' -prune -o -name "*.php" -exec grep -l "date_cache[$format]['lang']" {} \; #显示当前目录下不包含cache目录的所有含有“date_cache[$format]['lang']”字符串的php文件。
$ find . -type f -name \*.php -exec grep -l "info" {} \;
$ rename .rm .rmvb *.rm         # 把所有文件的後辍由rm改为rmvb
$ rename 'tr/A-Z/a-z/' *        # 把所有文件名中的大写改为小写
# 去掉文件中的^M
#注意不要使用同样的文件名，会清空掉原文件
$ cat filename | tr -d "^M" > newfile;
    或者
$ sed -e "s/^M//g" filename > newfile;
    或者
ex "+:%s/[Ctrl+V][Enter]//g" "+:wq"  filename #直接修改文件
# 批量修改文件和目录的权限
# 批量修改src目录下所有文件的权限为644：
$ find src -type f -exec chmod 644 {} \;
批量修改src目录下的所有子目录的权限为755：
$ find src -type d -exec chmod 755 {} \;
# 删除特殊文件名的文件
# 如文件名：–help.txt ：
$ rm -- --help.txt 或者 rm ./--help.txt
# 删除当前目录里面所有的.svn目录
$ find . -name .svn -type d -exec rm -fr {} \;
# 查找删除不以java和xml结尾，并7天没有使用的文件
$ find . ! -name *.java ! -name ‘*.xml’ -atime +7 -exec rm {} \;
# 查找目录下所有有包含abcd文字的文本文件，并替换为xyz
$ grep -rIl "abcd" ./## --color=never | xargs sed -i "s/abcd/xyz/g" #注意grep的一个参数是大写的i，一个参数是小写的L
# 服务和进程
# 列出头十个最耗内存的进程
ps aux | sort -nk +4 | tail
# 列出本机进程监听的端口号
netstat -tlnp
# 实时查看本机网络服务的活动状态
lsof -i
# 陈皓注： netstat -anop 可以显示侦听在这个端口号的进程 伟洲注： lsof -i:<端口号> 可以查看某个端口号被什么程序占用
# 实时监控并过滤log是否出现了某条记录
$ tail -f /path/to/file.log | sed '/^Finished: SUCCESS$/ q'
# 当file.log里出现Finished: SUCCESS时候就退出tail，这个命令用于实时监控并过滤log是否出现了某条记录。
# 在远程机器上运行一段脚本
$ ssh user@server bash < /path/to/local/script.sh
# 在远程机器上运行一段脚本。这条命令最大的好处就是不用把脚本拷到远程机器上。
# 比较一个远程文件和一个本地文件
$ ssh user@host cat /path/to/remotefile | diff /path/to/localfile -
# 后台运行一段不终止的程序，并可以随时查看它的状态
$ screen -d -m -S some_name ping my_router

```
ref
:   * [www.hahack.com](http://www.hahack.com/wiki/shell-snippets.html)


## Complex


```bash
# 删除 0 字节文件
find . -type f -size 0 -exec rm -rf {} \;
find . -type f -size 0 -delete
# 内存的大小
free -m |grep "Mem" | awk '{print $2}'
# 查看 80 端口的连接，并排序
netstat -an -t | grep ":80" | grep ESTABLISHED | awk '{printf "%s %s\n",$5,$6}' | sort
# CPU 数量
cat /proc/cpuinfo |grep -c processor
# CPU 负载
cat /proc/loadavg
# 内存空间
free
# 磁盘空间
df -h
# 文件占用排序
du -cks * | sort -rn | head -n 10
# 磁盘 I/O 负载
iostat -x 1 2
# 网络负载
sar -n DEV
# 网络错误
netstat -i cat /proc/net/dev
# 网络连接数目
netstat -an | grep -E "^(tcp)" | cut -c 68- | sort | uniq -c | sort -n
# 进程总数
ps aux | wc -l
# 进程树
ps aufx
# 可运行进程数
vmwtat 1 5
# 查看 DNS Server 工作是不是正常，以 61.139.2.69
dig www.baidu.com @61.139.2.69
# 检查当前登陆的用户个数
who | wc -l
# 日志查看，搜索
cat /var/log/syslog
# 内核日志
dmesg
# 打开的句柄数
lsof | wc -l
# 网络抓包，直接输出摘要信息到文件
tcpdump -c 10000 -i eth0 -n dst port 80 > root/pkts
# 最常用的 10 个命令
history | awk '{CMD[$2]++;count++;}END { for (a in CMD)print CMD[a] " " CMD[a]/count*100 "% " a;}' | grep -v "./" | column -c3 -s " " -t | sort -nr | nl |  head -n10
```
ref
:   * [jobbole](http://blog.jobbole.com/48173/)

Attention
:   * `cp` 注意 `cp -i 1.txt note/` and `cp - i 1.txt note`
    * `cp -i` `-i` ask you overwirte file,it's safe.
    * `chmod +x` `+x` 使文件有可执行权限.
    * not executable format file(不是可执行的文件类型)
    * 新建(fork)一个进程
    * source echo.sh (source may change environment variable(变量).)
        ```bash
        $ cat echo.sh
        #!/bin/sh
        cd /tmp
        echo "hello world!"
        $ pwd
        /home/lotsd/lotsd/projects/Bash
        $ sudo chmod +x echo.sh
        $ source echo.sh
        $ pwd
        /tmp
        ```
    * 运行 Linux program's 3 ways
        + 使文本具有可执行权限，直接运行。`./echo.sh`
        + 直接调用命令解释器执行程序。eg: `$ bash echo.sh`
        + 使用 source 执行文件。
    * Linux 可执行的命令有 3 种：
        + 内建命令
        + shell 函数
        + 外部命令
    * variable in Linux shell all are String, while variable is number can be operated(运算).
    * variable_name=value(值), `=` both sides not spacing.
    * $dir_name is abbreviated form (简写形式) ${dir_name}
    * single quotes represent strong reference.(单引号代表强引用)
    * double quotes represent weak reference.
        ```bash
        $ var=34
        $ echo "$var"
        34
        $ echo '$var'
        $var
        ```
