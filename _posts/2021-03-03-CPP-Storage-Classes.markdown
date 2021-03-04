---
layout: post
title: "Storage Classes in CPP (Notes)"
date: "2021-03-03"
slug: "ch"
description: "This post contains notes about the various storage classes in C++ and how they are different from each other. Read more to follow along."

category:
  - CPP
  - Programming-Languages
tags:
  - CPP
  - Programming
show_meta: true
comments: true
mathjax: true
gistembed: true
published: true
noindex: false
nofollow: false
hide_printmsg: false
summaryfeed: false
thumbnail: 
---

<div style="text-align:center"><img src =""/></div><br>

<h2> Storage classes </h2>

Storage classes define the life-time, scope and visibility of variables within a C++ program.
The different Storage Class Specifiers are:

- auto - automatic duration with no linkage
- register - automatic duration with no linkage
- static - static duration with internal linkage
- extern - static duration with external linkage
- mutable - 
- _Thread_local - thread storage duration.


#### Auto
- Default storage specifiers for variables that are delcared locally. 
- Can only be local and inside a function.

{% highlight ruby %}
    {
        int a = 0;
        auto a = 0; // type inference
    }
{% endhighlight %}

