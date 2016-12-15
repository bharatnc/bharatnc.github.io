---
layout: post
title: "How to use Netstat - Cheat Sheet"
date: "2016-10-01"
slug: "linux"
description: "Netstat stands for network statistics. This is a Linux command line application tool, that is really handy for getting information about network statistics and services running in any  machine. Trying to learn this tool, I ended up preparing a cheat sheet, which I am going to share here. As an advice, I would always recommend referring the <b>Linux manpage</b> for learning this tool the right-way. Once you have learnt the tool, this cheat sheet can come-in handy at most of the times."
category:
  - views
  - featured
#tags:
  #- examples
  #- common_tag
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

<h2>What is Netstat ?</h2>
Netstat stands for "network statistics". This is a Linux command line application tool, that is really handy for getting information about network statistics and services running in any  machine. Trying to learn this tool, I ended up preparing a cheat sheet, which I am going to share here. As an advice, I would always recommend referring the Linux manpage for learning this tool the right-way. Once you have learnt the tool, this cheat sheet can come-in handy at most of the times.

<h2>The Commands Cheat Sheet</h2>

<h4>List all ports</h4>
`sudo netstat -a | more`

<h4>List all tcp-ports </h4>

`sudo netstat -at`

<h4> Listing to a custom port </h4>

`sudo netstat -nlp | grep :53`<br>
`sudo lsof -i :80 | grep LISTEN`<br>
`sudo netstat -an | grep :80`

<h4>List all udp-ports </h4>

`sudo netstat -au`

<h4>List all ports that are listening</h4>

`sudo netstat -l`

<h4>List all TCP ports that are listening</h4>

`sudo netstat -al`


<h4>List all UDP ports that are listening</h4>

`sudo netstat -au`

<h4>List all Linux ports that are listening</h4>

`sudo netstat -lx`

<h4> List statistics </h4>
`sudo netstat -s`

<h4> List statistics for TCP ports </h4>
`sudo netstat -st`

<h4> List statistics for UDP ports </h4>
`sudo netstat -su`

<h4>Finding the port on which a program is running on</h4>

`sudo netstat -ap | grep ssh`

<h2>Other common prefix/suffixes</h2>


<li> <b>-c</b>     for continuous mode (Eg: netstat -c).
<li> <b>-n</b>     used for displaying numerical addresses of ports.
<li> <b>-v</b>     used for displaying verbose information.
<li> <b>-s</b>     to report statistics (Eg: used above in examples).
<li> <b>-e</b>     to report extended information.
<li> <b>-p</b>     display the PID and program name running on every socket.
<li> <b>-T</b>     handy when trimming occurs for long addresses. Prevents trimming.
<li> <b>State</b>  used for knowing about the state of a a socket.
<li> <b>User</b>   used to know the user/who owns the socket.
<li> <b>PID</b>    used to display the Process ID or PID that is using a socket.
<li> <b>FLAGS</b>  can be used to display information about the status of a connection.
<li> <b>RefCnt</b> can be used to get the reference count for the processes attached to a socket.
<br>
<br>
So, those are the most commonly used commands. Knowing these would help you to manage this tool quite well. If you want to be an expert at this, then a more comprehensive source such as the Linux manpage for netstat, would definitely help anybody.

<br>
<br>
<b>Do you find any typos or disagree with something on this page? Let me know!</b>
