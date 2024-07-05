# kafkaStreams

## About Instructor: 

- This course is by Stephane Marek ( CLOUD & DATA Instructor )
- LinkedIn : IN/STEPHANEMAAREK
- Instagram : STEPHANEMAAREK


## Starting Kafka from WSL Commands: 


```shell
sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1
sudo sysctl -w net.ipv6.conf.default.disable_ipv6=1
zookeeper-server-start.sh ~/kafka_2.13-3.0.0/config/zookeeper.properties
kafka-server-start.sh ~/kafka_2.13-3.0.0/config/server.properties
```