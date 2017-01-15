---
layout: post
title: "Grab API data using the Python Requests Module"
date: "2017-01-14"
slug: "Python Requests Module"
description: "Learn to efficiently grab data using the Python requests module"
category:
  - Python
  - api
tags:
  - Python
  - api

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


<h2> Using Python Request Module to Grab API data. </h2>

The python `requests` module helps us to carry out HTTP operations like POST, GET, PUT or DELETE on a given endpoint. This same module can be used to grab data from any given API endpoint. Now, the end-point that I am using in this post is a sample JSON endpoint - where JSON stands for Javascript Object Notation.


<h2> An example JSON end point ... </h2>

There are tons of sample JSON endpoints that you can use - they are all out there in the web. I am using this one from [here].

{% highlight ruby %}[
{
   "X-Cloud-Trace-Context": "88dcf8a5cdf64009d30f1b35c5e865b3/15181546534373111777",
   "Upgrade-Insecure-Requests": "1",
   "Accept-Language": "en-US,en;q=0.8",
   "Host": "headers.jsontest.com",
   "Referer": "http://www.jsontest.com/",
   "User-Agent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.75 Safari/537.36",
   "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8"
}

{% endhighlight%}

<h2>Using the  requests module ...</h2>
Install the Python requests module if it is not present. Use Python `pip` to install the `requests` module. Eg. `sudo pip install requests`. To tap the example end-point to get api data, we use the requests module as follows.

{% highlight ruby %}

import requests #importing the Python requests module
def get_api_data(url):
  endpoint = requests.get(url) 	#Getting data from specified endpoint using the ‘GET’ operation
  data = endpoint.json()        #process data as JSON object using the json function
  print data[‘Host’]                      #print required data using the key of the JSON object

if __name__ == '__main__':
  get_api_data(‘http://headers.jsontest.com/’)

{% endhighlight%}


[here]: http://headers.jsontest.com/
