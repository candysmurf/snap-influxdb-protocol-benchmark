# snap-influxdb-protocol-benchmark

This repository demostrates how to collect statistics of InfluxDB writes via UDP and HTTP which includes CPU usage reduction, write speed improvements, and comparison of data size reduction.
Prerequisite is having Docker and docker-compose installed.

## Exam CPU Usage
The example simulates 30 concurrent random number generators. They are continuously writing data into InfluxDB in 10 milisecond intervals.

Starting HTTP and UDP InfluxDB writes
```
$ docker-compose -f snap-influx-random-http.yml up -d
$ docker-compose -f snap-influx-random-udp.yml up -d
```

Observing Container process CPU usage
```
$ docker stats
```
Command `docker stats` shows the stream statistics of container CPU, memory, IO usage, etc.


## Exam Write Speed and Metric Size
The example collects InfluxDB write the number of metric data points in terms of using single value vs. field set via UDP and HTTP protocols.

Starting PSUTIL InfluxDB writes
```
$ docker-compose -f snap-influx-psutil-http.yml up -d
$ docker-compose -f snap-influx-psutil-udp.yml up -d
```

Dashboard is availabe at: http://[DOCKER-HOST]:8083.

Stopping and Removing Containers
```
$ docker-compose -f snap-influx-random-http.yml down
$ docker-compose -f snap-influx-random-udp.yml down
$ docker-compose -f snap-influx-psutil-http.yml down
$ docker-compose -f snap-influx-psutil-udp.yml down
```
