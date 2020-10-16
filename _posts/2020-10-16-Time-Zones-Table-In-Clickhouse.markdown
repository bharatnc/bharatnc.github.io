---
layout: post
title: "New time zones table in ClickHouse"
date: "2020-10-16"
slug: "ch"
description: "My recent contribution to ClickHouse introduces a new systems table for timezones. To learn more about this table continue reading this article."

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

<h2> New system.time_zones table in Clickhouse </h2>

In one of my recent contributions to ClickHouse, I helped to add a new table called `system.time_zones` table.

This new table contains the list of `time_zones` that are currently available and supported by the current version of ClickHouse that's running.

*Note:* At the time of writing this post, this feature only works with OS type Linux. For other OS's like Darwin, BSD etc. this new feature is not yet available.

Query for the time_zone information as follows:

{% highlight ruby %}

:) select * from system.time_zones limit 10;

SELECT *
FROM system.time_zones
LIMIT 10

┌─time_zone──────────┐
│ Africa/Abidjan     │
│ Africa/Accra       │
│ Africa/Addis_Ababa │
│ Africa/Algiers     │
│ Africa/Asmara      │
│ Africa/Asmera      │
│ Africa/Bamako      │
│ Africa/Bangui      │
│ Africa/Banjul      │
│ Africa/Bissau      │
└────────────────────┘

10 rows in set. Elapsed: 0.012 sec.

{% endhighlight %}

Useful links to check out:

1. Related [issue] link.
2. Checkout the [main] PR and the [linked] PR for implementation details.
3. [Documentation] for this new table.

[issue]: https://github.com/ClickHouse/ClickHouse/issues/12444
[main]: https://github.com/ClickHouse/ClickHouse/pull/13880
[linked]: https://github.com/ClickHouse/ClickHouse/pull/14030
[Documentation]: https://clickhouse.tech/docs/en/operations/system-tables/time_zones/
