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

### Why to install in ubuntu
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
./configure --with-features=huge \
            --enable-multibyte \
            --enable-rubyinterp \
            --enable-pythoninterp \
            --with-python-config-dir=/usr/lib/python2.7/config-x86_64-linux-gnu \
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
