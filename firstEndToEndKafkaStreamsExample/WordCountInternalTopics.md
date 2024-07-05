- Running a Kafka Streams may eventually create internal intermediary topics. 
- Two Types: 
  - Repartitioning topics: In case you start trasforming the key of your stream, a repartitioning
    will happen at some processor. 
  - Changelog topics: In case you perform aggregations, Kafka Streams will save compacted data in 
    these topics. 
- Internal Topics: 
  - Are managed by Kafka Streams.
  - Are used by Kafka Streams to save/restore state and re-partition data
  - Are prefixed by application.id parameter.
  - Should never be deleted, altered or published to. They are internal.
    ```
    kesharir@Ritanshu:~$ kafka-topics.sh --bootstrap-server localhost:9092 --list
    __consumer_offsets
    demo_java
    streams-plaintext-input
    streams-starter-app-KSTREAM-AGGREGATE-STATE-STORE-0000000004-changelog
    streams-starter-app-KSTREAM-AGGREGATE-STATE-STORE-0000000004-repartition
    streams-wordcount-KSTREAM-AGGREGATE-STATE-STORE-0000000003-changelog
    streams-wordcount-KSTREAM-AGGREGATE-STATE-STORE-0000000003-repartition
    streams-wordcount-output
    word-count-output
    word_count-output
    wordcount-input
    wordcount-output
    ```
    