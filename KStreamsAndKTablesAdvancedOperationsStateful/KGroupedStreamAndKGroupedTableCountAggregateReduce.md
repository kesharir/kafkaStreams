## KGroupedStream And KGroupedTable Count: 

- As a reminder, KGroupedStream are obtained after a `groupBy/groupByKey()` call on a KStream. 
- `Count` counts the number of record by grouped key.
- If used on KGroupedStream:
  - Null keys or values are ignored
- If used on KGroupedTable: 
  - Null keys are ignored
  - Null values are treated as "delete"

## KGroupedStream And KGroupedTable Aggregate: 

***KGroupedStream Aggregate:***
- You need an initializer (of any type), an adder, a Serde and a State Store name 
    (name of you aggregation).
- Example: Count total string length by key

```java
// Aggregating a KGroupedStream (note how the value type changes from String to Long)
KTable<byte[], Long> aggregatedStream = groupedStream.aggregate(
        () -> 0l, /* initializer */
        (aggKey, newValue, aggValue) -> aggValue + newValue.length(), /* adder */
        Serdes.Long(), /* serde for aggregate value */
        "aggregated-stream-store" /* state store name */
);
```

***KGroupedTable Aggregate:***

- You need an initializer (of any type),an adder, a substractor, a Serde and a State Store name
  (name of your aggregation).
- Example: Count total string length by key

```java
// Aggregating a KGroupedTable: 
KTable<byte[], Long> aggregatedStream = groupedTable.aggregate(
        () -> 0L,
        (aggKey, newValue, aggValue) -> aggValue + newValue.length(), /* adder */
        (aggKey, oldValue, aggValue) -> aggValue - oldValue.length(), /* subtractor */
        Serdes.Long(), /* serde for aggregate value */
        "aggregated-table-store" /* state store name */
);
```

## KGroupedStream And KGroupedTable Reduce: 

- Similar to ***Aggregate***, but the restlt type has to be the same as an input: 
- (Int, Int) => Int 
- (String,String) => String (example concat(a,b))

```java
// Reducing a KGroupedStream: 
KTable<String, Long> aggregatedStream = groupedStream.reduce(
        (aggValue, newValue) -> aggValue + newValue, /* adder */
        "reduced-stream-store" /* state store name */
);

// Reducing a KGroupedTable: 
KTable<String, Long> aggregatedTable = groupedTable.reduce(
        (aggValue, newValue) -> aggValue + newValue, /* adder */
        (aggValue, oldValue) -> aggValue - oldValue, /* subtractor */
        "reduced-table-store" /*state store name*/
);
```