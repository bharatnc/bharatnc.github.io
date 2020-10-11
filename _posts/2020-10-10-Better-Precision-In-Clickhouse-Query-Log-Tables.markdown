---
layout: post
title: "Better precision in ClickHouse system.query_log and system.query_thread_log tables"
date: "2020-10-10"
slug: "ch"
description: "My recent contribution to ClickHouse introduces microseconds precision to system.query_log and system.query_thread_log tables. Continue reading for more details."

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
thumbnail: https://github.com/ClickHouse/ClickHouse/raw/master/website/images/logo-400x240.png
---

<div style="text-align:center"><img src ="https://github.com/ClickHouse/ClickHouse/raw/master/website/images/logo-400x240.png"/></div><br>

<h2> ClickHouse - Better precision for system.query_log and system.query_thread_log tables. </h2>

Recently I contributed to ClickHouse where I added microseconds precision to several of the timing fields in the ClickHouse systems tables. In this post, I wish to highlight a few specific fields that were added to the `system.query_log` and the `system.query_thread_log` tables. Namely:

<ul>
    <li> event_time_microseconds </li>
    <li> query_start_time_micnroseconds </li>
</ul>

These new fields are of the `DateTime64` type. The `event_time` and `query_start_time` which are already present and are of `DateTime` type.
These new fields simply append the microseconds part of the timespec to the DateTime format as shown below:


{% highlight ruby %}

SELECT 
    query_id,
    query_start_time,
    query_start_time_microseconds
FROM system.query_log
LIMIT 3

┌─query_id─────────────────────────────┬────query_start_time─┬─query_start_time_microseconds─┐
│ df11cd7c-52c7-4e12-ba2f-0e12017d2dcb │ 2020-09-04 10:36:54 │    2020-09-04 10:36:54.809193 │
│ df11cd7c-52c7-4e12-ba2f-0e12017d2dcb │ 2020-09-04 10:36:54 │    2020-09-04 10:36:54.809193 │
│ 5b2b6719-6ba0-480b-8f9f-dbca41c6cb71 │ 2020-09-04 10:36:59 │    2020-09-04 10:36:59.538415 │
└──────────────────────────────────────┴─────────────────────┴───────────────────────────────┘

3 rows in set. Elapsed: 0.018 sec. 
{% endhighlight %}

{% highlight ruby %}

SELECT 
    query_id,
    query_start_time,
    query_start_time_microseconds
FROM system.query_thread_log
LIMIT 3

┌─query_id─────────────────────────────┬────query_start_time─┬─query_start_time_microseconds─┐
│ df11cd7c-52c7-4e12-ba2f-0e12017d2dcb │ 2020-09-04 10:36:54 │    2020-09-04 10:36:54.900885 │
│ df11cd7c-52c7-4e12-ba2f-0e12017d2dcb │ 2020-09-04 10:36:54 │    2020-09-04 10:36:54.899900 │
│ df11cd7c-52c7-4e12-ba2f-0e12017d2dcb │ 2020-09-04 10:36:54 │    2020-09-04 10:36:54.900338 │
└──────────────────────────────────────┴─────────────────────┴───────────────────────────────┘

3 rows in set. Elapsed: 0.018 sec. 
{% endhighlight %}


With these new fields, there would be better and more accurate introspection into query timings. This is especially useful for debugging failure scenarios.

If you're interested in learning more about the implementation details, please checkout my main [PR] and other linked PRs to that main PR.

[PR]: https://github.com/ClickHouse/ClickHouse/pull/14252

