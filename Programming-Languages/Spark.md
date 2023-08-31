# Spark

### Basic Knowledge

- Spark is a fast and general engine for large-scale data processing. It provides in-memory cluster computing capabilities.
- The core abstraction Spark uses is the resilient distributed dataset (RDD) - an immutable distributed collection of objects spread across a cluster.
- Spark utilizes a cluster manager like YARN, Mesos, or its standalone mode to allocate resources across applications. It isn't tied to Hadoop's MapReduce.
- Spark SQL allows querying data via SQL and the DataFrame API. Spark integrates with Hive metastores for schema management and querying.
- Compared to Hadoop, Spark provides faster iterative computation through in-memory caching. It is less suitable for purely file-based batch processing.
- For machine learning, Spark MLlib provides distributed implementations of algorithms like classification, clustering, regression.
- Spark Streaming lets you ingest and process live streams of data using mini-batching and stateful operations like windowing.
- Structured Streaming is a high-level streaming API built on DataFrames/Datasets for building continuously executing queries on static or streaming data.

### Problems

- A few ways to determine the total number of stages in a Spark job:

  1. Spark UI 

  The Spark UI web interface shows all the stages for a given job. You can navigate to the Jobs tab, click on your job, and view the list of stages under the Stage tab. This will show the total count of stages.

  2. Spark History Server

  Similar to the Spark UI, the History Server web UI lists all jobs and their associated stages. You can inspect past jobs and see the total stage count.

  3. Stage ID 

  As your job runs, each stage prints a stage ID like "Stage 5". The stage count continuously increments as more stages start. So the last stage ID gives you the total.

  4. In code

  You can add a `df.explain()` in your code after an action like `show()`. This will print the physical plan with all stages listed. Count the distinct stages to get the total. 

  5. Programmatically

  Call `sparkContext.statusTracker.getStageInfos()` and check the size of the returned list of StageInfo objects.

  So in summary, looking at the stage IDs as they print, using the Spark UI/History, or programmatically checking stage infos are some ways to get the total stage count for a Spark job. Let me know if you have any other questions!