# Resilient Distributed Datasets (RDD)

## Resilient Distributed Datasets (Bộ dữ liệu phân tán linh hoạt)

RDD is a fundamental data structure of Spark. It is an immutable distributed collection of objects. Each dataset in RDD is divided into logical partitions, which my be computed on different nodes of the clusters. RDDs can contain any type of Python, Java, or Scala objects, including user-defined classes.

RDD is a read-only, partitioned collection of records. RDD is a fault-tolerant collection of elements that can be operated on in parallel.

There are two ways to create RDDs - **parallelizing** an existing collection in driver program, and **referencing a dataset** in an external storage system.

## Data Sharing is slow in MapReduce

MapReduce is widely adopted for processing and generating large datasets with a parallel, distributed algorithm on a cluster. It allows users to write parallel computations, using a set of high-level operators, without having to worry about work distribution and fault tolerance.

In most current frameworks, the only way to reuse data between computations (e.g. ) is to write it to an external stable storage system (e.g. HDFS).

Data sharing is slow in MapReduce due to replication, serialization, and disk IO. In most of the hadoop applciations, they spend more than 90% of the time doing HDFS read-write operations.

### Iterative operations

![Iterative operations on MapReduce](https://www.tutorialspoint.com/apache_spark/images/iterative_operations_on_mapreduce.jpg)

The above illustration explains how the current framework works, while doing the iterative operations on MapReduce. This incurs substantial overheads due to data replication, disk I/O, and serialization, which makes the system slow.

### Interactive operations

![Interactive operations on MapReduce](https://www.tutorialspoint.com/apache_spark/images/interactive_operations_on_mapreduce.jpg)

User runs ad-hoc queries on the same subset of data. Each query will do the disk I/O on the stable storage, which can dominate application execution time.

## Data sharing using Spark RDD

RDD supports in-memory processing computation. It stores the state of memory as an object across the jobs and the object is sharable between those jobs.

### Interative operations on Spark RDD

![Interative operations on Spark RDD](https://www.tutorialspoint.com/apache_spark/images/iterative_operations_on_spark_rdd.jpg)

The illustration given above shows the iterative operations on Spark RDD. It will store intermediate results in a distributed memory instead of stable storage (disk) and make the system faster.

If the distributed memory (RAM) is not sufficient to store intermediate results (State of the JOB), then it will store those results on the disk.

### Interactive operations on Spark RDD

![Interactive operations on Spark RDD](https://www.tutorialspoint.com/apache_spark/images/interactive_operations_on_spark_rdd.jpg)

The above illustration shows interactive operations on Spark RDD. If different queries are run on the same set of data repeatedly, this particular data can be kept in memory for better execution times.

## Summarization

Here are the key points from the current page:

- **RDD Overview**: Resilient Distributed Datasets (RDD) are immutable, distributed collections of objects in Apache Spark, supporting in-memory processing for faster computations.
- **Creation Methods**: RDDs can be created by parallelizing existing collections or referencing external storage systems like HDFS.
- **Efficiency**: RDDs improve efficiency over traditional MapReduce by reducing data replication, serialization, and disk I/O.
- **Persistence**: RDDs can be persisted in memory or on disk for faster access during iterative and interactive operations.
