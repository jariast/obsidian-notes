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

