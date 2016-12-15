---
layout: post
title: "How DNS Works"
date: "2016-10-20"
slug: "linux"
description: "The Domain Name System or the DNS is a resolution protocol for mapping the domain name of a server to its ip address. Putting this term in much simpler words, DNS can also be viewed as the system that can help map much difficult to remember IP Addresses to easier to remember domain name. Looking at an example, the domain name, say www.foo.com can have a ipv4 address such as 195.156.7.8 and a much longer (too long) ipV6 address (I am not going to give an example ;)!)."
category:
  - views
  - featured
# tags will also be used as html meta keywords.
tags:
  - examples
  - common_tag
show_meta: true
comments: true
mathjax: true
gistembed: true
published: true
noindex: false
nofollow: false
# hide QR code, permalink block while printing.
hide_printmsg: false
# show post summary or full post in RSS feed.
summaryfeed: false
## for twitter summary card with squared image and page description or page excerpt:
# imagesummary: foo.png
## for twitter card with large image:
# imagefeature: "http://img.youtube.com/vi/VEIrQUXm_hY/0.jpg"
## for twitter video card: (active for this page)
videofeature: "https://www.youtube.com/embed/iG9CE55wbtY"
imagefeature: "http://img.youtube.com/vi/iG9CE55wbtY/0.jpg"
videocredit: tedtalks
---
<style>
p {
  text-align: justify
}</style>

<h1>The Domain Name System</h1>

<p>The Domain Name System or the DNS is a resolution protocol for mapping the domain name of a server to its ip address. Putting this term in much simpler words, DNS can also be viewed as the system that can help map much difficult to remember IP Addresses to easier to remember domain name. Looking at an example, the domain name, say www.foo.com can have a ipv4 address such as 195.156.7.8 and a much longer (too long) ipV6 address (I am not going to give an example ;)!).</p>

<p>So, it is practically not possible for a user to remember about a handful of websites’ IP Addresses. However, one could always remember a memory-friendly domain name such as www.google.com or www.yahoo.com.</p>

<p>This is where the DNS comes into play and believe it or not, the DNS has made lives much more simpler for us. Though the protocol as such is very complex and one could end up reading hours on it, I have created a sequence of events that take place in case of a DNS lookup.This high level overview would at least tell you what the overall mechanism of a DNS request is.</p>

<h1> Overview of the DNS Lookup </h1>

1. Let us start with an example - user types www.google.com on to the web browser and hits enter.<br>
2. This request is passed to the Local Name Server.  The IP address corresponding to this domain name could already be present in the memory/cache or the Local Name Server.<br>
3. If the local name server cannot resolve the IP, then the request is passed to a Resolving Name Server.<br>
4. Then the  Resolving name Server passes the request to a Root Name Server. One of the interesting facts is that there are only 13 Root Name Servers that are present all around the world. If the Root Name Server does not resolve the request, then it is passed to the TLD - or the Top level name Servers.<br>
5. The Top level name servers, again would point to the ANS or the Authoritative Name Servers. This would be the final end-point of this lookup. The Authoritative Name Servers are usually contain the IP Address information for the given domain name.<br>
6. The ANS would then respond to the Resolving Name server with the matching ip for that domain name. Then the Resolving Name Server would pass this information to the Operating System.<br>
7. The Operating System gives this information to the browser and then the browser would then make a connection to this IP Address. This is the end point.<br>


<h1>Summarizing the DNS Lookup</h1>

Browser -> Operating System ->  Local Name Server - > Root Name Server  -> Top Level Domain Name Servers -> Authoritative Name Server -> Operating System -> Browser -> Request the Corresponding IP Address.

This article does not cover all the intricacies of a DNS lookup, but would definitively summarize the overview of a DNS lookup.

<br>
<b>Do you find any typos or disagree with something on this page? Let me know!</b>
