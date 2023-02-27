What happens when something goes wrong?

What happens when an entire region goes down?

![[Pasted image 20230219170455.png]]

Before we hit a Load Balancer we can have a Router that directs traffic coming from a region to a region-specific Load Balancer, that way a request coming from NA will be served from the NA fleet of servers and DBs.

This allows us to increase resiliency by having fallbacks. For example, in case EU goes down we can send traffic coming from EU to one of the Balancers of India or NA.

# Tips
- Spread secondary servers in different racks, availability zones and even regions.
- Make sure the system has enough capacity to handle another entire zone going down. This means over-provisioning sites.
- We must balance budget vs availability. Not every system needs this fail safe, it all depends on the requirements laid out by the interviewer.
