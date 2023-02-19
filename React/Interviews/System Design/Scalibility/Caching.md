It is best to avoid having to go to a DB to retrieve a piece of Data from a Hard Disk, this is an expensive and slow operation.

# Caching Layer

A fleet of servers that maintain a copy of some of the data, it may be the latest requests or the most popular data, in memory in order to return it quickly.
Appropriate for apps that have more reads than writes.

# Expiration Policy
For how long is the data cached? Too long, the data may go stale. Too short and the cache won't do too much good.

Be sure to ask the interviewer the specific requirements.

# Warming the cache
When booting up the system, how do we "fill" the cache without consuming too many resources from whatever we're caching.