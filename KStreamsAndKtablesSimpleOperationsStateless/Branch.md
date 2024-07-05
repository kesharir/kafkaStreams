## Branch: 

- Branch (split) a KStream based on one or more predicates.
- Pedicates are evaluated in order, if no matches, records are dropped. 
- You get multiple KStreams as a result. 

```java
KStream<String, Long>[] branches = stream.branch(
        (key, value) -> value > 100, /* first predicate */
        (key, value) -> value > 10, /* second predicate */
        (key, value) -> value > 0 /* third predicate */
);
```