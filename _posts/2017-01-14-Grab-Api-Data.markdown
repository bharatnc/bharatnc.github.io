---
layout: post
title: "Grab API data using the Python Requests Module."
date: "2017-01-14"
slug: "Python requests"
description: "The python ‘requests’ module helps us to carry out HTTP operations like POST, GET, PUT or DELETE on a given endpoint. Learn to efficiently grab data using the Python requests module."
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


<h2>Using Python Request Module to Grab API data. </h2>


The python ‘requests’ module helps us to carry out HTTP operations like POST, GET, PUT or DELETE on a given endpoint. This same module can be used to grab data from any given API endpoint. Now, the end-points that I am using in this post are sample JSON endpoints - where JSON stands for Javascript Object Notation.


<h2>An example JSON end point… </h2>


There are tons of sample JSON endpoints that you can use - out there on the web. I am using this one from [here].

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


<h2>Using the  requests module ... </h2>

Install the Python requests module if it is not present. Use `pip` to install the requests module. Eg. `sudo pip install requests`.

1. To tap the example end-point to get api data, we first start by importing the requests module.
`import requests`. <br>
2. Next use the get method to get the contents of the url (endpoint). endpoint = requests.get(url).<br>
3. This data that is contained in the variable called `endpoint` has to be serialized into a JSON Object. For this purpose, we use the Python `json` module. `data = endpoint.json()`<br>
4. This data is now a representation of the Python dictionary data-structure. The value can be accessed using the key. In this example, we use `Host` as the key `print data[‘Host’]`.  This prints out the value corresponding to the key `Host`.


 <h2> Putting it all together </h2>

 Putting it all together into a function called `get_api_data()` which takes an url (JSON endpoint). In this case, the code prints out the value corresponding to our key called `Hosts`.

{% highlight ruby %}
import requests #importing the Python requests module
def get_api_data(url):
  endpoint = requests.get(url)
  data = endpoint.json()
  print data[‘Host’]
if __name __ == '__main__':
  get_api_data(‘http://headers.jsontest.com/’)

{% endhighlight%}

This example gives us a very high-level overview of how the python `requests` module can be used to grab data from APIs.





[here]: http://headers.jsontest.com/
