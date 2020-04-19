---
title: mac-alias-rm
date: 2020-04-18 09:39:55
tags: mac 
---
上次误删`rm -rf `写了自己的项目，也没有备份。使用了一些文件恢复程序也没有用。于是就想使用**trash**代替**rm**，把文件放入到废纸篓🗑️中这样就可以还原文件不怕误删。

> [trash](https://hasseg.org/trash/)，[作者博客](http://hasseg.org/blog/post/406/trash-files-from-the-os-x-command-line/)是通过**Finder**来删除文件，这样文件就会放到废纸篓了
## 设置别名
1. 安装**trash**,需要先安装**brew**,juti1
```shell
brew install trash
```
2. 设置**trash**的别名为**rm**
```shell
vim ~/.bash_profile;
# 文件底部添加
alias rm = "trash -F"
```
> 设置 `-F` 放到废纸篓的文件才有放回原处。
3. 使命令生效
```shell
source ~/.bash_profile
```
- 这样使用**rm**实际执行的是**trash**。到这边一步执行是有问题的，重新启动终端的化就会失效，这里需要另外设置下才可以一直有效

## 设置别名一直有效
1. 新建**bashrc**文件,添加`alias rm = "trash -F"`到底部
```shell
vim ~/.bashrc 
alias rm = "trash -F"
```
2. 在**bash_profile** 添加使**bashrc**生效的命令。
```
vim ~/.bash_profile;
source ~/.bashrc
```
- 到这一步使用`bash`的就算重新打开终端**alias**也是有效，但是使用了**zsh**的就不行了。
## **zsh**使用
- 创建**zshrc** 文件，将使`bash_profile`生效的命令写入，这样使用**zsh**的也就都可以了
```bash
vim zshrc 
test -f ~/.bash_profile  && source ~/.bash_profile
```
