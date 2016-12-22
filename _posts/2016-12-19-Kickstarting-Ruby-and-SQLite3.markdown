---
layout: post
title: "Kickstarting  database skills with simple Ruby and Sqlite3"
date: "2016-12-19"
slug: "Ruby and Sqlite3"
description: "Get started with Ruby and SQLite3. A fairly straight forward tutorial guiding beginners to begin exploring the world of Ruby and SQLite3. Not to forget, there would be more posts related to SQLite3 based on Python and Ruby programming languages."
category:
  - Ruby
  - SQLite3
tags:
  - Ruby
  - SQLite3

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

<h2> The requisites </h2>

I assume that you have Ruby installed on your computer. The latest one (version) is always the best. After we have all that setup neatly,  one more package -  Sqlite3 for Ruby, has to be installed. This is a Ruby specific library that will help us to utilize all of Sqlite3’s functions. Go ahead and install this package called `ruby-sqlite3` using your package manager. In my case I used `sudo apt-get install ruby-sqlite3` to install this package.

<h2> Writing some code … </h2>

Having made those installations, let us write some code to create a very simple database and a table using Ruby and our Sqlite3 library.

<h4>Code:</h4>

<b>Creating a simple database called tut1.db:</b>

{% highlight ruby %}

require ‘sqlite3’
db = SQLite3::Database.open “tut1.db”

{% endhighlight %}
We use the SQLite3 object that the Rubys’ Sqlite3 library provides, to create a new database called `tut1.db`.


<b>Creating a simple table inside tut1.db:</b>

For creating a table or inserting entries into the table, the `execute` operation of the SQLite is used.

{% highlight ruby %}

db.execute "CREATE TABLE IF NOT EXISTS prolang(Id INTEGER PRIMARY KEY, name TEXT, Year INT)"

{% endhighlight %}
The above query then creates a table called “prolang”. The table has the following schema:

Id - (unique identifier) - Primary key. <br>
name - (name of the programming language) - a TEXT field. <br>
Year - (year in which the language first appeared) - a INT field. <br>

You can go about modifying this table. It is completely up to you to discover the SQLite world out there! A good starting point would be SQLite3’s documentation [here].

<b>Inserting some values into our table:</b>

Now that we have our table lined up, we can go about inserting some values into our database using the execute statement.
db.execute “INSERT INTO prolang VALUES (1, “Ruby”, 1995)”

<h2>Putting it all together …</h2>

Let us go ahead and put the code supporting the  creation of the database, creation of table and the insertion of the values together.

{% highlight ruby %}

require ‘sqlite3’
db = SQLite3::Database.open “tut1.db”
db.execute "CREATE TABLE IF NOT EXISTS prolang(Id INTEGER PRIMARY KEY, name TEXT, Year INT)"
db.execute “INSERT INTO prolang VALUES (1, “Ruby”, 1995)”

{% endhighlight %}


This snippet now gives a handy database and a table where we can store our data for persistence. I hope that this post has given all of you a  good kickstart using Sqlite with Ruby. In the upcoming posts, we would discuss about more operations involving SQLite3 with Ruby and Python programming languages.


[here]: https://www.sqlite.org/docs.html
