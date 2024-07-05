## Stream as Table: 

A Stream can be considered a changelog of a table, where each data record in the stream captures a state change of the table.

## Table As Stream: 

A table can be connsidered a snapshot at a point in time of the latest value for each key in a stream (a stream's data records are key-value pairs).

## Transforming a KTable to a KStream: 

- It is sometimes helpful to trasform a KTable to a Kstream in order to keep a changelog of all the changes to the KTable.
- This can be easily achieved in one line of code. 

```java
KTable<byte[], String> table = ...;
KStream<byte[], String> stream = table.toStream();
```

## Transforming a KStream to a KTable: 

- Two Ways: 
  - Chain a groupByKey() and an aggregation step (count, aggregate, reduce)
    ```java
        KTable<String, Long> table = usersAndColours,groupByKey().count();
    ```
  - Write back to Kafka and read as KTable.   
    ```java
    // write to kafka
    stream.to("intermediary-topic");
    // read from Kafka as a table
    KTable<String, String> table = builder.table("intermediary-topic");
    ```
