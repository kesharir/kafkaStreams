## Refresher On Log Compaction: 

- Log compaction can be a huge improvement in performance when dealing with KTables because eventually records get discarded. 
- This means less reads to get to the final state (less time to recover).
- Log Compaction has to be enabled by you on the topics that get created (source or sink topics).

Watch This Later : https://marcelclasses.udemy.com/course/kafka-streams/learn/lecture/7636558#overview

### Resumed: 

- Suppose order of writes to topics is : 
  - Segment 0
    - Key=123 {"John":"80000"}
    - Key=456 {"Mark":"90000"}
    - Key=789 {"Lisa":"95000"}
  - Segment 1
    - Key=789 {"Lisa":"110000"}
    - Key=123 {"John":"100000"}

- After Compaction: 
  - Segment 0
    - Key=456 {"Mark":"90000"}
  - Segment 1
      - Key=789 {"Lisa":"110000"}
      - Key=123 {"John":"100000"}

### Log Compaction Gurantees: 

-  Any consumer that is reading from the head of a log will still see all the messages sent to the topic.
- Ordering of messages is kept, log compaction only removes some messages, but does not re-order them
- The offset of a message is immutable (it never changes). Offsets are just skipped if a message is missing.
- Deleted records can still be seen by consumers for a period of delete.retention.ms (default is 24 hours). 


### Log Compaction Myth Busting: 

- It doesn't prevent you from pushing duplicte data to Kafka.
  - De-duplication is done after a segment is committed
  - Your consumers will still read from head as soon as the data arrives.
- It doesn't prevent you from reading duplicate data from Kafka.
- Log Compaction can fail from time to time.
  - It is an optimization and the compaction thread might crash.
  - Make sure you assign enough memory to it and that it gets triggered. 

#### Producer Topic:
```shell
 kafka-topics.sh --bootstrap-server localhost:9092 \
    --create --replication-factor 1 \
    --partitions 1 \
    --topic employee-salary-compact \
    --config cleanup.policy=compact \
    --config min.cleanable.dirty.ratio=0.005 \
    --config segment.ms=10000
```

```
Created topic employee-salary-compact.
```

#### Consuming :

```shell
kafka-console-consumer.sh --bootstrap-server localhost:9092 \
  --topic employee-salary-compact \
  --from-beginning \
  --property print.key=true \
  --property key.separator=,
```

#### Producing to topic: 

```shell
kafka-console-producer.sh --bootstrap-server localhost:9092 \
  --topic  employee-salary-compact \
  --property parse.key=true \
  --property key.separator=,
```


```shell
>123,{"John":"80000"}
>456,{"Mark":"90000"}
>789,{"Lisa":"95000"}
>777,{"Stephane":"123"}
>789,{"Lisa":"1000000"}
>456,{"Mark":"2000000"}
>999,{"Philip":"123456"}
```

#### Consumer Output: 

```shell
123,{"John":"80000"}
777,{"Stephane":"123"}
789,{"Lisa":"1000000"}
456,{"Mark":"2000000"}
999,{"Philip":"123456"}
```