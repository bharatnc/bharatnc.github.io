---
layout: post
title: "Setting up Raspberry Pi 3 as a Wireless Access Point"
date: "2016-06-23"
slug: "rpi"
description: "Setting up your Raspberry Pi 3 as a Wireless Access Point is quite easy. There are so many interesting projects that you can do, if you can play around with this neat little device operating as an access point! I hope that this post will help all its' readers to set up their Pi as a Wireless Access Point and would also help them to start bootstrapping their dream project into place. As a reminder, this setup has only been tested to work with the <b>Raspberry Pi 3</b>"
category:
  - views
  - featured
#tags:
#  - examples
#  - common_tag
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


<div style="text-align:center"><img src ="http://cdn.mos.techradar.com/art/desktop_pcs_and_macs/Raspberry%20Pi/raspberry%20pi%203/hero-970-80.JPG"/></div>
<br/>
<p>
Setting up your Raspberry Pi 3 as a Wireless Access Point is quite easy. There are so many interesting projects that you can do, if you can play around with this neat little device operating as an access point! I hope that this post will help all its' readers to set up their Pi as a Wireless Access Point and would also help them to start bootstrapping their dream project into place. As a reminder, this setup has only been tested to work with the <b>Raspberry Pi 3</b>.
</p>
<h4>Step 1 - Install dnsmasq and hostapd packages</h4>
Start off by installing the required packages using the command `sudo apt-get install dnsmasq hostapd`, these are the only packages that we would need to make this magic happen. The interesting package of interest is the dnsmasq, which is the combined DHCP and DNS server. This can be configured  to be set up an access point.

<h4>Step 2 - Editing some configuration files</h4>
After you are done installing, open the file `/etc/dhcpcd.conf ` using your favorite text editor. In my case I usually use nano, so `sudo nano /etc/dhcpcd.conf`. Next, add `denyinterfaces wlan0` to the end of the file.

Following the previous step, use  the command `sudo vim /etc/network/interfaces` and edit the `wlan0section` so that it looks like this:
{% highlight ruby %}

allow-hotplug wlan0
iface wlan0 inet static
    address 172.24.1.1
    netmask 255.255.255.0
    network 172.24.1.0
    broadcast 172.24.1.255
#wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf

{% endhighlight %}

<h4>Step 3 - Create a new hostapd configuration file to describe your hotspot</h4>

Now, restart dhcpcd service by issuing a `sudo service dhcpcd restart`. Soon after this, reload the configuration for wlan0 with `sudo ifdown wlan0` followed by `sudo ifup wlan0`.
After that, use `sudo vim /etc/hostapd/hostapd.conf` to create a new configuration file  called `hostapd.conf`and add these details:

{% highlight ruby %}

# This is the name of the WiFi interface that we configured above
interface=wlan0
# Use the nl80211 driver with the brcmfmac driver
driver=nl80211
# This is the name of the network
ssid=PiAccess-Point #The name you prefer.
# Use the 2.4GHz band
hw_mode=g
# Use channel 6
channel=6
# Enable 802.11n
ieee80211n=1
# Enable WMM
wmm_enabled=1
# Enable 40MHz channels with 20ns guard interval
ht_capab=[HT40][SHORT-GI-20][DSSS_CCK-40]
# Accept all MAC addresses
macaddr_acl=0
# Use WPA authentication
auth_algs=1
# Require clients to know the network name
ignore_broadcast_ssid=0
# Use WPA2
wpa=2
# Use a pre-shared key
wpa_key_mgmt=WPA-PSK
# The network passphrase
wpa_passphrase=password #The password that you want.
# Use AES, instead of TKIP
rsn_pairwise=CCMP

{% endhighlight %}

<h4>Step 4 - Point your configuration file </h4>

Point the configuration file that you created in Step 4 to the correct path, so that it is recognized on bootup. For this, use `sudo nano /etc/default/hostapd`  to open up the required configuration file and find  `#DAEMON_CONF=""` and replace it with `DAEMON_CONF="/etc/hostapd/hostapd.conf "`.

<h4>Step 5 - Configure one more file - the "dnsmasq" file</h4>

Configure the dnsmasq file. Let us keep the original configuration file. Use `sudo nano /etc/dnsmasq.conf ` and then add the following to the file. If there is already a file, you can erase its’ contents or you  can backup the file using  ` cp or mv ` commands.

{% highlight ruby %}
interface=wlan0      # Use interface wlan0
listen-address=172.24.1.1 # Explicitly specify the address to listen on
bind-interfaces      # Bind to the interface to make sure we aren't sending things elsewhere
server=8.8.8.8       # Forward DNS requests to Google DNS
domain-needed        # Don't forward short names
bogus-priv           # Never forward addresses in the non-routed address spaces.
dhcp-range=172.24.1.50,172.24.1.150,12h # Assign IP addresses between 172.24.1.50 and 172.24.1.150 with a 12 hour lease time
{% endhighlight %}

<h4>Step 6 - Let's add some ip table rules</h4>

Use `sudo sh -c "echo 1 > /proc/sys/net/ipv4/ip_forward" ` to do an ipV4 forwarding.

Next add some iptables rules - mainly for sharing the wlan0 interface with eth0 interface.
{% highlight ruby %}

sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
sudo iptables -A FORWARD -i eth0 -o wlan0 -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i wlan0 -o eth0 -j ACCEPT

{% endhighlight %}

<h4>Step 7 - Finally there!</h4>


These configurations have to be saved. Otherwise, we have to enter them everytime we reboot the Raspberry Pi. Let us do a `sudo sh -c "iptables-save > /etc/iptables.ipv4.nat"`  to save these settings to the file `/etc/iptables.ipv4.nat`. Then open  rc.local as `sudo nano /etc/rc.local` and just above the line with exit 0 add `iptables-restore < /etc/iptables.ipv4.nat`

Perform a `sudo service hostapd start` and a `sudo service dnsmasq start` and you should be good to go! Find the wireless hotspot name and connect to it using the credentials that you have given.

Special thanks to Phil Martin on his [original post] - on using the Raspberry Pi 3 as a hotspot.

<br>
<b>Do you find any typos or disagree with something on this page? Let me know!</b>

[original post]: https://frillip.com/using-your-raspberry-pi-3-as-a-wifi-access-point-with-hostapd/
