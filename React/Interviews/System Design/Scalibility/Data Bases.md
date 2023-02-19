# Cold Standby

We have another server almost ready to take the place of the main server in case of failure. We use one of the periodical backups to restore the information on the "new" server. We must reroute all the traffic to the new server. 

This requires to tolerate downtime and data-loss.

# Warn Standby

We have a server replicating all the info from the main server. The routing to the new server can be done really fast. Is fairly simple to implement. The replicating is managed by directly by the DB.

# Hot Standby

We make the same operation in all the DB servers.

# Sharding

![[Pasted image 20230219151440.png]]We can have shards managing different data, each with its own backup. The router should know which Shard manages which information. Combining data from Shards is complicated and should be avoided.

## MongoDB & NoSQL DBs
Usually these types of DBs are sharded by default, they are built to handle sharding automatically or with very little configuration.

### Issues:
- Resharding: When adding a new shard for scaling, which data goes in the new shard and which data do we delete from old shards.
- Hotspots: If a shard contains data that has way more traffic, we need a way to distribute that load.

### Denormalizing

![[Pasted image 20230219153049.png]]

Is usually better to start with normalized data, because updates are way easier to implement. Later, if the app is suffering from low performance, we can move to using denormalized data to speed up the response time of the retrieval queries. If for the client is more important to answer fast to a READ operation than to an UPDATE, denormalize is the way to go.

# ACID Compliance

## Atomicity
The entire operation should succeed or fail. There can't be leftovers operations after a failure midpoint.
## Consistency
All the rules must be applied to all transactions, otherwise the transaction must rollback.
## Isolation
No transaction should be affected by any other transaction that is still in progress.
## Durability
A committed transaction should stay committed even if the system crashes.

# CAP Theorem
A DB can't be good at everything, it has to trade something off. Generally DBs are good in two things, and must sacrifice the 3rd one. For example, NoSQL DBs have fairly good Consistency and Partition-Tolerance, but they must sacrifice Availability, because they usually have a Master Node that acts as Single Point of Failure.

## Consistency
How fast can newly written data be retrieved? If I write data, how long does it take to move through all my shards?

## Availability

How much downtime can we expect from a DB? How many points of failure do we have?

## Partition Tolerance
How easy is to scale the DB?

![[Pasted image 20230219161649.png]]
