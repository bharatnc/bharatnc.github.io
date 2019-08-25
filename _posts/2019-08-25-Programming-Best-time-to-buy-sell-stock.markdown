---
layout: post
title: "Best time to buy and sell a stock"
date: "2019-08-25"
slug: "Algorithms"
description: "Solution to solving the problem: best time to buy and sell a stock."
category:
  - Python
  - Algorithms
tags:
  - Python
  - Algorithms

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


<h2>Solution</h2>

{% highlight ruby %}
#!/bin/python3
from sys import maxsize


def determine_best_time_bs(arr):
    curr_min = maxsize
    max_profit = 0
    for i in range(len(arr)):
        if arr[i] < curr_min:
            curr_min = arr[i]
        else:
            if (arr[i] - curr_min) > max_profit:
                max_profit = arr[i] - curr_min

    return max_profit

if __name__ == "__main__":
    print(determine_best_time_bs([7,1,5,3,6,4]))


{% endhighlight%}

