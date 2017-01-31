# Minerva Zookeeper

  - Zookeeper

##### Prerequisites

* Docker Engine https://docs.docker.com/engine/installation/
* Docker Compose https://docs.docker.com/compose/install/

##### Reference

* Debezium Zookeeper https://hub.docker.com/r/debezium/zookeeper/

##### Commands

Download:
```
$ docker pull jmilagrosoc4w/minerva.zookeeper
```

Start Zookeeper:
```
$ docker run -it --name zookeeper -p 2181:2181 -p 2888:2888 -p 3888:3888 jmilagrosoc4w/minerva.zookeeper
```

Start Zookeeper (Detached Mode):
```
$ docker run -d --name zookeeper -p 2181:2181 -p 2888:2888 -p 3888:3888 jmilagrosoc4w/minerva.zookeeper
```

Display Logs:
```
$ docker logs --follow --name zookeeper
```

Display Zookeeper status:
```
$ docker run -it --rm jmilagrosoc4w/minerva.zookeeper status
```

Use the Zookeeper CLI
```
$ docker run -it --rm jmilagrosoc4w/mineva.zookeeper cli
```

Environment variables
The Debezium Zookeeper image uses several environment variables.

SERVER_ID
This environment variable defines the numeric identifier for this Zookeeper server. The default is '1' and is only applicable for a single standalone Zookeeper server that is not replicated or fault tolerant. In all other cases, you should set the server number to a unique value within your Zookeeper cluster.

SERVER_COUNT
This environment variable defines the total number of Zookeeper servers in the cluster. The default is '1' and is only applicable for a single standalone Zookeeper server. In all other cases, you must use this variable to set the total number of servers in the cluster.

LOG_LEVEL
This environment variable is optional. Use this to set the level of detail for Zookeeper's application log written to STDOUT and STDERR. Valid values are INFO (default), WARN, ERROR, DEBUG, or TRACE."

Ports
Containers created using this image will expose ports 2181, 2888, and 3888. These are the standard ports used by Zookeeper. You can use standard Docker options to map these to different ports on the host that runs the container.

Storing data
The Kafka broker run by this image writes data to the local file system, and the only way to keep this data is to volumes that map specific directories inside the container to the local file system (or to OpenShift persistent volumes).

Zookeeper data
This image defines a data volume at /zookeeper/data, and it is in this directory that the Zookeeper server will persist all of its data. You must mount it appropriately when running your container to persist the data after the container is stopped; failing to do so will result in all data being lost when the container is stopped.

Log files
Although this image will send Zookeeper's log output to standard output so it is visible as Docker logs, this image also configures Zookeeper to write out more detailed lots to a data volume at /zookeeper/logs. You must mount it appropriately when running your container to persist the logs after the container is stopped; failing to do so will result in all logs being lost when the container is stopped.

Configuration
This image defines a data volume at /zookeeper/conf where the Zookeeper server's configuration files are stored. Note that these configuration files are always modified based upon the environment variables and linked containers. The best use of this data volume is to be able to see the configuration files used by Zookeper, although with some care it is possible to supply custom configuration files that will be adapted and used upon container startup.
