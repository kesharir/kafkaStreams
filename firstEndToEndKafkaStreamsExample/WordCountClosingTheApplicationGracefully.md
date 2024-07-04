- Adding a shutdown hook is key to allow for a graceful shutdown of the Kafka Streams application, which will help the speed of restart.
- This should be in every Kafka Streams application you create. 

```
// Add shutdown hook to stop the Kafka Streams threads.
// You can optionally provide a timeout to `close`
Runtime.getRuntime().addShutdownHook(new Thread(streams::close));

```