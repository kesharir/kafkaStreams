## Activity: 


1. Create a producer topic: 

```shell
kafka-topics.sh --bootstrap-server localhost:9092 --create \
  --replication-factor 1 \
  --partitions 1 --topic \
  favorite-colour-input
```

```
Created topic favorite-colour-input.
```

2. Create a intermediate topic:

```shell
kafka-topics.sh --bootstrap-server localhost:9092 --create \
  --replication-factor 1 \
  --partitions 1 --topic \
  favorite-colour-intermediate
```

```
Created topic favorite-colour-intermediate.
```

3. Producing to "favorite-colour-input" topic:
```shell
kafka-console-producer.sh --bootstrap-server localhost:9092 \
  --topic  favorite-colour-input
```

***Input Data***
```shell
>stephane,red
>ritanshu
>ritanshu,green
>ritanshu,blue
>anushree,green
```

```shell
kafka-console-consumer.sh --bootstrap-server localhost:9092 \
   --topic favorite-colour-intermediate   --from-beginning \
   --property print.key=true   --property key.separator=,
```
***Output Data to intermediate topic:***

```shell
stephane,RED
ritanshu,GREEN
ritanshu,BLUE
anushree,GREEN
```

4. Create a output topic:

```shell
kafka-topics.sh --bootstrap-server localhost:9092 --create \
  --replication-factor 1 \
  --partitions 1 --topic \
  favorite-colour-output
```

```
Created topic favorite-colour-output
```

***Now again inputting data to "favorite-colour-input" topic:***
```shell
>stephane,red
>stephane,red
>stephane,red
>ritanshu
>ritanshu,green
>ritanshu,blue
>anushree,green
>vishal,red
>ritanshu,green
>anushree,green
>anushree,blue
>ritanshu,blue
>ritanshu,blue
>ritanshu,blue
>ritanshu,blue
>ritanshu,red
>anushree,red
>anushree,blue
```

5. Consuming the messages from the output topic: 

```shell
kafka-console-consumer.sh --bootstrap-server localhost:9092 \
  --topic favorite-colour-output \
  --from-beginning \
  --formatter kafka.tools.DefaultMessageFormatter \
  --property print.key=true \
  --property print.value=true \
  --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer \
  --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
```

```shell
RED     1
BLUE    1
GREEN   1
RED     2
BLUE    0
GREEN   2
GREEN   1
BLUE    1
GREEN   0
BLUE    2
BLUE    2
BLUE    2
BLUE    2
BLUE    1
RED     3
BLUE    0
RED     4
RED     3
BLUE    1
```