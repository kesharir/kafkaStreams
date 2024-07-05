## Filter And FilterNot: 

- Takes one record and produces zero or one record. 
- Filter:
  - does not change keys/values
  - == does not trigger a repartition
  - For KStreams or Ktables
- FilterNot:
  - Inverse of Filter

```java
// A filter that selects only positive numbers:
KStream<String, Long> onlyPositive = stream.filter((key, value) -> value > 0);
// (alice, 5) --> (alice, 5)
// (alice, -2) --> Record deleted 
```