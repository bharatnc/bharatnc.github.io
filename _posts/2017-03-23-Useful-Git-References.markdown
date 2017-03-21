---
layout: post
title: "Useful Git References that I use."
date: "2017-03-21"
slug: "Git Ref"
description: "Git is really handy when you are developing a project. I am including the references that I often use to manage my repositories. I feel that these are quite handy and can help anyone in becoming more efficient in Managing their repos."
category:
  - Python
  - API
tags:
  - Python
  - API

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


Git is really handy when you are developing a project. I am including the references that I often use to manage my repositories. I feel that these are quite handy and can help anyone in becoming more efficient in Managing their repos.

##What will you do if you want to merge, edit or squash requests?

Surprisingly, merging, squashing and editing requests are really easy.

1. Use the rebase command to change whatever you want to change. Eg: `git rebase -i HEAD~8`. You can increase or reduce the HEAD size based on the number of commits that you want to edit.

Use this useful link [here]. This is in detail and is really helpful. <br>

Once you run these commands, you will be able to see you list of commits: <br>

Eg:

{% highlight ruby %}

edit f9h2g0d first commit
edit b6h2l0e second commit
edit k2o1d1d third commit

{% endhighlight%}

Next you will see a list of commands that you can use to modify these commits.

{% highlight ruby %}

# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell

{% endhighlight%}

You can perform edit, squash etc on these commits which are listed in order. For an example using a squash would combine all the commits into a single one:


{% highlight ruby %}

edit f9h2g0d first commit
squash b6h2l0e second commit
squash k2o1d1d third commit

{% endhighlight%


##What will you do if you want to test out your markdown?

Writing Git markdown for you repository can one of the most important things that you might have to do - if you want other to use/contribute to your code. Writing a markdown and pushing it to Github and only later realizing that the markdown is not proper, can be really irritating. Afterall, you can't afford to squash and edit your commits to fix your markdown. It is'nt very efficient or professional. What you can instead do is to use a online markdown editor. <br>

This [markdown editor] is really nice and will help you visualize you markdown.

##Do you want to add Emojis to your Git Markdown?

Use this [emoji cheat-sheet].  It is neat and handy!



## First of all,beginning to write markdowns?

If you are just beginning to write markdowns, then you should consider this [Markdown-Cheetsheet]. It is really useful for creating a efficient markdown.

[here]: https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History
[markdown editor]:http://dillinger.io/
[emoji cheat-sheet]:https://www.webpagefx.com/tools/emoji-cheat-sheet/
[Markdown-Cheetsheet]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet