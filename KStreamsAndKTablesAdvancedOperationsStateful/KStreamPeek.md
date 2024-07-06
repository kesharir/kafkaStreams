## KStream Peek: 

- Peek allows you to apply a side-effect operation to a KStream and get the same KStream as a result.
- A side effect could be: 
  - printing the stream to the console.
  - Statistics collection,
- Warning: It could be executed multiple times as it is side effect (in case of failures). 

```java
KStream<byte[], String> stream = ....;

// Java 8+ example, using lambda expressions
KStream<byte[], String> unmodifiedStream = stream.peek(
        (key,value) -> System.out.println("key=" + key + ", value=" + value)      
);
```