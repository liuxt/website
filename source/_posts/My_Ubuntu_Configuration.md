---
title: My Ubuntu Configuration
date: 2017-08-03 21:12:55
tags:
- ubuntu
---
This is my personal configuration of Ubuntu 16.04 LTS. I decided to write down these steps to remind me what I am going to do after I reinstall my system. In fact, this is my ***THIRD*** time to reinstall Ubuntu 16.04. Maybe I should install Arch or Gentoo as Zhuohua suggested! Operations below are necessary steps to make a Ubuntu System ready to use.

## Configure networks

- Configure network according to [Proxy in CSE](https://ansrlab.org/wiki/everything-you-always-wanted-to-know-about-ansr.html#proxy-in-cse)
- IPV4
	- IP Address: 137.189.XX.XX
	- NetMask: 
	- GateWay: 137.189.91.254
	- DNS Servers: 137.189.91.188, 137.189.91.187


## Install .deb files:
``` bash
$sudo dpkg -i ./name-of-the-file
$sudo apt install -f
```

## Install Sougou Pinyin
[2 Best Chinese PinYin Input Method in Ubuntu 16.04](http://ubuntuhandbook.org/index.php/2016/07/2-best-chinese-pinyin-im-ubuntu-16-04/)

## Update apt-get

``` bash
$sudo apt-get update
```

## Configure Vim

#### Install Vim and Vim-gnome(for clipboard)

``` bash
$sudo apt-get install vim
$sudo apt-get install vim-gnome
```

#### Clone vimrc
In `/home/liuxt` directory(or `~/`), clone vimrc file.

``` bash
$git clone https://github.com/liuxt/vimrc.git
```

Then change directory name to `.vim`

``` bash
$mv vimrc .vim
```

#### PlugInstall 

Go into `vim` and print

``` bash
:PlugInstall
```

#### Special tips for YouCompleteMe
- remember to change gcc version in file `.vim/ycm_extra_conf.py` to the one in your system(gcc 6.1.3 in original file)
- remember to install `python-dev` `python3-dev`
- remember to run python script `~/.vim/plugged/YouCompleteMe/install.sh` by printing:

``` bash
$sh install.sh --clang-completer
```

At last, *DO NOT* power off ubuntu by cutting down power.Believe me, it *WILL CRASH*!



