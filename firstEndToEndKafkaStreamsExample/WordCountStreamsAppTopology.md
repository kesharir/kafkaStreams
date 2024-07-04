## WordCountStreamsAppTopology: 


- Lets write the topology using the High Level DSL for our application.
- Remember data in Kafka Streams is <Key, Value>. 

1. Stream from Kafka <null, "Kafka Kafka Streams">
2. MapValues lowercase <null, "kafka kafka streams">
3. FlatMapValues split by space : 
   <null, "kafka">,
   <null,"kafka">,
   <null,"streams">
4. SelectKey to apply a key :
   <"kafka", "kafka">,
   <"kafka","kafka">,
   <"streams","streams">
5. GroupByKey before aggregation :
   (<"kafka", "kafka">,<"kafka","kafka">),
   (<"streams","streams">)
6. Count occurences in each group : 
    <"kafka", 2>, <"streams", 1>
7. **To** in order to write the results back to Kafka 
    data point is written to kafka