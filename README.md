# snap-influxdb-protocol-statistics

This repository demostrates how to collect statistics of InfluxDB writes via UDP and HTTP which includes CPU usage reduction, write speed improvements, and comparison of data size reduction.
Prerequisite is having Docker and docker-compose installed.

## Exam CPU Usage
The example simulates 30 concurrent random number generators. They are continuously writing data into InfluxDB in 10 milisecond intervals.
Please try one at the time on the same machine as examples share the same application ports although they're in different containers.  

Starting InfluxDB writes
```
$ docker-compose -f snap-influx-random-http.yml up -d

OR  

$ docker-compose -f snap-influx-random-udp.yml up -d
```

Observing Container process CPU usage
```
$ docker stats
```
Command `docker stats` shows the stream statistics of container CPU, memory, IO usage, etc.

Stopping and Removing InfluxDB writes 
```
$ docker-compose -f snap-influx-random-http.yml down

OR

$ docker-compose -f snap-influx-random-udp.yml down
```


## Exam Write Speed and Metric Size
The example collects the number of metric data points in terms of using single value vs. field set via UDP and HTTP protocols.

Starting PSUTIL InfluxDB writes
```
$ docker-compose -f snap-influx-psutil-http.yml up -d

OR

$ docker-compose -f snap-influx-psutil-udp.yml up -d
```

Dashboard is availabe at: http://[DOCKER-HOST]:8083. Selecting `snap_http` or `snap_udp` database, you can query statistics:
```
  select * from psutil limit 10
```

Stopping and Removing PSUTIL InfluxDB HTTP writes
```
$ docker-compose -f snap-influx-psutil-http.yml down

OR

$ docker-compose -f snap-influx-psutil-udp.yml down
```

