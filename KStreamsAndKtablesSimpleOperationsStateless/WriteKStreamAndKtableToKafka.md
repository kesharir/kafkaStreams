## Write KStream And KTable to Kafka: 

- You can write any KStream or KTable back to Kafka. 
- If you write a KTable back to Kafka, think about creating a log compacted topic!
- ***To***:Terminal operation - write the records to a topic: 

    ```java
        stream.to("my-stream-output-topic");  
        table.to("my-table-output-topic");
    ```
- ***Through***: Write to a topic and get a stream/table from the topic:

    ```java
        KStream<String, Long> newStream = stream.through("user-clicks-topic");
        KTable<String, Long> newTable = table.through("my-table-output-topic");
    ```