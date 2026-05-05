# 🚀 Cassandra Docker Compose Project

## 📌 Overview

This project demonstrates how to deploy Apache Cassandra using Docker
Compose with environment variables and understand its storage engine
internals including Commit Log, MemTables, and SSTables.

------------------------------------------------------------------------

## ⚙️ Setup

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

``` yaml
version: '3.8'

services:
  cassandra1:
    image: cassandra:4.1
    container_name: cassandra1
    env_file:
      - .env
    environment:
      - MAX_HEAP_SIZE=256M
      - HEAP_NEWSIZE=50M
      - CASSANDRA_CLUSTER_NAME=${CASSANDRA_CLUSTER_NAME}
      - CASSANDRA_DC=${CASSANDRA_DC}
      - CASSANDRA_RACK=${CASSANDRA_RACK}
    ports:
      - "9042:9042"
    volumes:
      - cassandra_data:/var/lib/cassandra

volumes:
  cassandra_data:
```

------------------------------------------------------------------------

## ▶️ Run Cassandra

``` bash
docker compose up -d
```

------------------------------------------------------------------------

## 🔌 Connect to Cassandra

``` bash
docker exec -it cassandra1 cqlsh
```

------------------------------------------------------------------------

## 🧪 Database Operations

``` sql
CREATE KEYSPACE testdb WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 1};
USE testdb;

CREATE TABLE users (
  id UUID PRIMARY KEY,
  name TEXT,
  age INT
);

INSERT INTO users (id, name, age) VALUES (uuid(), 'Usama', 25);
INSERT INTO users (id, name, age) VALUES (uuid(), 'Ali', 30);

SELECT * FROM users;
```

------------------------------------------------------------------------

## 🔍 Storage Engine Internals

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

------------------------------------------------------------------------

## 🔄 Data Flow

Write → Commit Log → MemTable → SSTable → Compaction

------------------------------------------------------------------------

## 🎯 Purpose

-   High availability
-   Fault tolerance
-   Scalable storage
-   Fast writes

------------------------------------------------------------------------

## 🏁 Conclusion

This project demonstrates Cassandra deployment and internal working
practically using Docker Compose.
