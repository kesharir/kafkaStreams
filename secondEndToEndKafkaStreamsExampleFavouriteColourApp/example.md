## Example: Favourite Colour App

- Write your own advanced Kafka Streams application using the operations we saw in the previous section: 
- Take a comma delimeted topic of userId, colour
  - Filter out bad data
  - Keep only colour of "green", "red" or "blue"
- Get the running count of the favourite colours overall and output this to a topic.
- !!! A use's favorite colour can change.

### Example:
    - stephane, blue
    - john, green
    - stephane, red (update here!)
    - alice, red

***Output:***
```
blue: 0
green: 1
red: 2
```

## Favourite Colour App Guidance: 

- Write topology
- Start finding the right transformations to apply (see previouus section)
- Creating input and output topics (and intermediary topics if you think of any)
- Feed the sample data as a producer
  - stephane, blue
  - john, green
  - stephane, red
  - alice, red

