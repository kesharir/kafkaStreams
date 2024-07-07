## Problem With Atleast Once Semantics AnyWay : 

- Cases when it's ***not acceptable*** to have at least once:
  - Getting the exact count by key for a stream
  - Summing up bank transactions to compute a person's bank balance. 
  - Any operation that is not idempotent
  - Any financial computation. 
- Cases when it's ***acceptable*** at have at least once: 
  - Operations on time windows (because the  time itself can be vague).
  - Approximate operations (counting the number of times an IP hits a webpage to detect attacks 
  and web scraping).
  - Idempotent operations (such as max,min, e.t.c)