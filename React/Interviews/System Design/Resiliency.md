What happens when something goes wrong?

What happens when an entire region goes down?

![[Pasted image 20230219170455.png]]

Before we hit a Load Balancer we can have a Router that directs traffic coming from a region to a region-specific Load Balancer, that way a request coming from NA will be served from the NA fleet of servers and DBs.

This allows us to increase re