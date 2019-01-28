[//]: # (#CPU caches)

## Fundamentals
1. cache miss: 
   You want a piece of data, but it is not ready waiting in the cache
2. false sharing: 
   It happens when different threads are accessing the same cache line simultaneously, not the same data though. As soon as one thread writes to that cache line. The same cache line will be marked dirty across all the other cores and those cores who are accessing the same cache line will need to refetch the cache line from the main memory.