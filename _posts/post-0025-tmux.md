---
title: Tmux
date: Sat Jul  8 21:12:43 CST 2017
---

Tmux
====

Install
-------

```bash
$ git clone https://github.com/tmux/tmux.git
$ cd tmux
$ sh autogen.sh
$ ./configure && make
$ sudo make install
or
$ sudo checkinstall
It's simple to control.
```

Session
-------

------------      ------------
change Session      prefix s
leave Session       prefix d
rename Session      prefix $
------------      ------------

Window
------

------------        ------------
new Window          prefix c
change Window       prefix space
close Window        prefix &
change by number    prefix number
------------        -------------

Pane
----

-------------        --------------
change to next       prefix o
view Pane number     prefix q
| Pane               prefix "
--- Pane             prefix %
Zoom Pane            prefix z
-------------        --------------


