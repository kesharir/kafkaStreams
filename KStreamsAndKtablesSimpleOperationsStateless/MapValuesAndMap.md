## MapValues & Map: 

- Takes one record and produces one record. 
- MapValues : 
  - is only affecting values
  - == does not change keys
  - == does not trigger a repartition
  - For KStreams and KTable
- Map :
  - Affects both keys and values
  - Triggers a repartitions
  - for Kstreams only 

- MapValues Example:
```java
// KStream<byte[], String>
uppercased = stream.mapValues(value -> value.toUpperCase());
// (alice, cow) --> (alice, COW)
```
