## Reading from Kafka: 

- You can read a topic as a KStream, a KTable or a GlobalKTable: 

***KStream***
```java
KStream<String, Long> wordCounts = builder.stream(
    Serdes.String(), /* key serde */
    Serdes.Long(), /* value serde */
    "word-counts-input-topic" /* input topic */    
);
```

***KTable***
```java
KTable<String, Long> wordCounts = builder.table(
        Serdes.String(), /* key serde */
        Serdes.Long(), /* value serde */
        "word-counts-input-topic" /* input topic */
);
```

***GlobalKTable***
```java
GlobalKTable<String, Long> wordCounts = builder.globalTable(
    Serdes.String(), /* key serde */
    Serdes.Long(), /* value serde */
    "word-counts-input-topic" /* input topic */
);
```