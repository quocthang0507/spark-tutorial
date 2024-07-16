# Apache Spark - Introduction

## Apache Spark

Apache Spark which is based on Hadoop MapReduce, which is a lightning-fast cluster computing technology, designed for fast computation.

![Spark built on hadoop](https://www.tutorialspoint.com/apache_spark/images/spark_built_on_hadoop.jpg)

|Standalone|Hadoop Yarn|Spark in MapReduce (SIMR)|
|:---:|:---:|:---:|
|Spark occupies the place on top of HDFS (Hadoop Distributed File System) and space is allocated for HDFS explicitly. Spark and MapReduce will run side by side to cover all spark jobs on cluster.|Spark runs on Yarn without any pre-installation or root access required. It helps to integrate Spark into Hadoop ecosystem or stack and allows other components to run on top of stack.|Spark in MapReduce is used to launch spark job in addition to standalone deployment. User can start Spark and uses its shell without any administrative access.|

![Spark components](https://www.tutorialspoint.com/apache_spark/images/components_of_spark.jpg)

|Spark SQL|Spark Streaming|MLlib (Machine Learning Library)|GraphX|
|:---:|:---:|:---:|:---:|
|SchemaRDD is a data abstraction which provides support for structured and semi-structured data.|It ingests data in mini-batches and performs RDD (Resilient Distributed Datasets) transformations on those mini-batches of data.|A distributed machine learning framework above Spark because of the ditributed memory-based Spark architecture.|GraphX is a distributed graph-processing framework which provides an API for expressing graph computation.|
||The underlying general execution engine for spark platform that all other functionality is built upon. It provides in-memory computing and referencing datasets in external storage systems.|||

## Features of Apache Spark

> * Speed − Spark helps to run an application in Hadoop cluster, up to 100 times faster in memory, and 10 times faster when running on disk. This is possible by reducing number of read/write operations to disk. It stores the intermediate processing data in memory.
>
> * Supports multiple languages − Spark provides built-in APIs in Java, Scala, or Python. Therefore, you can write applications in different languages. Spark comes up with 80 high-level operators for interactive querying.
>
> * Advanced Analytics − Spark not only supports ‘Map’ and ‘reduce’. It also supports SQL queries, Streaming data, Machine learning (ML), and Graph algorithms.

## Summarization

- **Hadoop and Spark**: Hadoop is widely used for data analysis due to its scalability and fault tolerance. Spark, introduced by Apache, speeds up Hadoop's computational processes and can operate independently of Hadoop.

- **Spark Features**: Spark offers in-memory cluster computing, which enhances processing speed. It supports various workloads, including batch applications, iterative algorithms, interactive queries, and streaming.

- **Components of Spark**: Spark Core, Spark SQL, Spark Streaming, MLlib, and GraphX are key components, each serving different purposes like structured data support, streaming analytics, machine learning, and graph processing.

- **Deployment**: Spark can be deployed in multiple ways, leveraging Hadoop for storage and using its own cluster management for computation.