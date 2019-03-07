---
tip: 24
title: TRC-24 Implement DB storage with RocksDB
author: shydesky<shydesky@gmail.com>
type: Standards Track
category: TRC
discussion-to: https://github.com/tronprotocol/TIPs/issues/24
status: in process
created: 2019-03-04
---

## Simple Summary
Implement the database storage layer with RocksDB.  
## Abstract
Currently, java-tron project uses LevelDB as the only implement of the database storage layer.This Tip is created for the purpose of adding a new implement of the database storage layer.
## Motivation
RocksDB is a good storage engine built on earlier work on LevelDB and it is widely used in production environments.It has higher performance when storing key-value data benefiting from exploiting many cpu cores than LevelDB.RocksDB provides all of the features of LevelDB and some useful functions like backups and snapshots.It is very friendly to the developers to find the bottleneck of the system and contains many parameters used to tune RocksDB for your workload and your system configuration.
So, it is wisely add the implement of the database storage layer with RocksDB to make our java-tron more effective and robust.

## Implement
Database storage layor with RocksDB is implemented easily because of interfaces' good designing in java-tron project.It is just the bottom storage engine we use the RocksDB as. It is transparent completely to the network module. 

### Overview
First and the most important,the RocksDB implement and the LEVELDB are in the same level of the java-tron.
The storage engine choosen by the project depends on the parameter (`db.engine`) in the `config.conf` file. The valid value is one of "LEVELDB" and "ROCKSDB".

And then, you can do some code review at `RocksDbDataSourceImpl` class, it is the most important class in our implement.

####  Compatible with LevelDB
It is important to distinguish which engine is used by java-tron project if we do not delete the whole database. That means we can just use one type of engine (rocksdb or leveldb) because the data structure in this two engine is not compatible, so we add a properties.prop file used to indicate which engine is choosen before in every database's directory.
There are 20+ databases in our java-tron project and it is requested using one type of engine continuously in one databases. 
we provide a convert tool to convert the LevelDB database to the RocksDB database.It can be used by run `java -jar DBConvert.jar`.

#### Support tuning with RocksDB engine
We expose some parameters to supprot tuning the database based on RocksDB engine.These are listed as follows:
```levelNumber
compactThreads
blocksize
maxBytesForLevelBase
level0FileNumCompactionTrigger
compressionTypeListStr
targetFileSizeBase
targetFileSizeMultiplier
```
you can check the [RocksDB Tuning Guide](https://github.com/facebook/rocksdb/wiki/RocksDB-Tuning-Guide) for more details and try it by modifing the parameters defined in the `config.conf`. 

#### Support Backup with RocksDB engine
This function is a very cool and you can use it by modifing the parameter `backup` in the `config.conf`.The detail of usage is shown in the `config.conf`.We strongly recommend you must check whether it has enough hard disk space to enable the backup the database. 
