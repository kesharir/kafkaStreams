## How to do exactly once in kafka streams ? 

- One additional line of code, the rest is same.

```java
import java.util.Properties;

Properties props = new Properties();
//...
props.put(StreamsConfig.PROCESSING_GUARANTEE_CONFIG, StreamsConfig.EXACTLY_ONCE);
//...
KafkaStreams streams = new KafkaStreams(builder, props);
```

- Currently, Kafka Streams is the only library that has implemented this feature, but its possible
    that Spark, Flink and other frameworks implement it in the future too. 

- What's the trade-off?
  - Results are published in transactions, which might incur a small latency.
  - You can fine tune this setting using ***commit.interval.ms***