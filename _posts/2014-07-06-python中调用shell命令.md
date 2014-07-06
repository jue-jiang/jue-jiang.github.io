---
published: true
layout: post
title:  python中调用shell命令
date:   2014-07-06 20:24
categories: jekyll update
---

python支持直接调用shell命令的方式，这个程序的编写带来很大方便,比如可以直接通过调用R脚本来进行绘图。对于shell中的执行的命令，通常有两个值，一个是命令的执行状态，另一个是命令的执行结果。这里总结了python调用shell以及如何获得命令执行状态和执行结果的方式

##方法一：os.system
os.system是不能将返回结果保存到变量中的，适合修改类型的命令
import os
a=os.system("mkdir test")
a的值为0，表示命令成功执行

##方法二：subprocess
通过subprocess可以在当前进程中新建进程，并在新的进程中执行命令。采用subprocess.Popen方法可以获得命令执行状态和执行结果。os.popen在2.6之前[2]也可以用来实现相同的功能，但是在2.6之后已经deprecated了[1]。
stackoverflow中的回答已经给出了使用subprocess获得命令执行状态和执行结果的方式[4]，具体是
>>> import subprocess
>>> process=subprocess.Popen("ls -al",stdout=subprocess.PIPE,shell=True)
或者 process=subprocess.Popen(["ls","-al"],stdout=subprocess.PIPE)
>>> result=process.communicate()
>>> process.returncode
0
>>> result[0]
result 长度为2，第一个是stdout,第二个是stderr

[1][python subprocess.Popen vs os.popen - Stack Overflow](http://stackoverflow.com/questions/17916876/python-subprocess-popen-vs-os-popen)
[2][Python执行系统命令的方法 os.system()，os.popen()，commands - renwofei423的个人空间 - 开源中国社区](http://my.oschina.net/renwofei423/blog/17403)
[3][Python标准库06 子进程 (subprocess包) - Vamei - 博客园](http://www.cnblogs.com/vamei/archive/2012/09/23/2698014.html)
[4][How to get exit code when using Python subprocess communicate method? - Stack Overflow](http://stackoverflow.com/questions/5631624/how-to-get-exit-code-when-using-python-subprocess-communicate-method)


