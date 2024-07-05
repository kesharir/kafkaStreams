## Streams marked for re-partition: 

- As soon as an operation can possibly change the key, the stream will be marked for repartitition
  - Map
  - FlatMap
  - SelectKey
- So only use these APIs if you need to change the key, otherwise use their counterparts: 
  - MapValues
  - FlatMapValues
- Repartitioning is done seamlessly behind the scenes but will incur a performance cost (read and write to kafka).

