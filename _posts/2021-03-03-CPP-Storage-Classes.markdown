---
layout: post
title: "Storage Classes in CPP (Notes)"
date: "2021-03-03"
slug: "ch"
description: "This post contains notes (organized from various sources to make it easier to understand storage classes) about the various storage classes in C++ and how they differ from each other. Please read more to follow along."

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

#### Register

- Used to directly define `local` variables to directly store them inside registers instead of the RAM.
- Varaible max size = register size and doesn't take a reference (`&` -  unary reference operator).

{% highlight ruby %}
    {
        register int a = 10;
    }
{% endhighlight %}

#### Static 

- Keeps the variable in existence until the execution of the program ends.
- Local variables made static retain their value between function calls.
- Global variables can also be declared using static. 
- Global static variables have a scope which is limited to the file in which they are declared.

{% highlight ruby %}
    {
        static int a = 10;
    }
{% endhighlight %}

#### Extern

- Gives the reference of a variable that is visible to all program files.
- Can't be initialized.
- Used when a global variable is to be used by multiple files. 

{% highlight ruby %}
    {
        extern int a = 10;
    }
{% endhighlight %}


#### Mutable

- Mutable allows the value of class member to be overridden using a const specifier.
- Can't be used with members that are declared as static, const or as a reference.

{% highlight ruby %}
{
    class Foo
    {
       public:
       Foo() : x(4), y(5) { };
       mutable int x;
       int y;
    };
    
    int main()
    {
       const Foo var2;
       var2.x = 2;
       var2.y = 3; /// cannot do this. This will error.
    }
}
{% endhighlight %}
