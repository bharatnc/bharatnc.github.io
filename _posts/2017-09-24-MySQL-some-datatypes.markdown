---
layout: post
title: "MySQL some character types"
date: "2017-09-24"
description: "What's different between CHAR, VARCHAR and NVARCHAR when using MySQL? This post briefly explains the differences that I did not know when I dived into MySQL. I hope that this post would be interesting for someone to read and find more about!"
category:
  - MySQL
tags:
  - MySQL

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


### The data-types CHAR and VARCHAR

VARCHAR consists of characters that can be of variable length ranging from 0 - 65,535 characters. On the other hand, CHAR consists of characters that range from 0 - 255 characters. So, where does the difference between CHAR and VARCHAR come from?

VARCHAR requires 1 byte or 2 byte prefix that denotes the number of bytes that are in the value stored. This means that any data that is stored under the VARCHAR datatype needs a 1 byte prefix up to a length of 255 bytes and 2 bytes prefix upto a length of 255.

Some examples:

1. 'abc' needs 3 bytes as a CHAR datatype and 4 bytes as a VARCHAR datatype.
2. 'ab' needs 2 bytes as a CHAR datatype and 3 bytes as a VARCHAR datatype and so on - I guess you get the idea here!

The one  or byte(s) prefix contains the length of the value that is being stored under the VARCHAR data type. 

#### The Padding stuff.

Whenever you declare something like CHAR(40) and try to store a string like "iamawesome" the reality is that the string right-padded with spaces i.e spaces for the remaining characters of what is left over of 40 - length of (iamawsome). When the string is retrieved, these spaces are striped off.

### The difference between VARCHAR and NVARCHAR

VARCHAR can be used to store variable length data and cannot store the unicode format. On the other hand, "N" in NVARCHAR stands for the  `n` in u`n`icode data. It can be used to store [unicode] data - this means that VARCHAR needs 1 byte per character and NVARCHAR needs 2 bytes per character to store the same string. This would result in NVARCHAR using up double the amount of space to store the same amount of data unicode/non-unicode that it takes for VARCHAR to store (except in reality there is no way for VARCHAR to store unicode data - just stating "unicode/non-unicode" for example sake).

[unicode]: https://en.wikipedia.org/wiki/Unicode