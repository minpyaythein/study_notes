# General Knowledge

#### Latency is about how fast a system responds to a single request while throughput is about how many requests a system can handle every second.

Latency is usually inversely proportional to throughput i.e. optimizing latency results in killing throughput and vice versa. For example, caching in database layer for better latency results in lower memory available for other tasks, reducing the amount of what a system can handle. Finding the right balance is very important.

#### IOPS vs. Throughput

The Disk IOPS Describes the count of input/output operations on the disk per seconds, regardless block size.

The disk throughput describes how many data may be transferred per second, so the block size play a huge role upon calculating the throughput required by app.

Let's consider as the sample the 3000 IOPS and SQL database engine, the block size in terms of db engine is called the page size and for SQL Server it's equal to 8 KB. If you wish to calculate the actual throughput, if the IOPS defined, you will end up with the formula below:

throughput = [IOPS] _ [block size] = 3000 _ 8 = 24 000 KB/s = 24 MB/s

#### While IOPS tell us how many actual operations we can perform per second, throughput tells us how much data can be transferred in the same time. Latency, however, tells us how long we have to wait for this operation to be performed (or finished, depending on what type of latency you're looking for)

#### Method Monitoring

RED Method happens on Application side.
Rate or throughput: request per second
Errors: Failed requests i.e., HTTP 500
Duration: Latency or Transaction Response Time

USE Method happens on Infrastructure side.
Utilization i.e., CPU, Memory, Disk Usage
Saturation: Network queue length i.e., when network is fully utilized and no space for the next one, the network packets would queue up the length of that queue.
Errors i.e., Disk write error

Four Golden Signals Method (RED+S)

Core web vitals are also called frontend part of a web app.

#### Monitoring is not equal to Observability.

Observability tells you why an issue occurred and better suited for modern, complex and distributed systems.

Monitoring lets you decide what to keep an eye on before collecting data and better suited for monolithic architecture and only tells when an issue occurred.

#### Types of Telemetry Data

MELT: Metric, Event, Log and Trace.

Traces show exactly where the request has gone through and then where it may have failed.
