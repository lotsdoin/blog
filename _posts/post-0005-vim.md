---
title: Vim
date: 2017-05-15 18:19:42
---

# Vim

## List Number
```sh
:%s/^/\=line(".").",\t"/  最正规的方法 
:let i=0|g/^/s//\=i.','/ |let i+=1 不用函数的方法
:g/^/exec "s/^/".strpart(line(".")."   ", 0, 4)  
:g/^/exec "s/^/".line(".")."\t"
```
## Compete

```vimL
自动补全                        `CTRL + N/P`
整行补全                        `CTRL-X CTRL-L`
根据当前文件里关键字补全        `CTRL-X CTRL-N`
根据字典补全                    `CTRL-X CTRL-K`
根据同义词字典补全              `CTRL-X CTRL-T`
根据头文件内关键字补全          `CTRL-X CTRL-I`
根据标签补全                    `CTRL-X CTRL-]`
补全文件名                      `CTRL-X CTRL-F`
补全宏定义                      `CTRL-X CTRL-D`
补全vim命令                     `CTRL-X CTRL-V`
用户自定义补全方式              `CTRL-X CTRL-U`
拼写建议                        `CTRL-X CTRL-S` 
```
```vimL
:%s/.*HREF="\([^"]*\)".*$/\1/
:-r document
:r !date
:!date
```
