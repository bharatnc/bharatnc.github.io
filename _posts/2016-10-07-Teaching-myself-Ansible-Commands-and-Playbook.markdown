---
layout: post
title:  "Teaching myself Ansible  - Using Ansible Commands"
date: "2016-10-07"
slug: "ansible"
description: "In the  previous post, we have discussed about setting up bare-metal BeagleBone Black servers and installing Ansible on it. In this post, we would be setting up and configuring Ansible and be trying out a few Ansible commands."

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

<div style="text-align:center"><img src ="https://codereviewvideos.com/blog/wp-content/uploads/2015/06/ansible-tutorial.gif"/></div><br>

In the [previous] post, we have discussed about setting up bare-metal BeagleBone Black servers and installing Ansible on it. In this post, we would be setting up and configuring Ansible and be trying out a few Ansible commands.

<h2> Starting out with Ansible </h2>
Before we are ready to run our first Ansible command, there are a few configurations that  have to set up. Open up the shell on your master machine - in my case, this is going to be an Ubuntu Virtual Machine (only machine on which Ansible is installed). In order to start our automation, we should manipulate the default "hosts" file that comes with  the installation process. This is the file, where the overall configuration and grouping of your servers will be specified. Taking a backup of this file is often a really good practice. Use `sudo cat /etc/ansible/hosts >> /etc/ansible/hosts.original` to copy the contents of the original file into a new backup file.

<h2> The "hosts" file </h2>

The "hosts" file contains all the important information that is required by Ansible, to run tests and installations on your severs. An example of my  "hosts" file is as shown below. Since, you have copied the contents of the original "hosts" file, go ahead and start with a blank "hosts" file,  by deleting all of its contents. Use your favorite text-editor such as the `vim or nano` to do this. You can then go ahead writing your new "hosts" file. Let us take the entire chunk of this "hosts" file and then analyze what is happening in it.

{% highlight ruby %}
[foo]
10.0.0.10
10.0.0.22

[foo:vars]
ansible_ssh_user=foo

{% endhighlight %}

In the above example, the `[foo]` refers to a group of servers. In my case I am having just two of them. If you have more than two machines, you could go ahead and create several other groups such as [database], [loadbalancers],[webservers] and so on. Next, you have to specify the IPs that would be under this group. Just add the IPs of the machines(slaves) that you are using. Next, we would specify some vars like the username for these machines under `[groupname:vars]`. In my case, this would be `[foo:vars]`. Under this, just specify the username that Ansible would use to ssh - here, the user is  `foo`. With this, we have successfully created the  basics of a "hosts" file.

<h2> Running your first Ansible command </h2>

Having created the hosts configuration file, we can go ahead and run some installations on these servers. For this, let us consider a simple command.<br>

`ansible all -s -m shell -a 'ls -al'`

The above command uses `all`. This means that it references all the machines in all the user groups. This is something that we described in our "hosts" file. In this case, we just have one user group by the name `[foo]`. Alternatively, you could specify the name of the group too. Then comes the `-s` option, this instructs Ansible to use sudo previeges on the command that is being executed. The next important one to notice is the `-a` - this is used to pass arguments to the target machines. In this example, the argument is going to be a `ls -al`. Running the above command would result in an output as shown below.


{% highlight ruby %}


10.0.0.10 | SUCCESS | rc=0 >>
total 96
drwxr-xr-x 13 debian debian 4096 Apr 23  2014 .
drwxr-xr-x  5 root   root   4096 Sep 17 07:41 ..
drwx------  3 debian debian 4096 Apr 23  2014 .dbus
drwxr-xr-x  2 debian debian 4096 Sep 17 01:06 Desktop


10.0.0.22 | SUCCESS | rc=0 >>
total 116
drwxr-xr-x 15 debian debian 4096 Apr 23  2014 .
drwxr-xr-x  7 root   root   4096 Oct  5 07:20 ..
drwx------  3 debian debian 4096 Oct  1 18:55 .ansible
drwxr-xr-x  4 debian debian 4096 Oct  1 08:33 ansible-pi


{% endhighlight %}


I have just cut short the list that showed up when I ran the command. But for the general idea, I guess this should be enough.


<h2> Running some installations </h2>

Now similarly, you could also run some installations like the one shown below:

` ansible all -s -m shell -a 'apt-get install -y htop'` <br>

In this case, the above command will install `htop` on the machines. Remember to include the `-y` parameter to force a [Y/n] option to the installation. If everything were to be correct, you would observe an output like this:<br>

{% highlight ruby %}
10.0.0.22 | SUCCESS | rc=0 >>
Reading package lists...
Building dependency tree...
Reading state information...
Suggested packages:
  strace ltrace
The following NEW packages will be installed:
  htop
0 upgraded, 1 newly installed, 0 to remove and 194 not upgraded.
Need to get 0 B/70.6 kB of archives.
After this operation, 188 kB of additional disk space will be used.
Selecting previously unselected package htop.
(Reading database ... 64223 files and directories currently installed.)
Unpacking htop (from .../htop_1.0.1-1_armhf.deb) ...
Processing triggers for man-db ...
Processing triggers for desktop-file-utils ...
Setting up htop (1.0.1-1) ...

10.0.0.10 | SUCCESS | rc=0 >>
Reading package lists...
Building dependency tree...
Reading state information...
Suggested packages:
  strace ltrace
The following NEW packages will be installed:
  htop
0 upgraded, 1 newly installed, 0 to remove and 194 not upgraded.
Need to get 0 B/70.6 kB of archives.
After this operation, 188 kB of additional disk space will be used.
Selecting previously unselected package htop.
(Reading database ... 64448 files and directories currently installed.)
Unpacking htop (from .../htop_1.0.1-1_armhf.deb) ...
Processing triggers for man-db ...
Processing triggers for desktop-file-utils ...
Setting up htop (1.0.1-1) ...


{% endhighlight %}

If it had been already installed, then the following would be the output.

{% highlight ruby %}

10.0.0.22 | SUCCESS | rc=0 >>
Reading package lists...
Building dependency tree...
Reading state information...
htop is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 194 not upgraded.

10.0.0.10 | SUCCESS | rc=0 >>
Reading package lists...
Building dependency tree...
Reading state information...
htop is already the newest version.
0 upgraded, 0 newly installed, 0 to remove and 194 not upgraded.
{% endhighlight %}


So, these commands are just similar to ordinary shell commands, but what makes Ansible so much more powerful? The Ansible specific commands and Playbooks of course! Let us look into these in detail, in the coming articles. Hope that this article helped all of you to get started with Ansible.


<br>
<b>Do you find any typos or disagree with something on this page? Let me know!</b>
