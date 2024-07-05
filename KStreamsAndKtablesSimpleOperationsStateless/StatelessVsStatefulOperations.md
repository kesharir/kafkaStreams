- Stateless means that the result of a transformation only depends on the data-point you process.
  - Example: a "multiply value by 2" operation is stateless because it doesnot need memory of the past to be achieved.
    - 1 => 2
    - 300 => 600
- ***Stateful*** means that the result of a transformation also depends on an external information - the state
  - Example: a count operation is stateful because your app needs to know what happened since it started running in order to know the computation result.
    - hello => 1
    - hello => 2

