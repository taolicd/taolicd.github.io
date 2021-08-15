---
layout: post
title:  "Hadoop and Spark"
date:   2019-04-30
categories:  big data framework


---
When talking about big data frameworks, most likely people will bring up Apache Hadoop and Apache Spark. This post will explain what they are and their relationships.   

## Apache Hadoop

Apache Hadoop is an open source big data framework written in Java for distributed storage and distributed processing of big data. At the core of the Hadoop system are two important parts:

 * HDFS (Hadoop Distributed File System), which is the storage unit of the system. Each HDFS has one single namenode and a bunch of datanodes. The namenode stores the metadata of the system including the name and addresses of the datanodes. The datanodes are where the actual data is stored. 
 * MapReduce, which is the processing unit of the system. MapReduce is a programming model for distributed parallel processing of data. 

Hadoop has been around since 2010 and it has become the cornerstone in the big data arena. A slew of supporting tools have emerged to form the Hadoop ecosystem:

 * Pig Latin, the scripting language used on Hadoop
 * Hive, SQL query on Hadoop
 * YARN, also called MapReduce 2.0, it is the cluster resource management and job scheduling tool 
 * Mahout, machine learning and data mining tool on Hadoop
 * Oozie, workflow management tool
 * Flume, log collector
 * Zookeeper, coordination tool
 * Ambari, provisioning, managing and monitoring tool
 * Sqoop, data exchange tool

The major disadvantage with Hadoop is it is batch-driven and therefore not for real-time data processing. 

## Apache Spark

Apache Spark is an open source big data framework released in 2014 mainly to tackle the performance issue with big data computation. Spark has become more and more popular among data scientists who want to get an answer quickly rather than waiting for the batch processing result the next day. 

Spark reads data from other sources and stores it in resilient distributed dataset (RDD), a read-only multiset of data items distributed over a cluster of machines. This mechanism greatly improves Spark's speed when doing data processing. Spark is claimed to be up to 100 times faster than Hadoop MapReduce although some people are skeptical about this claim. 

Spark is written in Scala and it supports programs written in Scala, Python, Java and R. Spark's ecosystem contains the following:

 * Spark Shark, SQL on Spark
 * Spark Streaming, for real-time data streaming
 * Spark MLLib, machine learning library on Spark
 * GraphX, graph computation on Spark
 * SparkR, R on Spark

Apache Spark does not have its own dedicated distributed storage solution.

## Summary

Hadoop and Spark are not mutually exclusive. You can configure them to work together to take advantage of Hadoop's HDFS for storage and Spark for computation. 
