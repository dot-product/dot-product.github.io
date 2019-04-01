---
layout : default
title : SPARK
permalink: /spark
---


### Terminology

   - Spark Driver Program

   - Spark Context

   - Spark Executors

   - Spark DAG

   - Stages

   - Tasks

   - RDD( Resillient Distributed Data stores)


### Heap of executor

   - heap = some lefover + safe

   - safe = spark.storage.safetyFraction * heap

   - Shuffle = 20% of safe (or) spark.shuffle.memoryFraction * safe

   - Storage = 60% of safe (or) spark.storage.memoryFraction * safe

   - Unroll = 20% of storage (or) spark.storage.unrollFraction


