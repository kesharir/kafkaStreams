## WordCount Scaling Our Application: 

- Our input topic has 2 partitions, therefore we can launch up to 2 instances of our application in parrallel without any changes in the code!
- This is because a Kafka Streams application relies on KafkaConsumer, and we saw in the Kafka Basics course that we could add consumers to a consumer group by just running the same code. 
- This makes scaling super easy without the need of the cluster. 

## Demo: 

- Run two instances of our kafka streams application
- Start publishing data to the source topic
- Observe our kafka Streams application receive distinct data and still work. 