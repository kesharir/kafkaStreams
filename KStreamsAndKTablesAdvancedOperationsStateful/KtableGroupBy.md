## KTable GroupBy: 

- GroupBy allows you to perform more aggregations within a KTable. 
- It triggers a repartition because the key changes. 

```java
// Group the table by a new key and key type: 
KGroupedTable<String, Integer> groupedTable = table.groupBy(
    (key,value) -> KeyValue.pair(value, value.length()),
    Serdes.String(), /* key (note: type was modified) */
    Serdes.Integer() /* value (note: type was modified) */
);
```

