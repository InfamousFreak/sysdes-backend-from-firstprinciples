SKILLS : 

**SQL : **structured query language, standard prog language used to communicate with, manage and manipulate data stored in relational databases

If a database is like a collection of highly organised spreadsheets , sql is what u use to ask that sheet questionsm add new rows, or update existing information


SQL DOES : 4 CORE OPS
- almost everything sql does boils down to 4 fundamental tasks : 
    - CREATE (INSERT) : adding new user to a website after they sign up
    - READ (SELECT) : askign the database ot find and show you specific information
    - UPDATE (UPDATE) : change existing data inside the tables
    - DELETE (DELETE) : permannelty moving records

**WHY IS SQL SPECIAL?**
- it handles massive scale efficienlty : while progs like excel slow or crash handlign millions of rows, sql db can store, search and filter hundreds of millions of records in fractions of a second

- strict structure and data integrity : sql db use a rigid layout called schema, ensures thr data remains clean, if a column is configured to hold *date, *sql will physically block anyoen from accidentaly typing a text string other than date into that box

- it is a universal standard : whether i use a open soruce db system like postgresql or mysqlm or enterprise system like oracle or ms sql server, they all use exact same foundational sql language, learning it once allows you to work across almost any tech stack.

**BLOCKCHAIN : **

**blockchain is a **decentralized digital ledger that securely records transactions across a network of computers, instead of relying on a single central authority like a bank, visa netwrok or tech company to keep track of balances and data, the entire network maintains and verifies the ledger simulataneously

HOW IT WORKS ?

- the ledger : imagine a shared google sheet where everyone has aview only copy, but no sinfle person can edit it arbitrarily
- blocks : transactions are grouped together into a block
- the chain : once verified by the netrwork using cryptographic algorithms, this block is securely linked to the previous block using a unique digital fingerprint (a hash). 


**PROXY SERVER**

** : **INTERMEDIARY SERVER that sits between a user's device and the internet, actign as a gateway for all your nnetwork traffic. When using a proxy, internet reqs travel through a proxy server first, which then evaluates the request perfoms security chcks,and forwards it to the destination webist e on your behslf

the website sees the proxy server identity and ip addeess, our data is safe.

Forward proxy (client side) - sits in front of clients, interncepts outgoing reqs from private network to public internet, businesses often use them to block employees from visitng speifc websites filter out malware or hide the users real internal ip addresses.

Reverse proxy (server side) - sits in front of web servers, intercepts incoming reqs from public internet before they reavhthe backend db, this is the architecture used by load balancers, api gateways and cdns to protect, optimize and scale web applications. 

**benefits and use cases : **privacy and anonimity - by maskign original ip with its own, a proxy prevents webistes from tracing your precise physical location and network footprint

content filtering and control : organizations use proxies to restrict access to unsafe or distracting websites, conversely individuals sometimes use proxies to bypass school or workplace network restricttions

caching and speed : just like caching concepts, proxy can save copies of frequently visited websites, instalty returning from local cache

security shielding : prevents direct connection attempts from the outside world into a private network, acting as an extra layer of defense against hackers


PROXY VS VPN  : proxy - layer 7, only reroutes traffic from a specific application configured to use it, such as your web browser or a torrent client, most standard proxies dont encrypt our data

 VPN (virtual private network) : layer 3 - os level, captures and rerooutes and fully encrypts 100 % of all internet traffic leaving you device, makign it much more secure for public networks 


**DDoS Attacks : **distributed denial of service attack is amalicious attempt to disrupt the noraml traffic of a targeted sevrer, service or network by overhwein it with a flood of internet traffic.  Unlike a standard dos attack, which originates from a single computer, ddos attacks use a vast, distributed network of compromised devices acorss the globe to stroke a single target simultaneously. 

massive influx of fake traffic clogs the network pipelines, causing the website app to slow down dramatically or crash for real users


**the BOTNET (how ddos works) : **ddos attack relies on a network of hijackd, internet connceted machines : 
- infectio : attackers infect thousands or millions of devices, such as pc, phones, smarthome iot devices(sec cam or routers) with malware
- botnet : these infected devices become bots or zombies and collectively they form a botnet controlled remotely by the attacker (the botmaster)
- the strike : attacker instructs botnet to send a massive wave of coordinated requests to the target's IP address, as each bot is a legit device with real ip address, separating the malicious flood from real customers traffic is incredibly difficult.

Common types of DDOS attacks : these attacks generally target different layers of network infrastructure and are classified into three main categories : 
- **volumetric attacks : **goal is to completely consume all available bandwidth between target and larger internet, attackers often use amplification techniques like NTP or DNS amplification, to turn tiny requests into massive tidal waves of data.

- protocol attacks : focus on exhausting the actual processign resources of network infrastructure equipment, such as firewalls, routing tables or load balancers, common example is **SYN FLOOD, **exploits the standard TCP handshake mechanism to leave connections hanging open until the server runs out of memory

- application layer attacks (layer 7 ) : stelthier attacks that atrget the specific application layer where web pages are generated, by mimicking human behaviour (such as repeatedly refreshing an expensive db heavy search query) a small botnet can exhaust server cpu power without needing massive network bandwidth.


**Preventing ddos : since attacks are from a network, blocking one IP will not work**
- anycast routing or cdns : utilizing a globally distributed network, like cdn, lets u absord and scatter the massive influx of traffic accorss hundredsof edge servers worldwide before it can ever reach yourmain origin server

- rate limiting : network admins restrict the number of requests to a single user or IP address can make a within a specific timeframe 

- web aplication firewalls : a WAF implements customized rulesets to analyze traffic patterns at the application layer, allowing it to filter out automated bot behaviours while lettign human traffic pass through 

MSUT READ : cisa ddos quick guide


**system component : **
a system component is a self contained, modular building block of application that handles a specific isolated responsibility, interacts with other components through clearly defined boundaries or interfaces

is like a lego brick : hidden internal structure, but pegs allow it to snap into other blocks

**how components connect to threads : **
a component is a structural unit (machine code or logic), while a thread is the execution unit (the engine that runs that logic), 

**core traits of a system component : **
- encapsulation : it hides its internal data logic, other parts of the system cannot see how it works, only what it outputs
- reusability : is designed so it can be plugged into different parts of the system (for entirely diff projects) withotu reqriting the code
- independence : can be developed, tested and updated in isolation without breaking the rest of the application 

**user auth -> login service -> verifies passwords, issues security tokens, and blocks bad actors**
**notification engine -> email sms sender -> accepts a message payload and pushesh it to external dleivery apis**
**db wrapper -> data access layer (dal) -> manages connections, safely queries data, and prevents corruption**
**cachign layer -> redis integration -> temporarily holds frequently read data to speed up system response times**


 

