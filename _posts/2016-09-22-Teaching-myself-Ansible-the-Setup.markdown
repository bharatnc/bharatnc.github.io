---
layout: post
title: "Teaching myself Ansible  - Setting up bare-metal severs using BeagleBone Blacks"
date: "2016-09-27"
slug: "ansible"
description: "I decided to teach myself Ansible, which I wanted to have hands-on for a long time. I had to search through the web, Ansible documentation pages and many other sources to get a grip on the tool. Thanks to Ansible - the tool was not too complex and was quite easy to learn. I decided to gather some of my notes to write this article. Hopefully, someone who wants to learn Ansible, will find this page useful. In this article, I would go about setting up my servers and then install Ansible on them."

category:
  - Automation

tags:
  - Ansible
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
<div style="text-align:center"><img src ="https://codereviewvideos.com/blog/wp-content/uploads/2015/06/ansible-tutorial.gif"/></div><br>

<h2> Ansible - the easy open-source automation tool </h2>
I decided to teach myself Ansible, which I wanted to have hands-on for a long time. I had to search through the web, Ansible documentation pages and many other sources to get a grip on the tool. Thanks to Ansible - the tool was not too complex and was quite easy to learn. I decided to gather some of my notes to write this article. Hopefully, someone who wants to learn Ansible, will find this page useful. In this article, I would go about setting up my servers and then install Ansible on them.<br>

<h2> Using bare-metal BeagleBone Black severs</h2>
To start off, one has to use servers to play with Ansible. This can be as simple as a couple of Virtual Machines, spun up using Virtual Box or VM Ware. On the contrary, I decided to use some bare-metal power, to check out Ansible. I used a couple of BeagleBone Blacks to act as slave servers! My laptop (Ubuntu 14.04) or a similar VM would then be the master.<br>

<h2> The Network Setup </h2>
As mentioned earlier, I used a couple of BeagleBone Blacks. Used Ethernet cables connect the boards to my router. In my case, I had more than 2 unused Ethernet ports  on my router. If you do not, I would recommend you to use one of the standard network switches available on market. This would extend the available number of Ethernet ports. I also used a USB-Hub to power up my BeagleBone Blacks. The next task would be to find out the IP addresses of these boards. I logged on to my routers' homepage at the default IP assigned to my router (depends on the ISP), here it was 10.0.0.1. Having done so, I had the list of devices connected to my router. I then looked up for my  device IP Addresses using the hostname - "beaglebone" in this case.<br>

<h2> Ansible - uses SSH!</h2>

Having found your IP addresses for your BeagleBone Blacks, I spun up a new Virtual Machine (Ubuntu 14.04)  and started to generate ssh-key pairs. Before learning about ssh-key pairs, I would like to mention that Ansible works on the `ssh protocol` to gain an access over your servers. ssh-key pairs usually allow the user of a particular machine to ssh into a given target machine, without entering the password for that machine.<br>

<h2> Generating a ssh-key pair </h2>
To generate a ssh key pair, let us consider an example. In my case, I have machine A - (VM) and machines B and C (BeagleBone Blacks). If I want to do a password-less ssh from my VM into one or both of the BeagleBones, I would have to generate a private and public ssh key pairs and place the public key on both of the BeagleBone Blacks. To do so, cd `~/.ssh` (on your master VM) and use `ssh-keygen` command to generate a private and public key pair. Depending upon how you name your key, you would have a file called `some_name.pub`. This is the public key that will be kept on the bare-metal servers - BeagleBones. We can then copy the content of the public key file by opening it using the `nano or vim` editors. After doing this, ssh into the BeagleBones and create a new files under `.\ssh` folder and give them any name you want(bb_key in my case). Next, you would be able to see another file by the name `authorized_keys` under the same directory. Using `cat bb_key >> authorized_keys` copy the content of your key file that you had created into the authorized_keys file. This has to be done for both the BeagleBones. Having done this, you can now reboot both the machines and can try ssh'ing into them without a password. Not working? You can read  [this], to get a greater insight on this part. Hopefully, this would help most of you to make it work - after all, your machine setup can be very different from mine!<br>

<h2> Installing Ansible on your VM - and only on your VM</h2>
Yes, Ansible has to be only installed on one machine - ideally the master machine. After doing that, you can control all the other machines (which we would discuss about). On your VM, go forward and add the Ansible repository using the ppa tool. Start-off with these commands:
<br>
1. `sudo apt-get update`<br>
2. `sudo apt-get install software-properties-common`<br>
3. `sudo apt-add-repository ppa:ansible/ansible`<br>
4. `sudo apt-get update`<br>
5. `sudo apt-get install ansible`<br>

Yay! This would now complete your installation of Ansible. You now have Ansible on your master machine and you can also ssh onto the target machines, without the need to enter a password - so can Ansible! In the next article, I would try to control my bare-metal servers using this cool tool! This would include setting up the hosts file and installing basic programs on your servers. Hopefully, I can also write something about how to use Ansible playbooks!

<br>
<b>Do you find any typos or disagree with something on this page? Let me know!</b>

[this]: https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2
