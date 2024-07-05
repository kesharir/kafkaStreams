## Refresher On Log Compaction: 

- Log compaction can be a huge improvement in performance when dealing with KTables because eventually records get discarded. 
- This means less reads to get to the final state (less time to recover).
- Log Compaction has to be enabled by you on the topics that get created (source or sink topics).

W- atch This Later : https://marcelclasses.udemy.com/course/kafka-streams/learn/lecture/7636558#overview