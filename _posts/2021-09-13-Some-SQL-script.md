---
layout: post
title: Some useful SQL scripts
description: A collection of SQL scripts.
tags: 
- sql
- database
---
# Collection of some SQL script

## How to find the number of bytes per row
``` tsql
-- This query will return which table uses the most space and start from there
<<<<<<< HEAD
--  In some case, this query is faster than the select COUNT(*) from *TABLE_NAME*
=======
>>>>>>> 93e9ded5c40fae3b97e8a648a275734ac0a21574
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

## How to delete large amount of data from tables

### If you want to delete all data

``` tsql
Truncate table TABLE_Name
```

Once the table is truncated, the database might not release the space immediately. In this case, run the following command

``` tsql
DBCC SHRINKDATABASE (N'YouDbName')
```

### If you want to delete records meet certain criteria

``` tsql
DECLARE @Deleted_Rows INT;
SET @Deleted_Rows = 1;


WHILE (@Deleted_Rows > 0)
  BEGIN

   BEGIN TRANSACTION

   -- Delete some small number of rows at a time
     DELETE TOP (10000)  LargeTable 
     WHERE readTime < dateadd(MONTH,-7,GETDATE())

     SET @Deleted_Rows = @@ROWCOUNT;

   -- Below two line will ensure the log file from increasing
   COMMIT TRANSACTION
   CHECKPOINT -- for simple recovery model
END
```