## Steps: 

1. Create the final topic using **kafka-topics**. 
```
kafka-topics.sh --bootstrap-server localhost:9092 --create --replication-factor 1 --partitions 2 --topic wordcount-input
kafka-topics.sh --bootstrap-server localhost:9092 --create --replication-factor 1 --partitions 2 --topic wordcount-output
kesharir@Ritanshu:~$ kafka-topics.sh --bootstrap-server localhost:9092 --list
__consumer_offsets
streams-plaintext-input
streams-wordcount-KSTREAM-AGGREGATE-STATE-STORE-0000000003-changelog
streams-wordcount-KSTREAM-AGGREGATE-STATE-STORE-0000000003-repartition
streams-wordcount-output
wordcount-input
wordcount-output
```
2. Lets run a **kafka-console-consumer** to the final topic.
```
kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic word-count-output \
    --from-beginning --formatter kafka.tools.DefaultMessageFormatter \
    --property print.key=true \
    --property print.value=true \
    --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer \
    --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
```
3. Lets run our application from Intellij. 
4. And publish some more data to our input topic using **kafka-console-producer**. 
```
kesharir@Ritanshu:~$ kafka-console-producer.sh --bootstrap-server localhost:9092 --topic wordcount-input
>hello kafka streams
>kafka streams is working
>stephane is kafka level awesome
>hello
>hello
>hello
>hwwllo
>hello kafka kafka kafka
>kafka
>we can type any kafka sentence
>kafka kafka kafka kafka kafka
>debug kafka
```


**Output from kafka-console-consumer**

```
kesharir@Ritanshu:~$ kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic word-count-output --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property print.value=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
kafka   6
hwwllo  1
hello   5
kafka   7
can     1
kafka   8
sentence        1
we      1
type    1
any     1
kafka   13
debug   1
kafka   14
```