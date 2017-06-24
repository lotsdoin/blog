---
title: Sublime
date: 2017-06-06
---

Sublime text 3
==============

[Sublime Text 3](http://www.sublimetext.com/3)

:   * ` Ctrl + '` take out Console
    * [Packagecontrol](https://packagecontrol.io/installation#st3) take it in Console and reboot

        ```python
        import urllib.request,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by) 
        ```

    * Emmet: write HTML and CSS

Emment

:   * `! + Tab` or `html:5 + Tab` build a HTML fragment.
    * `div*4 + Tab`
        
        ```html
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        ```

    * `span.menu#name + Tab`

        ```html
        <span class="menu" id="name"></span>
        ```

    * `span.span${span$$}*5 + Tab`

        ```html
        <span class="span1">span01</span>
        <span class="span2">span02</span>
        <span class="span3">span03</span>
        <span class="span4">span04</span>
        <span class="span5">span05</span>
        ```

    * `section>h2+p*3 + Tab`

        ```html
        <section>
            <h2></h2>
            <p></p>
            <p></p>
            <p></p>
        </section>
        ```
    * `ul>li*2.item>h2+img[src="image-$.jpg"] + Tab`

        ```html
        <ul>
        <li>
            <div class="item">
                <h2></h2>
                <img src="image-1.jpg" alt="">
            </div>
        </li>
        <li>
            <div class="item">
                <h2></h2>
                <img src="image-2.jpg" alt="">
            </div>
        </li>
        </ul>
        ```

Useful-tips

:   * (Snap Views)分屏显示 
    * switchover view or file-switching `Ctrl + p`
    * Goto Symbols `Ctrl + r`
    * Multi-Edit(多行编辑) `Ctrl + click`
        + ctrl + d: 选中光标所占的文本，继续操作则会选中下一个相同的文本。
        + ctrl + click: 单击想要编辑的每一个地方，都将创建一个光标
        + ctrl + shift + f 和 alt + enter: 在你的文件查找一个文本，然后将其全部选中
    * ctrl+l 选中整行，继续操作则继续选择下一行，效果和 shift+↓ 效果一样。
    * :w
    ctrl+shift+l 先选中多行，再按下快捷键，会在每行行尾插入光标，即可同时编辑这些行。
    * ctrl+alt+↑ 或 ctrl+alt+鼠标向上拖动 向上添加多行光标，可同时编辑多行。
    * ctrl+alt+↓ 或 ctrl+alt+鼠标向下拖动 向下添加多行光标，可同时编辑多行。
    * shift+↑ 向上选中多行。
    * shift+↓ 向下选中多行。
    * repalce `Ctrl + h`

