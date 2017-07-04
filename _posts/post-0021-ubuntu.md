---
title: Ubuntu
date: Tue Jul  4 13:38:56 CST 2017
---

Ubuntu 16.04 LST
================

Change sources
----
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

## Git

```sh
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

## Remove Amazon link
`sudo apt-get remove unity-webapps-common`

## Install Java

### Install Oracle Java

[Oracle](http://www.oracle.com/technetwork/cn/java/javase/downloads/jdk8-downloads-2133151-zhs.html)

```sh
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

```sh
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```
## Install Sublime Text 3
```sh
sudo add-apt-repository ppa:webupd8team/sublime-text-3    
sudo apt-get update    
sudo apt-get install sublime-text 
```
## Install axel (like wget)

`sudo apt-get install axel`

## Install CMake and Qt Creator
`sudo apt-get Install cmake qtcreator`

## Install lnav (review log)

`sudo apt-get Install lnav`

## Install unrar

`sudo apt-get Install unrar`

## Ubuntu 16.04 L2TP

long long age,use `sudo apt-get Install l2tp-ipsec-vpn`,but 
now Ubuntu 16.04 remove it.

```sh
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

## Install YaHeiConsolas

```sh
wget http://www.mycode.net.cn/wp-content/uploads/2015/07/YaHeiConsolas.tar.gz
tar -zxvf YaHeiConsolas.tar.gz
sudo mkdir -p /usr/share/fonts/vista
sudo cp YaHeiConsolas.ttf /usr/share/fonts/vista/
sudo chmod 644 /usr/share/fonts/vista/*.ttf
cd /usr/share/fonts/vista/
sudo mkfontscale && sudo mkfontdir && sudo fc-cache -fv # refresh and install
```
and download unity-tweak-tool like `sudo apt-get install unity-tweak-tool` change font .

## Flatabulous theme

```sh
sudo add-apt-repository ppa:noobslab/themes
sudo apt-get update
sudo apt-get install flatabulous-theme
```
and icons

```sh
sudo add-apt-repository ppa:noobslab/icons
sudo apt-get update
sudo apt-get install ultra-flat-icons
```

## Compile vim by Ubuntu

### Install lib

```sh
sudo apt-get install libncurses5-dev libgnome2-dev libgnomeui-dev \
    libgtk2.0-dev libatk1.0-dev libbonoboui2-dev \
    libcairo2-dev libx11-dev libxpm-dev libxt-dev python-dev \
    python3-dev ruby-dev lua5.1 lua5.1-dev git
```
### Remove old vim

```sh
dpkg -l | grep vim
sudo dpkg -p vim vim-common vim-run
```

### Download vim and install

```sh
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

```sh
sudo apt-get install checkinstall
cd vim
sudo checkinstall
```

### Set vim as default editor
```sh
sudo update-alternatives --install /usr/bin/editor editor /usr/bin/vim 1
sudo update-alternatives --set editor /usr/bin/vim
sudo update-alternatives --install /usr/bin/vi vi /usr/bin/vim 1
sudo update-alternatives --set vi /usr/bin/vim
```

