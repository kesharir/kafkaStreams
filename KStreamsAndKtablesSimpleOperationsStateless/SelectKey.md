## SelectKey: 

- Assigns a new key to the record (from old key and value)
- == marks the data for repartitioning. 
- Best practice to isolate that transformation to know exactly where the partitioning happens.
- Example: 

```java
// Use the first letter of the key as the new key: 
rekeyed = stream.selectKey((key, value) -> key.substring(0, 1))
// (alice,paris) --> (a, paris)
// (bob, new york) --> (b, new york)
```



