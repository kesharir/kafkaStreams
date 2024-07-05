## KStreams:

- All inserts 
- Similar to a log
- Infinite
- Unbounded data streams

- Example:
(alice, 1)
(marc, 4)
(alice, 2)

## KTables: 

- App upserts on non null values
- Deletes on null values
- Similar to a table 
- Parallel with log compacted topics. 


- Example:
Topic: 
  (alice, 1)
  (marc, 4)
KTable:
    (alice, 1)
    (marc, 4)

(alice, 1)
KTable:
(alice, 1)
(marc, 4)

(marc, null)
KTable:
(alice, 1)


## When to use KStream vs Ktable ? 

- KStream reading from a topic that's not compacted. 
- KTable reading from a topic that's log-compacted (aggregations).
- KStream if new data is partial information/transactional. 
- KTable more if you need a structure that's like a database table, where every update is self sufficient.
  (think - total bank balance)


