# Core Programming

## Spark shell

Open Spark shell:

```bash
spark-shell
```

Create a simple RDD:

```bash
$ scala> val inputfile = sc.textFile("input.txt")
inputfile: org.apache.spark.rdd.RDD[String] = input.txt MapPartitionsRDD[1] at textFile at <console>:23
```

## RDD transformations

RDD transformations return pointer to new RDD and allow you to create dependencies between RDDs. Each RDD in dependency chain has a function for calculating its data and has a pointer to its parent RDD.

Spark won't executed unless you call some transformation or action that will trigger job creation and execution. So, RDD transformation is a step in a program telling Spark how to get data and what to do with it.

Given below is a list of RDD transformations:

| Transformation       | Description |
|----------------------|-------------|
| **map(func)**        | Applies a function to each element in the RDD. |
| **filter(func)**     | Selects elements that meet a specific condition. |
| **flatMap(func)**    | Similar to map, but each input item can be mapped to 0 or more output items. |
| **groupByKey()**     | Groups all values with the same key. |
| **reduceByKey(func)**| Merges values with the same key using a function. |
| **union(otherRDD)**  | Combines two RDDs into one. |
| **distinct()**       | Removes duplicate elements. |
| **sample(withReplacement, fraction, [seed])** | Returns a random sample of the RDD. |
| **join(otherRDD)**   | Joins two RDDs by their keys. |
| **cogroup(otherRDD)**| Groups data from two RDDs sharing the same key. |
| **cartesian(otherRDD)** | Returns the Cartesian product of two RDDs. |
| **pipe(command, [envVars])** | Transforms each RDD element using an external program. |
| **coalesce(numPartitions)** | Reduces the number of partitions in the RDD. |
| **repartition(numPartitions)** | Increases or decreases the number of partitions in the RDD. |
| **sortByKey([ascending])** | Sorts the RDD by key. |
| **subtract(otherRDD)** | Returns an RDD with elements from the first RDD that are not in the second RDD. |
| **intersection(otherRDD)** | Returns an RDD with elements common to both RDDs. |

## Actions

| Action                | Description |
|-----------------------|-------------|
| **collect()**         | Returns all elements of the dataset as an array to the driver program. |
| **count()**           | Returns the number of elements in the dataset. |
| **take(n)**           | Returns an array with the first n elements of the dataset. |
| **reduce(func)**      | Aggregates the elements of the dataset using a function. |
| **saveAsTextFile(path)** | Saves the dataset as a text file. |
| **saveAsSequenceFile(path)** | Saves the dataset as a Hadoop sequence file. |
| **saveAsObjectFile(path)** | Saves the dataset as a serialized Java object. |
| **countByKey()**      | Counts the number of elements for each key. |
| **foreach(func)**     | Applies a function to each element of the dataset. |
| **lookup(key)**       | Returns the list of values for a key in the dataset. |
| **first()**           | Returns the first element of the dataset. |
| **takeSample(withReplacement, num, [seed])** | Returns a fixed-size sample subset of the dataset. |
| **takeOrdered(n, [ordering])** | Returns the first n elements of the dataset, ordered by a specified comparator. |
| **top(n)**            | Returns the top n elements of the dataset. |
| **countByValue()**    | Returns a map of (value, count) pairs. |
| **saveAsHadoopFile(path, [keyClass], [valueClass], [outputFormatClass])** | Saves the dataset as a Hadoop file. |
| **saveAsNewAPIHadoopFile(path, [keyClass], [valueClass], [outputFormatClass])** | Saves the dataset as a Hadoop file using a new API. |
| **saveAsHadoopDataset(conf)** | Saves the dataset as a Hadoop dataset. |
| **saveAsNewAPIHadoopDataset(conf)** | Saves the dataset as a Hadoop dataset using a new API. |

## Programming

For the example, It counts each word appearing in a document.

The input file's content:

```text
people are not as beautiful as they look, as they walk or as they talk. 
they are only as beautiful  as they love, as they care as they share.
```

Save the above content as an **input.txt** file in home user directory.

Read file from given location:

```bash
scala> val inputfile = sc.textFile("input.txt")
inputfile: org.apache.spark.rdd.RDD[String] = input.txt MapPartitionsRDD[1] at textFile at <console>:23
```

Execute word count transformation:

```bash
scala> val counts = inputfile.flatMap(line => line.split(" ")).map(word => (word, 1)).reduceByKey(_+_);
counts: org.apache.spark.rdd.RDD[(String, Int)] = ShuffledRDD[4] at reduceByKey at <console>:23
```

Show the description about current RDD and its dependencies for debugging:

```bash
scala> counts.toDebugString
res1: String =
(2) ShuffledRDD[4] at reduceByKey at <console>:23 []
 +-(2) MapPartitionsRDD[3] at map at <console>:23 []
    |  MapPartitionsRDD[2] at flatMap at <console>:23 []
    |  input.txt MapPartitionsRDD[1] at textFile at <console>:23 []
    |  input.txt HadoopRDD[0] at textFile at <console>:23 []
```

Store the intermediate transformations in memory:

```bash
scala> counts.cache()
res3: counts.type = ShuffledRDD[4] at reduceByKey at <console>:23
```

Save the output in a output directory:

```bash
scala> counts.saveAsTextFile("output)
```

To interrupt the current Spark session, press the combination hot key: `Ctrl + C`.

Check output directory:

```bash
$ ~/output$ ls -1
part-00000
part-00001
_SUCCESS
```

See output from **Part-00000** and **Part-00001** files:

```bash
$ ~/output$ cat part-00000
(talk.,1)
(are,2)
(only,1)
(as,8)
(,1)
(they,7)
(love,,1)
$ ~/output$ cat part-00001
(not,1)
(people,1)
(share.,1)
(or,1)
(care,1)
(beautiful,2)
(walk,1)
(look,,1)
```

## UN Persist storage

If you want to see the Shark shell application UI, open the following URL: `http://localhost:4040/`.

If you want to UN-persist the storage space of particular RDD, then use the following command:

```bash
scala> counts.unpersist()
res1: counts.type = ShuffledRDD[4] at reduceByKey at <console>:23
```

## Summarization

- **Spark Core**: The foundation of the project, providing distributed task dispatching, scheduling, and basic I/O functionalities.
- **RDD (Resilient Distributed Datasets)**: A fundamental data structure in Spark, partitioned across machines, created from external storage or by applying transformations.
- **Interactive Shell**: Available in Scala or Python, allowing for interactive data analysis.
- **Transformations and Actions**: Transformations create new RDDs, while actions trigger execution and return values. Examples include `map`, `filter`, `reduceByKey`, and `saveAsTextFile`.
