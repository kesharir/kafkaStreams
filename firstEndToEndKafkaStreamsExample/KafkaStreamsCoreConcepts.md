## KafkaStream: 

- A **stream** is a sequence of immutable data records, that fully ordered, can be 
    replayed and is fault tolerant (think of kafka Topic as parallel). 
- A **stream processor** is a node in the processor topology (graph). 
    It transforms incoming streams, record by record and may 
    create a new stream from it. 
- A topology is a graph of porcessors chained together by streams. 

### Source Processor: 

A source processor is a special processor that takes its data directly from a 
kafka topic. It has no predecessors in a topology and doesn't 
transform the data. 

### Sink Processor: 

A Sink Processor is processor that does not have children, it sends the stream 
data directly to a kafka topic. 

### Kafka Streams Applications Writing a topology: 

- In this course we will leverage the High Level DSL.
  - It is simple
  - It has all the operations we need to perform most transformations tasks.
  - It contains a lot of syntax helpers to make our life easy. 
  - Its descriptive
- There is also a Low Level Processor API (not in this course)
  - It's an imperative API
  - Can be used to implement the most complex logic, but its rarely needed. 






