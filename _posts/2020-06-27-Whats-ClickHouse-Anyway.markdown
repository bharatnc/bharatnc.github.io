---
layout: post
title: "What's ClickHouse anyway ?"
date: "2020-06-27"
slug: "ch"
description: "A brief introduction to ClickHouse if you haven't heard of it. We discuss about potential use-cases and understand the difference between row and columnar stores."

category:
  - Databases
  - Distributed-Systems
  - Analytics
tags:
  - ClickHouse
  - Databases
  - DataEngineering
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

<div style="text-align:center"><img src ="https://github.com/ClickHouse/ClickHouse/raw/master/website/images/logo-400x240.png"/></div><br>

<h2> ClickHouse - the blazing fast analytics columnar database! </h2>

I'm writing this short blog post in which I want to very briefly talk about ClickHouse and explain what it is. I aim to 
keep this post short and potentially discuss use cases in which it shines and where one should use it or not use it. 
For all those who already know what ClickHouse is, you can probably skip this blog post. <br>

If you haven't already noticed the section heading, ClickHouse is a columnar analytics database by Yandex and is
blazing fast and also is [distributed]. If you are interested in a few [benchmarks] comparing other analytics 
databases that are also columnar, you can check them out.

<h2> Columnar database </h2>

ClickHouse's [introduction] page has really good content on what a columnar database is and how it's different from a row based
database. Nevertheless I would like to very briefly explain what it's by using a very simple example. <br>

Let's consider a simple employee database which contains these fields `employee_name`, `employee_join_date`, `employee_dob` and `employee_yoe`. <br>

<h3>Row based store </h3>

{% highlight ruby %}
id  |  employee_name | employee_join_date | employee_dob | employee_yoe |
1   |   foo          |  2020-06-20        | 01-01-1975   |  4           |
2   |   bar          |  2020-06-21        | 01-01-1985   |  3           |
5   |   foobar       |  2020-06-20        | 06-01-1995   |  2           |
{% endhighlight %}

<h3> Column based store </h3>

{% highlight ruby %}
fields              |   1            |   2           |   3          | 
employee_name       |   foo          |  bar          |   foobar     |
employee_join_date  |   2020-06-20   |  2020-06-21   |   01-01-1985 |
employee_yoe        |   01-01-1975   |  01-01-1985   |   06-01-1995 |             
{% endhighlight %}

As you can see, the row style arrangement is similar to how relational databases like Postgres, MySQL, etc organize data.
Every row has an id and a set of fields. In this case, these are the employee details which are all stored next to each other. <br> 

However, in the case of columnar style of arrangement, the various fields are actually stored separately and the data from the
fields are stored together as columns. For instance `employee_name` and `employee-yoe` are stored separately and the values of these
fields are stored together. <b>

<h2> What's ClickHouse good for ? </h2>
* When you need really high insertion rates. <br>
* When data written doesn't need to be modified. <br>
* Data consistency is not a hard requirement. <br>
* Large number of rows for only a small sub-set of columns. <br>

So, generally, ClickHouse suits all kinds of analytical uses cases. These are use cases that involve 
ingesting a large amount of data, processing and retrieving a small subset of fields from a larger set of fields.

<h2> What's ClickHouse not so good for ? </h2>
* High requirement for data consistency. <br>
* If data that's inserted needs to be updated. <br>
* When database transactions are necessary. <br>

Therefore, ClickHouse won't suit if the requirement is that data that's read should always be consistent. It also wont' work 
out well if queries are of transactional nature and involve deleting or mutating the state of data. Databases like Postgres 
and MySQL are better suited for such scenarios. <br>

<h2> So how Columnar data arrangement makes ClickHouse faster for analytics use-case ? </h2>

The ClickHouse [introduction] doc provides a really good visualization of why Columnar stores are faster for
retrieving data. Nevertheless, I'll try to explain.<br>

<h4> Retrieval </h4>

For analytics use-case, when only a small subset of columns are needed from a larger number of columns, these columns can 
be read separately in chunks and this is exactly what ClickHouse does.<br>

Let's imagine using row based databases for analytics use-cases where you only need a few fields from a larger list of fields. 
In this case, all N rows and M fields in the database need to be read to return only a few fields. This is expensive and 
this is why ClickHouse shines when it comes to processing a large number of columns as data can be read in packets.<br>

<h4> Insertion through MergeTree Engine </h4>

ClickHouse uses the [MergeTree] Database Engine (one of the main engines that it supports) which is responsible for inserting 
data into the table in chunks and later merges them in the background. I'll attempt to explain MergeTree Engine in detail in 
another post, but basically, this is what really makes insertions so fast. <br>

That sums up this post. You might have noticed a few links while reading through this blog post. Those links will bring you to 
ClickHouse's official documentation on the topics that we just discussed. If you are interested in exploring ClickHouse for your 
projects, that's a good place to start learning more about it. 

[benchmarks]: https://clickhouse.tech/benchmark/dbms/
[distributed]: https://clickhouse.tech/docs/en/engines/table-engines/special/distributed/
[introduction]: https://clickhouse.tech/docs/en/
[MergeTree]: https://clickhouse.tech/docs/en/engines/table-engines/mergetree-family/mergetree/
