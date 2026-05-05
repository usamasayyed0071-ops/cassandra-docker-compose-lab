# Cassandra Docker Compose Project

##  Overview

This project demonstrates how to deploy Apache Cassandra using Docker
Compose with environment variables and understand its storage engine
internals including Commit Log, MemTables, and SSTables.


##  Setup

### 1. Create Project Directory

``` bash
mkdir cassandra-docker
cd cassandra-docker
```

### 2. Create .env File

``` env
CASSANDRA_CLUSTER_NAME=MyCluster
CASSANDRA_DC=DC1
CASSANDRA_RACK=RACK1
```

### 3. Create docker-compose.yml

##  Run Cassandra

``` bash
docker compose up -d
```

##  Connect to Cassandra

``` bash
docker exec -it cassandra1 cqlsh
```

##  Database Operations

##  Storage Engine Internals

### Commit Log

``` bash
cd /var/lib/cassandra/commitlog
ls
```

### SSTables

``` bash
cd /var/lib/cassandra/data/testdb
ls
cd users*
ls
```

### Flush MemTable

``` bash
nodetool flush
```

### Compaction

``` bash
nodetool compact
```

##  Data Flow

Write → Commit Log → MemTable → SSTable → Compaction

## Purpose

-   High availability
-   Fault tolerance
-   Scalable storage
-   Fast writes





This project demonstrates Cassandra deployment and internal working
practically using Docker Compose.
