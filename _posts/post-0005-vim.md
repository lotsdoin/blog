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
