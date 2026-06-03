LOAD BALANCER : **load balancer is a device or software component that acts as a traffic cop, distributign incoming network requests acorss a pool of backend sevrers**

**- sits between the user and server infra, ensuring no single server becomes overwheled, which prevents slowdowns and webisite crashes**

key benefits : **high availability - if backend server crahses, load balancer automatically detects the failure and redicets usrs to healthy servers, keeping the application online**

**smart scalability - alows a business to add or remove servers seamlessly without users ever experiencing donwtime or noticing a change**

**enhanced security : by acting as a single entry point, it shields the underlying servers from direct public internet  exposure and can help mitigate ddos attacks**

****common routing algos : ****
**- Round Robin : requests are distributed sequentially down the list of servers in a continuous loop **
**- Least connections : requests are sent to the server that is currently handling the fewest active user sessions**
**- IP Hash : user's ip address determines which serve rhandles their request, ensuring that a specific user always reconnects to the same server**

Hardware vs Software Load balancers : **load balancing originally required expensive dedicated physical appliances deployed in corporate data centers. Today while hardware options still exist ffor specialized enviromemts, most modern systems rely on lightweight software solutions (NGINX and haproxy) or cloud managed services.**


**SHARDING : **
diving traffic or infrastructure into isolated segments(shards) so that specific requests are consistently routed to a specific subset of resources,  while traditional load balancing randomly or sequentially distributes incoming requests acroess an interchanegable pool of servers, **sharding introduces data or contextual routing into the traffic distribution layer**

**2 ways sharding and load balancing interact : **
- sharding the load balancer infra itself (horizon scalign)    : when net traffci too massive for single load balancer, the infra itself is sharded
              - deploy multiple independent load balancers, use DNS service like amazon route 53, to split the total client volume into smaller "shards" across these balancers
              - it prevents the load balancer from becoming a single bottleneck and isolates structural railures to just one subset of users

- shard aware load balancing (data driven routing )     : backend data tier or app servers are sharded and the load balancer must act intelligently to route traffic to the exact server that holds that specific data
              - instead of treating all backend servers equally, the load balancer inspects incoming requests (checks user auth tokens, url paths, cookies), runs a routing algo such as **consistent hashing **to send user a's requests exclusively to server shard 1, and user b's requests to server shard 2.


**server equality       **
all backend servers are identical clones and can handle any request         backend servers hold unique partiotioned slices of the system data
**routing logic           **
uses abstract metrics like round robin, least connections or random choices      uses strictural attributes like hash based keys, tenant id or geographic region
**state management       **
state is usually stored externally( stateless application layer)      state or data is tightly localized to specific compute nodes
**blast radius       **
if a backend bug or bad query crashes a server, the load balancer routes traffic to others      if a shard crashes, only the users mapped to that specific shard are impacted

**core benefits of sharded load balancing : **
- eliminates cross node communication : cause a user's request is directly routed to exact machine housing thier data, the server doesnt have to waste time querying other internal servers
- **optimizes localised caching : **since a servrr only processes requests fora a specific shard of users, its internal memory cache remains highly relevant local data longer, driving up cache hit ratios
- **mitigates system wide outages : **instead of a massive spike in global traffic bringin down the entire system, a single overloaded hotspot will only degrade performance for a fraction of your user base






