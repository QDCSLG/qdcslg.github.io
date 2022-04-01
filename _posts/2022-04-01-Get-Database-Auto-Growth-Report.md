---
layout: post
title: How to increase the diskspace after Ubuntu VM using Quick create by Hyper-V 
description: By default, when creating a Ubuntu VM on Hyper-V machine, one 10Gb of the disk is available. It is not enough
tags: 
- sql
---


``` sql
DECLARE @current_tracefilename VARCHAR(500);
DECLARE @0_tracefilename VARCHAR(500);
DECLARE @indx INT;
SELECT @current_tracefilename = path
FROM sys.traces
WHERE is_default = 1;
SET @current_tracefilename = REVERSE(@current_tracefilename);
SELECT @indx = PATINDEX('%\%', @current_tracefilename);
SET @current_tracefilename = REVERSE(@current_tracefilename);
SET @0_tracefilename = LEFT(@current_tracefilename, LEN(@current_tracefilename) - @indx) + '\log.trc';
SELECT DatabaseName, 
       te.name, 
       Filename, 
       CONVERT(DECIMAL(10, 3), Duration / 1000000e0) AS TimeTakenSeconds, 
       StartTime, 
       EndTime, 
       (IntegerData * 8.0 / 1024) AS 'ChangeInSize MB', 
       ApplicationName, 
       HostName, 
       LoginName
FROM ::fn_trace_gettable(@0_tracefilename, DEFAULT) t
     INNER JOIN sys.trace_events AS te ON t.EventClass = te.trace_event_id
WHERE(trace_event_id >= 92
      AND trace_event_id <= 95)
ORDER BY t.StartTime;
```

Let’s understand the query quickly.

- We use the `sys.trace_events` catalog view to get SQL Server events and filter those events for our SQL Server database. In the following query, we can see the trace event id 92 to 95 with their description. The event id and description do not change with the new versions of SQL Server

- We use sys.traces catalog view to get details of current running traces on the system. If the is_default property value for any running trace is 1, it shows for the default trace. We also get the trace file location using this catalog view
- We use the fn_trace_gettable table-valued function to read the content of a trace file and return it in a tabular format. In this query, it reads the default trace file and gives us the required information