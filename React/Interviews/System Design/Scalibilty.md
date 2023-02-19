# Single-server design
Personal projects. Low-traffic. DB in the same server.
This is a single point of failure.

# Vertical scaling
Use a bigger server, more powerful. You can only grow a single server until certain point. Still a single point of failure.

# Horizontal Scaling

We have a Load Balancer routing traffic to a fleet of servers. All the servers can point to the same DB server. We add more servers to the fleet when the traffic is heavier, it can theoretically scale infinitely.

## Stateles servers

A request received by any given server, should not depend on the state of any previous request in the system. This means that any server in the fleet can handle any request in any time.


# DB Scaling

## Cold Standby

We have another server almost ready to take the place of the main server in case of failure. We use one of the periodical backups to restore the information on the "new" server. We must reroute all the traffic to the new server. 

This requires to tolerate downtime and data-loss.

## Warn Standby

We have a server replicating all the info from the main server.
