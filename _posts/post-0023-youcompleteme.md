---
title: YouCompleteMe
date: 2017-07-08
---

YouCompleteMe
=============

Install vundle
--------------

```bash
$ mkdir -p ~/.vim/bundle
$ cd ~/.vim/bundle
$ git clone https://github.com/VundleVim/Vundle.vim
$ sudo vim ~/.vimrc
add

set nocompatible " be iMproved, required
filetype off " required
" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')
" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'
" All of your Plugins must be added before the following line
call vundle#end() " required
filetype plugin indent on " required
```
Install 依赖
-----------
```bash
$ sudo apt-get install build-essential cmake
$ sudo apt-get install python-dev python3-dev
```
Install YouCompleteMe repo
-------------------------

use PluginInstall install YCM, or `sudo git clone https://github.com/Valloric/YouCompleteMe.git ~/.vim/bundle/`

```bash
$ cd ~/.vim/bundle/YouCompleteMe/
$ git submodule update --init --recursive
```
Compile YouCompleteMe
---------------------
C# support: install Mono and add --omnisharp-completer when calling ./install.py.
Go support: install Go and add --gocode-completer when calling ./install.py.
TypeScript support: install Node.js and npm then install the TypeScript SDK with npm install -g typescript.
JavaScript support: install Node.js and npm and add --tern-completer when calling ./install.py.
Rust support: install Rust and add --racer-completer when calling ./install.py.

if you stop in download clang-4.0, you can add `--system-libclang` when you calling ./install.py.Absolutely, use `sudo apt-get isntall clang` install it in your PC.
It's my,`sudo ./install.py --clang-completer --gocode-completer  --system-libclang`.

Config your .vimrc
------------------
When you use it after you will get a warning.`still no falgs, no completions yet`.
solve use follow steps.
```bash
$ cp ~/.vim/bundle/YouCompleteMe/third_party/ycmd/examples/.ycm_extra_conf.py ~/.vim/
$ sudo vim ~/.vimrc
add follow:

let g:ycm_server_python_interpreter='/usr/bin/python'
let g:ycm_global_ycm_extra_conf='~/.vim/.ycm_extra_conf.py'
```
