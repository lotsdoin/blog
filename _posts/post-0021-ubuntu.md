---
title: Ubuntu
date: Tue Jul  4 13:38:56 CST 2017
---

Ubuntu 16.04 LST
================

Build ubuntu
------------

### Change sources

`sudo vim /etc/apt/sources.list`

```bash
# deb cdrom:[Ubuntu 16.04 LTS _Xenial Xerus_ - Release amd64 (20160420.1)]/ xenial main restricted
deb-src http://archive.ubuntu.com/ubuntu xenial main restricted #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted multiverse universe #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted multiverse universe #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ xenial universe
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates universe
deb http://mirrors.aliyun.com/ubuntu/ xenial multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse #Added by software-properties
deb http://archive.canonical.com/ubuntu xenial partner
deb-src http://archive.canonical.com/ubuntu xenial partner
deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted multiverse universe #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ xenial-security universe
deb http://mirrors.aliyun.com/ubuntu/ xenial-security multiverse
```
`sudo apt-get update`

`or`
choose `http://mirrors.aliyun.com/ubuntu` in `system seting / software and update`

### How to install in ubuntu
```bash
$ sudo apt-get install package-name -y # 默认为 yes
# deb 包安装 & 卸载
$ sudo dpkg -i xxx.deb
$ sudo apt-get install -f # 安装依赖
$ sudo apt-get autoclean
$ sudo apt-get autoremove
$ sudo apt-get remove --purge package-name # 完全卸载
$ sudo apt-get install ./xxx.deb
# 常见解压文件命令
$ *.tar               : tar -xvf
$ *.gz                : gzip -d or gunzip
$ *.tar.gz or *.tgz   : tar -xzf
$ *.bz2               : bzip2 -d or bunzip2
$ *.tar.bz2           : tar -xjf
$ *.Z                 : uncompress
$ *.tar.Z             : tar -xZf
$ *.rar               : unrar e
$ *.zip               : unzip
```

### Install Albert
```bash
$ sudo add-apt-repository ppa:nilarimogard/webupd8
$ sudo apt-get update
$ sudo apt-get install albert

```

### Git

```bash
$ sudo apt-get install git
$ git config --global user.name "lotsdoin"
$ git config --global user.email "lotsdoin@gmail.com"
$ ssh-keygen -t rsa C "lotsdoin@gmail.com"
$ eval "($ssh-agent -s)" # use ssh-agent
Agent pid 14051
$ ssh-add ~/.ssh/id_rsa
Identity added: /home/lotsd/.ssh/id_rsa (/home/lotsd/.ssh/id_rsa)
$ ssh -T git@github.com # check it
```

### Remove Amazon link
`sudo apt-get remove unity-webapps-common`

### Install Java

#### Install Oracle Java

[Oracle](http://www.oracle.com/technetwork/cn/java/javase/downloads/jdk8-downloads-2133151-zhs.html)

```bash
wget http://download.oracle.com/otn-pub/java/jdk/8u111-b14/jdk-8u111-linux-x64.tar.gz`
tar -zxvf jdk-8u111-linux-x64.tar.gz
mkdir /usr/lib/jdk
mv jdk-8u111  /usr/lib/jdk/jdk1.8
vim /etc/profile # all users
export JAVA_HOME=/usr/lib/jdk/jdk1.8
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=.:${JAVA_HOME}/bin:$PATH
vim ~/.bashrc # local user
export JAVA_HOME=/usr/lib/jdk/jdk1.8
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=.:${JAVA_HOME}/bin:$PATH
source /etc/profile  or  source ~/.bashrc # work now.
java -version # check it.
```

```bash
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```
### Install Sublime Text 3
```bash
sudo add-apt-repository ppa:webupd8team/sublime-text-3    
sudo apt-get update    
sudo apt-get install sublime-text 
```
### Install Code::Blcoks 16.01
```bash
$ sudo apt-get Install build-essential
$ sudo apt-get install gdb
$ sudo add-apt-repository ppa:damien-moore/codeblocks-stable  
$ sudo apt-get update  
$ sudo apt-get install codeblocks 
#将会同时安装下列软件：  
#codeblocks-common libcodeblocks0 libwxbase2.8-0 libwxgtk2.8-0  
#建议安装：  
#libwxgtk2.8-dev | libwxgtk3.0-dev wx-common codeblocks-contrib   
$ sudo apt-get install codeblocks-dbg  
$ sudo apt-get install codeblocks-contrib  
# //将会同时安装下列软件：  
# //cccc codeblocks-contrib-common codeblocks-libwxcontrib0 cppcheck cscope  
# //gamin libgamin0 libtinyxml2-2v5 libwxsmithlib0 python-chardet  
# //python-pkg-resources python-pygments valgrind  
# 建议安装：  
# //cscope-el python-setuptools ttf-bitstream-vera valgrind-dbg kcachegrind  
# //alleyoop valkyrie   
$ sudo apt-get install valgrind-dbg  
# //Valgrind 用来探测内存泄露  

# wxWindgets 图形界面库
$ sudo apt-get install libwxbase3.0  
$ sudo apt-get install libwxbase3.0-dev  
$ sudo apt-get install libwxgtk3.0-0  
$ sudo apt-get install libwxgtk3.0-dev  
$ sudo apt-get install wx-common  
$ sudo apt-get install wx3.0-headers  
$ sudo apt-get install wx3.0-i18n  
```
ref
:   * [CSDN](http://blog.csdn.net/left_coast/article/details/52159762)

### Install axel (like wget)

`sudo apt-get install axel`

### Install CMake and Qt Creator
`sudo apt-get Install cmake qtcreator`

### Install lnav (review log)

`sudo apt-get Install lnav`

### Install unrar

`sudo apt-get Install unrar`

### Ubuntu 16.04 L2TP

long long age,use `sudo apt-get Install l2tp-ipsec-vpn`,but 
now Ubuntu 16.04 remove it.

```bash
sudo apt install intltool libtool network-manager-dev libnm-util-dev libnm-glib-dev libnm-glib-vpn-dev libnm-gtk-dev libnm-dev libnma-dev ppp-dev libdbus-glib-1-dev libsecret-1-dev libgtk-3-dev libglib2.0-dev xl2tpd strongswan

git clone https://github.com/nm-l2tp/network-manager-l2tp.git    
cd network-manager-l2tp    
autoreconf -fi    
intltoolize 

./configure \  
  --disable-static --prefix=/usr \  
  --sysconfdir=/etc --libdir=/usr/lib/x86_64-linux-gnu \  
  --libexecdir=/usr/lib/NetworkManager \  
  --localstatedir=/var \  
  --with-pppd-plugin-dir=/usr/lib/pppd/2.4.7  

make    
sudo make install

sudo apparmor_parser -R /etc/apparmor.d/usr.lib.ipsec.charon    
sudo apparmor_parser -R /etc/apparmor.d/usr.lib.ipsec.stroke

sudo apt remove xl2tpd    
sudo apt install libpcap0.8-dev  

wget https://github.com/xelerance/xl2tpd/archive/v1.3.6/xl2tpd-1.3.6.tar.gz    
tar xvzf xl2tpd-1.3.6.tar.gz    
cd xl2tpd-1.3.6    
make    
sudo make install  
```

IPsec add `Pre-shared key`

### Install YaHeiConsolas

```bash
wget http://www.mycode.net.cn/wp-content/uploads/2015/07/YaHeiConsolas.tar.gz
tar -zxvf YaHeiConsolas.tar.gz
sudo mkdir -p /usr/share/fonts/vista
sudo cp YaHeiConsolas.ttf /usr/share/fonts/vista/
sudo chmod 644 /usr/share/fonts/vista/*.ttf
cd /usr/share/fonts/vista/
sudo mkfontscale && sudo mkfontdir && sudo fc-cache -fv # refresh and install
```
and download unity-tweak-tool like `sudo apt-get install unity-tweak-tool` change font .

### Flatabulous theme

```bash
sudo add-apt-repository ppa:noobslab/themes
sudo apt-get update
sudo apt-get install flatabulous-theme
```
and icons

```bash
sudo add-apt-repository ppa:noobslab/icons
sudo apt-get update
sudo apt-get install ultra-flat-icons
```

### Compile vim by Ubuntu

#### Install lib

```bash
sudo apt-get install libncurses5-dev libgnome2-dev libgnomeui-dev \
    libgtk2.0-dev libatk1.0-dev libbonoboui2-dev \
    libcairo2-dev libx11-dev libxpm-dev libxt-dev python-dev \
    python3-dev ruby-dev lua5.1 lua5.1-dev git
```
#### Remove old vim

```bash
dpkg -l | grep vim
sudo dpkg -p vim vim-common vim-run
```

#### Download vim and install

```bash
git clone https://github.com/vim/vim.git
cd vim
# complie with python2
./configure --with-features=huge \
            --enable-multibyte \
            --enable-rubyinterp \
            --enable-pythoninterp \
            --with-python-config-dir=/usr/lib/python2.7/config-x86_64-linux-gnu \
            --enable-perlinterp \
            --enable-luainterp \
            --enable-gui=gtk2 --enable-cscope --prefix=/usr

# complie with python3
./configure --with-features=huge \
            --enable-multibyte \
            --enable-rubyinterp \
            --enable-python3interp \
            --with-python-config-dir=/usr/lib/python3.5/config-3.5m-x86_64-linux-gnu \
            --enable-perlinterp \
            --enable-luainterp \
            --enable-gui=gtk2 --enable-cscope --prefix=/usr

make VIMRUNTIMEDIR=/usr/share/vim/vim80
sudo make install
```

use `checkinstall` change tool compile by self to `deb` package, it is easy to remove it
like `sudo dpkg -P vim`.

```bash
sudo apt-get install checkinstall
cd vim
sudo checkinstall
```

#### Set vim as default editor
```bash
sudo update-alternatives --install /usr/bin/editor editor /usr/bin/vim 1
sudo update-alternatives --set editor /usr/bin/vim
sudo update-alternatives --install /usr/bin/vi vi /usr/bin/vim 1
sudo update-alternatives --set vi /usr/bin/vim
```
### Install uGet

```bash
sudo add-apt-repository ppa:t-tujikawa/ppa 
sudo apt-get update 
sudo apt-get install uget 
```

### Uninstall ppa

```bash
sudo add-apt-repository --remove ppa:t-tujikawa/ppa
sudo ppa-purge ppa:t-tujikawa/ppa
```
### Install wine

```bash
1、安装源
      sudo add-apt-repository ppa:wine/wine-builds
      sudo apt-get update
2、安装wine
     sudo apt-get install --install-recommends wine-staging
     sudo apt-get install winehq-staging
3、卸载wine
     1).卸载wine主程序，在终端里输入：
       sudo apt-get remove --purge wine
     2).然后删除wine的目录文件：
       rm -r ~/.wine
     3).卸载残留不用的软件包：
       sudo apt-get autoremove
```
### Install pptp vpn server

You can configure pptp VPN server and client from the terminal using these steps:
VPN Server Setup:

Install and update the VPN server and client packages:

`$ sudo apt-get install pptpd ppp pptp-linux`

Four files has to be configured for the server:

    /etc/pptpd.conf
    /etc/ppp/pptpd-options
    /etc/ppp/options
    /etc/chat-secrets)

/etc/pptpd.conf:

option /etc/ppp/pptpd-options
logwtmp
localip 192.168.23.20
remoteip 192.168.23.30-39

/etc/ppp/pptpd-options:

name pptpd
refuse-pap
refuse-chap
refuse-mschap
require-mschap-v2
require-mppe-128
proxyarp
nodefaultroute
lock
nobsdcomp
noipx ## you don’t need IPX
mtu 1490 ## may help your linux client from disconnecting
mru 1490 ## may help your linux client from disconnecting

/etc/ppp/options:

lock

/etc/ppp/chap-secrets:

| # Secrets for authentication using CHAP
| # client    server  secret  IP addresses

[username]  pptpd [userpass] *

(The [username] and [userpass] are entries without the brackets.)

Now restart the server with:

$ sudo service pptpd restart

VPN Client Setup:

Four configuration files are involved:

    /etc/ppp/peers/myvpn
    /etc/ppp/options.pptp
    /etc/ppp/chap-secrets
    /etc/ppp/ip-up.local

/etc/ppp/peers/myvpn:

| # replace the bracket paramters with the host name of the VPN server and VPN user
remotename myvpn
linkname myvpn
ipparam myvpn
pty "pptp [vpn server] --nolaunchpppd "
name [username]
usepeerdns
require-mppe
refuse-eap
noauth

| # adopt defaults from the pptp-linux package
file /etc/ppp/options.pptp

/etc/ppp/options.pptp:

lock
noauth
refuse-pap
refuse-eap
refuse-chap
refuse-mschap
nobsdcomp
nodeflate

/etc/ppp/chap-secrets:

| # Secrets for authentication using CHAP
| # client    server  secret  IP addresses
username myvpn password *

/etc/ppp/ip-up.local:

| #!/bin/sh
network=`echo $IPREMOTE | awk -F\. '{print $1"."$2"."$3".0/24"}'`
route add -net $network $IFNAME

Connect the VPN client with:

$ sudo pon myvpn

End the VPN connection with:

$ sudo poff myvpn


Ubuntu tips
-----------

search
:   * whereis document
    * find path -option document
        + eg: find ~ -name .vimrc
    * locate document

```bash
$ lspci # 驱动信息
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor DRAM Controller (rev 06)
00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor PCI Express x16 Controller (rev 06)
00:02.0 VGA compatible controller: Intel Corporation 4th Gen Core Processor Integrated Graphics Controller (rev 06)
00:03.0 Audio device: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor HD Audio Controller (rev 06)
00:14.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB xHCI (rev 05)
00:16.0 Communication controller: Intel Corporation 8 Series/C220 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB EHCI #2 (rev 05)
00:1b.0 Audio device: Intel Corporation 8 Series/C220 Series Chipset High Definition Audio Controller (rev 05)
00:1c.0 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #4 (rev d5)
00:1c.4 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #5 (rev d5)
00:1d.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB EHCI #1 (rev 05)
00:1f.0 ISA bridge: Intel Corporation HM86 Express LPC Controller (rev 05)
00:1f.2 SATA controller: Intel Corporation 8 Series/C220 Series Chipset Family 6-port SATA Controller 1 [AHCI mode] (rev 05)
00:1f.3 SMBus: Intel Corporation 8 Series/C220 Series Chipset Family SMBus Controller (rev 05)
01:00.0 3D controller: NVIDIA Corporation GM107M [GeForce GTX 850M] (rev a2)
07:00.0 Ethernet controller: Qualcomm Atheros QCA8171 Gigabit Ethernet (rev 10)
08:00.0 Network controller: Broadcom Corporation BCM43142 802.11b/g/n (rev 01)
```
### Solve the Wireless

```bash
$ sudo apt-get install bcmwl-kernel-source
$ 无线网卡是BCM4312 802.11b/g
# 以下是我的网卡信息以及网卡安装
08:00.0 Network controller: Broadcom Corporation BCM43142 802.11b/g/n (rev 01)
$ sudo apt-get install Linux-headers$(uname -r | grep -Po "\-[a-z].*")
$ sudo apt-get install build-essential dkms
$ sudo apt-get install dpkg
$ sudo apt-get install bcmwl-kernel-source
```
### 添加开机自启动
```bash
$ sudo gnome-session-properties
```

### Ubuntu 目录结构
|  /bin: bin是Binary的缩写。存放系统中最常用的可执行文件（二进制）。
| /boot: 这里存放的是Linux内核和系统启动文件，包括Grub、lilo启动器程序。
| /dev: dev是Device(设备)的缩写。该目录存放的是linux的外部设备，如硬盘、分区、键盘、鼠标、usb等。
| /etc: 这个目录用来存放所有的系统管理所需要的配置文件和子目录，如passwd、hostname等。
| /home: 用户的主目录，在Linux中，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的。
| /lib: 存放共享的库文件，包含许多被/bin和/sbin中程序使用的库文件。
| /lost+found: 磁盘修复文件,这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些零散文件。
| /media: ubuntu系统自动挂载的光驱、usb设备，存放临时读入的文件。
| /mnt: 作为被挂载的文件系统得挂载点。
| /opt: 作为可选文件和程序的存放目录，主要被第三方开发者用来简易安装和卸载他们的软件。
| /proc: 这个目录是一个虚拟的目录，它是系统内存的映射，我们可以通过直接访问这个目录来获取系统信息。这里存放所有标志为文件的进程，比较cpuinfo存放cpu当前工作状态的数据。
| /root: 该目录为系统管理员，也称作超级权限者的用户主目录。
| /sbin: s就是Super User的意思，这里存放的是系统管理员使用的系统管理程序，如系统管理、目录查询等关键命令文件。
| / srv: 存放系统所提供的服务数据。
| /sys: 系统设备和文件层次结构，并向用户程序提供详细的内核数据信息。
| /tmp: 这个目录是用来存放一些临时文件的，所有用户对此目录都有读写权限。
| /usr: 存放与系统用户有关的文件和目录。
| /usr/bin/应用程序
| /usr/sbin/管理员应用程序
| /usr/lib/应用程序文件
| /usr/share/应用程序资料文件
| /usr/src/应用程序源代码
| /usr/local:这里主要存放那些手动安装的软件，即不是通过“新立得”或apt-get安装的软件。它和/usr目录具有相类似的目录结构。让软件包管理器来管理/usr目录，而把自定义的脚本（scripts）放到/usr/local目录下面
| /usr/local/soft/用户程序
| /usr/temp/临时文件
| /var:动态数据,长度可变的文件，尤其是些记录数据，如日志文件和打印机文件。
| /var/cache: 应用程序缓存目录；
| /var/crash: 系统错误信息；
| /var/games: 游戏数据；
| /var/log: 日志文件；
| /var/mail: 电子邮件；
| /var/tmp: 临时文件目录；
| /temp/临时文件
|
|
| 常用系统服务:
| acpi-support 高级电源管理支持
| acpid acpi守护程序.这两个用于电源管理，非常重要
| alsa 声音子系统
| alsa-utils
| anacron cron的子系统，将系统关闭期间的计划任务，在下一次系统运行时执行。
| apmd acpi的扩展
| atd 类似于cron的任务调度系统。建议关闭
| binfmt-support 核心支持其他二进制的文件格式。建议开启
| bluez-utiles 蓝牙设备支持
| bootlogd 启动日志。开启它
| cron 任务调度系统，建议开启
| cupsys 打印机子系统。
| dbus 消息总线系统(message bus system)。非常重要
| dns-clean 使用拨号连接时，清除dns信息。
| evms 企业卷管理系统（Enterprise Volumn Management system）
| fetchmail 邮件用户代理，用于收取邮件
| gdm gnome登录和桌面管理器。
| gdomap
| gpm 终端中的鼠标支持。
| halt 别动它。
| hdparm 调整硬盘的脚本，配置文件为“/etc/hdparm.conf”。
| hibernate 系统休眠
| hotkey-setup 笔记本功能键支持。支持类型包括： HP, Acer, ASUS, Sony, Dell, 和IBM。
| hotplug and hotplug-net 即插即用支持，比较复杂，建议不要动它。
| hplip HP打印机和图形子系统
| ifrename 网络接口重命名脚本。如果您有十块网卡，您应该开启它
| inetd 在文件“/etc/inetd.conf”中，注释掉所有你不需要的服务。如果该文件不包含任何服务，那关闭它是很安全的。
| klogd 重要。
| linux-restricted-modules-common 受限模块支持。“/lib/linux-restricted-modules/”文件夹中的模块为受限模块。例如某些驱动程序，如果您没有使用受限模块，就不需要开启它。
| lvm 逻辑卷管理系统支持。
| makedev 创建设备文件，非常重要。
| mdamd 磁盘阵列
| module-init-tools 从/etc/modules加载扩展模块，建议开启。
| networking 网络支持。按“/etc/network/interfaces”文件预设激活网络，非常重要。
| ntpdate 时间同步服务，建议关闭。
| pcmcia pcmcia设备支持。
| powernowd 移动CPU节能支持
| ppp and ppp-dns 拨号连接
| readahead 预加载库文件。
| reboot 别动它。
| resolvconf 自动配置DNS
| rmnologin 清除nologin
| rsync rsync守护程序
| sendsigs 在重启和关机期间发送信号
| single 激活单用户模式
| ssh ssh守护程序。建议开启
| stop-bootlogd 在2，3，4，5运行级别中停止bootlogd服务
| sudo 检查sudo状态。重要
| sysklogd 系统日志
| udev & udev-mab 用户空间dev文件系统（userspace dev filesystem）。重要
| umountfs 卸载文件系统
| urandom 随机数生成器
| usplash 开机画面支持
| vbesave 显卡BIOS配置工具。保存显卡的状态
| xorg-common 设置X服务ICE socket。
| adjtimex 调整核心时钟的工具
| dirmngr 证书列表管理工具,和gnupg一起工作。
| hwtools irqs优化工具
| libpam-devperm 系统崩溃之后，用于修理设备文件许可的守护程序。
| lm-sensors 板载传感器支持
| mdadm-raid 磁盘陈列管理器
| screen-cleanup 清除开机屏幕的脚本
| xinetd 管理其他守护进程的一个inetd超级守护程序
|
| 全局配置文件:
| 系统初始化
| /etc/inittab 运行级别、控制台数量
| /etc/timezone 时区
| /etc/inetd.conf 超级进程
| 文件系统
| /etc/fstab 开机时挂载的文件系统
| /etc/mtab 当前挂载的文件系统
| 用户系统
| /etc/passwd 用户信息
| /etc/shadow 用户密码
| /etc/group 群组信息
| /etc/gshadow 群组密码
| /etc/sudoers Sudoer列表（请使用“visudo”命令修改此文件，而不要直接编辑）
| Shell
| /etc/shell 可用Shell列表
| /etc/inputrc ReadLine控件设定
| /etc/profile 用户首选项
| /etc/bash.bashrc bash配置文件
| 系统环境
| /etc/environment 环境变量
| /etc/updatedb.conf 文件检索数据库配置信息
| /etc/issue 发行信息
| /etc/issue.net
| /etc/screenrc 屏幕设定
| 网络
| /etc/iftab 网卡MAC地址绑定
| /etc/hosts 主机列表
| /etc/hostname 主机名
| /etc/resolv.conf 域名解析服务器地址
| /etc/network/interfaces 网卡配置文件 



ref
:   * [CSDN](http://blog.csdn.net/poplong/article/details/8259386) 
