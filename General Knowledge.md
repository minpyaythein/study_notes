#### Latency is about how fast a system responds to a single request while throughput is about how many requests a system can handle every second.

Latency is usually inversely proportional to throughput i.e. optimizing latency results in killing throughput and vice versa. For example, caching in database layer for better latency results in lower memory available for other tasks, reducing the amount of what a system can handle. Finding the right balance is very important.

#### IOPS vs. Throughput

The Disk IOPS Describes the count of input/output operations on the disk per seconds, regardless block size.

The disk throughput describes how many data may be transferred per second, so the block size play a huge role upon calculating the throughput required by app.

Let's consider as the sample the 3000 IOPS and SQL database engine, the block size in terms of db engine is called the page size and for SQL Server it's equal to 8 KB. If you wish to calculate the actual throughput, if the IOPS defined, you will end up with the formula below:

throughput = [IOPS] _ [block size] = 3000 _ 8 = 24 000 KB/s = 24 MB/s
