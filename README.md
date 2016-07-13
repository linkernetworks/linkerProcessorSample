# linkerProcessorSample Intro
[![Build Status](https://travis-ci.org/adolphlwq/linkerProcessorSample.svg?branch=master)](https://travis-ci.org/adolphlwq/linkerProcessorSample)

A sample code for processing infomation from Kafka and store to Cassandra using Apache Spark

## Usage
### Prerequisite
First, you should set up zookeeper, cassandra and kafka broker. Then create kafka topic and cassandra keyspace

Second:

1. download [Apache Spark](spark.apache.org)
2. run [linkerConnector](https://github.com/LinkerNetworks/linkerConnector)
    - git clone https://github.com/LinkerNetworks/linkerConnector.git
    - install [Golang](https://golang.org/)
    - cd path/to/linkerConnector
    - `go build` and `go install`
3. git clone linkerProcessSample(https://github.com/adolphlwq/linkerProcessorSample.git)
3. submit python code to spark(**local mode**):
```
path/to/spark/bin/spark-submit \
    --packages org.apache.spark:spark-streaming-kafka_2.10:1.6.1  \
    path/to/linkerProcessorSample/spark2cassandra.py kafka_broker_servers kafka_topic
```

## Note:
1. interval of spark streaming **>** interval of linkerConnector

## Reference
- [calculate cpu usage in Golang](https://sourcegraph.com/github.com/statsd/system/-/def/GoPackage/github.com/statsd/system/pkg/cpu/-/totals)
- [Linux Kernel about proc](http://www.mjmwired.net/kernel/Documentation/filesystems/proc.txt#1271)
- [Cassandra tutorial](http://www.tutorialspoint.com/cassandra/cassandra_alter_table.htm)
- [Cassandra data types](https://docs.datastax.com/en/cql/3.0/cql/cql_reference/cql_data_types_c.html)
- [Cassandra user user-defined-type](https://docs.datastax.com/en/cql/3.1/cql/cql_using/cqlUseUDT.html)

## Docker image
This image is for Spark exector on Mesos

## TODOs
- [X] collect info from kafka
- [X] save processes info to cassandra
- [X] save machine info to cassandra
- [X] save kafka message to cassandra directly
- [X] overall cpu usage from linkerConnector (via Kafka)
    - [X] calculate cpu usage and save to cassandra
- [ ] research spark streaming's "window" and improve code
- [ ] mesos agent usage from linkerConnector (via Kafka)
- [ ] build spark docker image for testing code on [Spark on Mesos mode](http://spark.apache.org/docs/latest/running-on-mesos.html) using [linkerDCOS](http://linkernetworks.com/) or [DC/OS](https://dcos.io/)