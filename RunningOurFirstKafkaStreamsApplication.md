## Steps: 

1. Download Kafka binaries
2. Start ZooKeeper and Kafka
   ```
   zookeeper-server-start.sh ~/kafka_2.13-3.0.0/config/zookeeper.properties 
   kafka-server-start.sh ~/kafka_2.13-3.0.0/config/server.properties
   ```
3. Create input and output topics using `kafka-topics`
   ```
    kafka-topics.sh --bootstrap-server localhost:9092 --create --replication-factor 1 --partitions 1 --topic streams-plaintext-input
    kafka-topics.sh --bootstrap-server localhost:9092 --create --replication-factor 1 --partitions 1 --topic streams-wordcount-output
    kesharir@Ritanshu: kafka-topics.sh --bootstrap-server localhost:9092 --list
    streams-plaintext-input
    streams-wordcount-output 
   ```

4. Publish data to the input topic.
   ``` 
   kafka-console-producer.sh --bootstrap-server localhost:9092 --topic streams-plaintext-input
   >kafka streams udemy
   >kafka data processing
   >kafka streams course
   ```
   
    ```
    kesharir@Ritanshu:~$ kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic streams-plaintext-input --from-beginning
    kafka streams udemy
    kafka data processing
    kafka streams course
    ^CProcessed a total of 3 messages
    ```

5. Run the WordCount example.
   ```
   kafka-run-class.sh org.apache.kafka.streams.examples.wordcount.WordCountDemo
   ``` 
   
6. Stream the output topic using `kafka-console-consumer`. 

    ```
    kesharir@Ritanshu:~$ kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic streams-wordcount-output \
    > --from-beginning \
    > --formatter kafka.tools.DefaultMessageFormatter \
    > --property print.key=true \
    > --property print.value=true \
    > --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer \
    > --property value.deserializer=org.apache.common.serialization.LongDeserializer
    ```
   
    **Console Output**

    ```
   kafka   1
   streams 1
   udemy   1
   kafka   2
   data    1
   processing      1
   kafka   3
   streams 2
   course  1
    ```
   

**Note: Kafka Additional Topics created**

```
kesharir@Ritanshu:~$ kafka-topics.sh --bootstrap-server localhost:9092 --list
__consumer_offsets
streams-plaintext-input
streams-wordcount-KSTREAM-AGGREGATE-STATE-STORE-0000000003-changelog
streams-wordcount-KSTREAM-AGGREGATE-STATE-STORE-0000000003-repartition
streams-wordcount-output
```


