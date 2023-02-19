It is best to avoid having to go to a DB to retrieve a piece of Data from a Hard Disk, this is an expensive and slow operation.

# Caching Layer

A fleet of servers that maintain a copy of some of the data, it may be the latest requests or the most popular data, in memory in order to return it quickly.
Appropriate for apps that have more reads than writes.

# Expiration Policy
For how long is the data cached? Too long, the data may go stale. Too short and the cache won't do too much good.

Be sure to ask the interviewer the specific requirements.

# Warming the cache
When booting up the system, how do we "fill" the cache without consuming too many resources from whatever we're caching.

# Eviction Policies
- LRU Least Recently Used. We can maintain a HashMap where the keys point to where in the Cache they're stored, when we access an item, we move it to the Head of the Linked List. When the cache needs to free up space, we can Evict the tail from the List.
![[Pasted image 20230219165123.png]]
- LFU Least Frequently Used
- FIFO

# Cache Technologies

- Memcached: One of the most used until Redis came. Pretty simple to use, its just a in-memory key/value store.
- Redis: Has a lot more features.