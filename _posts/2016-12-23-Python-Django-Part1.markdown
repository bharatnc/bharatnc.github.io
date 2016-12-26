---
layout: post
title: "Python Django - Part1 - Getting started"
date: "2016-12-19"
slug: "Django-part1"
description: "This Django blog series aims to familiarize those who are new to Django - help them get started quickly and have a simple web page up and running. This part of the tutorial gives us a gist of how to get started and getting the first app up and running. "
category:
  - Python
  - Django
tags:
  - Python
  - Django

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


This Django blog series aims to familiarize those who are new to Django - help them get started quickly and have a simple web page up and running. This part of the tutorial gives us a gist of how to get started and getting the first app up and running.

<h3>Requisites …</h3>

As a prerequisite, install Python and Python pip (Django uses Python). To install python-pip refer [this] documentation. Based on the kind of Operating system that you are using, follow the installation guide that is the most relevant to you. In this tutorial I am using a PC with Ubuntu 14.04 LTS. All my references relate to this version and only the installations are platform dependent. The actual application and how it works is uniform across all the platforms.



<h3>Creating a Virtual Environment and installing Django locally.</h3>

1. Install python [virtual environment] package. Use sudo pip install virtualenv to install this package. <br>
2. Create a new virtual environment using sudo virtualenv <name of the env>. <br>
3. Activate the virtual environment using the source bin/activate from within the virtual environment folder. <br>
4. To make a local installation of the Django framework - use sudo pip install django==1.9. In this case it installs the 1.9 version of Django. <br>
5. After this you can start a new Django Project using `sudo django-admin startproject <project-name>`. This would be the main project directory. <br>
6. For every additional app that would be created, we can create a new app using `sudo django-admin startapp <app-name>`.
The main project would be the master and would control all the applications that are running under it. The following is a rough directory structure for the application that I have: <br>

{% highlight ruby %}

venv
  - bin
  - include
  - lib
  - local
  - pip-selfcheck.json
  - testprj
        --  testapp
        --  db.sqlite3
        --  manage.py
        --  testprj

{% endhighlight %}
Where `testprj` is the project that we created and the `testapp` is the app that we created.



<h3> Running the first web-app … </h3>

After creating a new project, navigate to the project folder and use `sudo python manage.py` runserver to run the Django webserver. By default it would run at http://127.0.0.0.1:8000 - in other words, at the localhost across port number 8000. Boom! We have got our first Django app running. If you browse to the link - you would see a pretty much plain page that says 'It worked! Congratulations on your first Django-powered page.'


[this]: https://pip.pypa.io/en/stable/installing/
[virtual environment]: http://docs.python-guide.org/en/latest/dev/virtualenvs/
