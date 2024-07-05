## Favourite Colour App Hint: 

### Observation: 

- The input data does not have keys, but represent updates. 
  - We should read it a KStream and extract the key
  - We should write the result to Kafka (as a log compacted topic)
- The results can now be read as a KTable so that updates are correctly applied.
- We can now perform an aggregation on the KTable (groupBy theh count)
- And write the results back to Kafka 

### Hint: 

- Read one topic from Kafka (KStream)
- Filter bad values
- SelectKey that will be the userId
- MapValues to extract the colour (as lowercase)
- Filter to remove bad colours
- Write to Kafka as intermediary topic
- Read from Kafka as a KTable 
- GroupBy colours
- Count to count colours occurrences 
- Write to Kafka as final topic