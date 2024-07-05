## FlatMapValues And FlatMap: 

- Takes one record and produces zero, one or more record. 
- FlatMapValues: 
  - does not change keys
  - == does not trigger a repartition
  - for KStreams only
- FlatMap: 
  - Change the Keys
  - == triggers a repartition
  - for KStreams only. 

```java
// Split a sentence into words 
words = sentences.flatMapValues(value -> Arrays.asList(value.split("\\s+")));
// (alice, alice is nice)
// -> (alice,alice)
// -> (alice,is)
// -> (alice,nice)
```

