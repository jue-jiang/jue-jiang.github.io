---
published: true
layout: post
date: 2014-7-27 16:57
categories: jekyll update
---


   在使用mininet仿真的时候，遇到了需要多次修改系统参数，之后再运行iperf测量带宽。如果多次直接使用server.sendCmd('iperf -s')命令的话，会遇到类似assert waiting的错误，因此需要在完成一次带宽测试之后关闭iperf server的进程。
   
   也尝试了其它几种方式，目前确认下面代码段中的方法是有效的。
   
   server.sendCmd("iperf -s")
   
   pids_string=server.pexec('pidof iperf')
   
   print pids_string
   
   print server.pexec('kill '+pids_string[0])
   
   print server.pexec('pidof iperf')
   
   print server.waitOutput()
   
   print server.waiting
