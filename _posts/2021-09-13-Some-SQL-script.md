---
layout: post
title: Some useful SQL scripts
description: A collection of SQL scripts.
tags: 
- sql
- database
---
# Collection of some SQL script

``` tsql
-- This query will return which table uses the most space and start from there
select 
    o.name, 
    max(s.row_count) AS 'Rows',
    sum(s.reserved_page_count) * 8.0 / (1024 * 1024) as 'GB',
    (8 * 1024 * sum(s.reserved_page_count)) / (max(s.row_count)) as 'Bytes/Row'
from sys.dm_db_partition_stats s, sys.objects o
where o.object_id = s.object_id
AND o.type='U' -- Only want to know the user table
group by o.name
having max(s.row_count) > 0
order by GB desc
```
