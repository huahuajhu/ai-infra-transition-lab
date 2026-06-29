# Week 1 Day 3 Checkpoint

## Status

Completed first-pass MapReduce concept map, AI training data pipeline sketch, and checkpoint answers.

## Sources

- MIT 6.5840 schedule: https://pdos.csail.mit.edu/6.824/schedule.html
- MIT 6.5840 Lab 1: MapReduce: https://pdos.csail.mit.edu/6.824/labs/lab-mr.html
- MapReduce paper: https://pdos.csail.mit.edu/6.824/papers/mapreduce.pdf

## Type

Source-grounded + artifact-grounded

## A. Source-Grounded Questions From The MapReduce Paper

### 1. What do the `map` and `reduce` functions do?

My answer:

The `map` function processes input key/value pairs and emits intermediate key/value pairs. The `reduce` function receives an intermediate key plus all values for that key and merges those values into output values.

Confidence: High

### 2. What does the master/coordinator track?

My answer:

The master tracks every map and reduce task state: idle, in-progress, or completed. It also tracks which worker owns non-idle tasks and records the locations and sizes of intermediate map outputs so reduce workers know where to fetch data.

Confidence: High

### 3. How does MapReduce handle worker failure?

My answer:

The master periodically pings workers. If a worker stops responding, the master marks it failed, resets in-progress tasks to idle, and reschedules them. Completed map tasks from that worker are also rerun because their intermediate output lived on the failed worker's local disk, while completed reduce outputs do not need rerun if they were written to the global file system.

Confidence: High

### 4. Why is a straggler different from a failed task?

My answer:

A failed task is on a worker that has crashed, stopped responding, or been marked failed, so the system reschedules the work. A straggler is still running, but it is unusually slow and can delay the whole job near the end.

Confidence: High

### 5. Why does data locality matter?

My answer:

Data locality matters because network bandwidth is scarce compared with reading data locally. The MapReduce master tries to schedule map tasks on, or near, machines that already store the input split so large jobs do not waste network bandwidth moving input data around the cluster.

Confidence: High

### 6. Why can backup tasks reduce job completion time?

My answer:

Backup tasks reduce job completion time by launching duplicate executions of remaining slow in-progress tasks near the end of the job. The task is considered complete when either the original or backup execution finishes, so one slow worker does not hold the entire job hostage.

Confidence: High

### 7. What tradeoff exists in choosing the number of map and reduce tasks?

My answer:

More tasks improve load balancing and make recovery faster because work can be spread across many workers. But too many tasks increase coordinator overhead: the master must make more scheduling decisions and store more task/partition metadata.

Confidence: High

## B. Artifact-Grounded Questions From The Pipeline Sketch

### 8. In your AI training data pipeline sketch, what is the map stage?

My answer:

The map stage is `parse/filter/tokenize`. Each worker reads a raw input split, parses records, cleans text, filters bad or low-quality examples, tokenizes usable text, and emits intermediate records such as document IDs, token counts, language/domain signals, content hashes, or target shard IDs.

Confidence: High

### 9. In your AI training data pipeline sketch, what is the reduce stage?

My answer:

The reduce stage is `aggregate/dedupe/shard`. It groups intermediate records by key or target shard, aggregates quality statistics, removes duplicates by hash or document ID, writes final training shard contents, and produces metadata needed by the output manifest.

Confidence: High

### 10. Which stage is most likely to become a bottleneck, and what metric would you watch first?

My answer:

The most likely bottleneck is the shuffle/partition plus reduce boundary, because large tokenized records or skewed keys can create heavy network transfer and uneven reduce partitions. I would watch shuffle bytes and the slowest partition duration first, then compare them with map tokens/sec and reduce spill/sort time.

Confidence: Medium

## Follow-Up

- Revisit this after Week 4 distributed training and Week 10 capacity planning.
