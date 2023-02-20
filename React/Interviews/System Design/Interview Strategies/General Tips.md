# Clarify Requirements

Ask a lot of questions. Think out loud.

# Working Backwards

Start from the customer experience. For example: Start asking where does the content come from? How do we store it? Which regions do we must serve (do we need CDNs?)? How is the data catalogued in the CDN?

WHO are the customers? Geo location, time-zones. What are their use cases.

# Define Scaling Reqs

Thousands vs Millions of users?
Define the scale of data.
Vertical scaling can work for smaller use cases. 

# Define Latency Reqs

Do we need cache and CDN?
Define the three-nines SLA.

# Define Availability Reqs
Is being down a threat to the business?
If high availability is required, we must avoid single points of failure.

h