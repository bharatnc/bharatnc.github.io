---
layout: post
title: "Short post on running background processes"
date: "2017-09-12"
slug: "background and nohup"
description: "This is a very very short post for running background processes. What does nohup does and how it is different from running a process by using &. Short read."
category:
  - Linux
tags:
  - Linux

show_meta: true
comments: true
mathjax: true
gistembed: true
published: true
noindex: false
nofollow: false
hide_printmsg: false
summaryfeed: false
---


<style>
p {
  text-align: justify
}</style>


### Running processes in a shell

If you want to run a process in a shell and want to continue working on other development work, then, one usually would use the "&" operator appended to the end of the application that they are wanting to run. So, what does "&" do?

### Using &.
The "&" usually is used like this : `python sample.py &`. This creates a child process under the existing shell and returns after the child process completes. The command usually runs in a sub-shell. When you close the main terminal, then all these processes receive a `SIGHUP` signal and are automatically terminated.

### Using nohup as opposed to &

The "nohup" keyword is a more professional way to run an application. These can be services or other programs that should remain open and be relatively stable - unlike when running them using a `&` operator. <br>

`nohup` when used, changes the PPID of the process to (1), or in other words, it is made as an init process and not a child process of the main shell. Also, any SIGHUP signal to that process would be ignored when run as a `nohup` job.
	

