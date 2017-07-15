---
title: Bash
date: Sat Jul  8 20:16:21 CST 2017
---

Bash
====

高效编写 Bash 脚本的 10 个技巧
:   * 脚本里多写注释
        ```bash
        # $1 是变量
        ```
    * 运行失败时退出
        ```bash
        set -o errexit
        # or
        set -e
        ```
    * Bash 未声明变量时退出
        ```bash
        set -o nounset
        # or
        set -u
        ```
    * 使用双引号来引用变量
        ```bash
        #!/bin/bash
        # 若命令失败让脚本退出
        set -o errexit
        # 若未设置的变量被使用让脚本退出
        set -o nounset
        echo "Names without double quotes"
        echo
        names="Tecmint FOSSMint Linusay"
        for name in $names; do
          echo "$name"
        done
        echo
        echo "Names with double quotes"
        echo
        for name in "$names"; do
        echo "$name"
        done
        exit 0
        ```
    * 在脚本里使用函数
        ```bash
        function check_root(){
          command1;
          command2;
        }
        # or
        check_root(){
          command1;
          command2;
        }
        # 写成单行，每个命令后都要用终止符号:
        check_root(){ command1; command2; }
        ```
    * 字符串比较时用 `=` 而不是 `==`
        ```bash
        value1 = "tec.com"
        value2 = "font.com"
        if [ "$value1" = "$value2" ]
        ```
    * 用 `$(command)` 而不是老旧的 `command` 来替换
        ```bash
        user = 'echo "$UID"'
        user = $(echo "$UID")
        ```
    * 用 readonly 来声明静态变量
        ```bash
        readonly passwd_file = "/etc/passwd"
        readonly group_file = "/etc/group"
        ```
    * 环境变量用大写，自定义变量用小写
        ```bash
        nikto_file = "$HOME/Downloads/Compressed/program/nino.pl"
        perl "$nikto_file" -h "$1"
        ```
    * 总是对长脚本进行调试。

ref
:   * [伯乐在线](http://blog.jobbole.com/111514/)


