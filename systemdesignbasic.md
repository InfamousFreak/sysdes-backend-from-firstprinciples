**SYSTEM DESIGN : **

system design is the process of defining the architecture, components, moduels interfaces and data for a system to satisfy specified requirements. **blue print phase of **building large scale software arpplications, focusing on how different parts of  asytem will interaact, scale an dhandle failures seamlessly.

sysdes deals with high level infrastructure choices, such as choosing betwene databases, mapping data flow, organizing servers

core concepts : 

**scalability** : system's ability to handle growing amounts of work or traffic, includes horizontal scaling (adding more machines) and vertical scaling (adding more power to one machine) 

**availability : **ensuring the system remains operational and accessible even if certain hardware components fail, often measured in nines

**load balancing : **distributing incoming network traffic across multiple servers to prevent any single server from becoming a bottleneck

**caching : **storing copies of frequently accessed data in high peed memory ( like <u>redis</u>) to reduce db load and speed up response times 

**dbs : **choosing the right storage model, such as SQL (relational, structured data) and NoSQL (non relational, highly scalable unstructured data)

**Horizontal Scaling (Scale out) : **multiple same size servers, load balancer redircets
**Vertical scaling (scale up) : **more ram/ cpu to existing server

follows a sturctured framework : 
- requirement classification : defining functional requirements (what the features are and system needs to do), and non funcitonal requirements ( how it perofrms, like bvideos must play inlow latency)
- estimation : calculating the estimated traffic, syorage needs, and bandwidth requirements to size the infrasturcture properly
- API Design : outlining the specific endpoints and communication protocols (like REST or gRPC) that the frontend and backend will use to talk to each other
- Data model : mapping out how data will be stored, linked and indexed in the db layers
- HLD : drawing block diagrams representing the servers, databases caches and queues then identifying potential single points of failure


**CACHING : **process of storign compies of data in a temporary, high speed storage layer so that future requests for that same data can be served mch faster, prevents system from having to repeat expensive operations, like runnign a slow db query, calculating complex data and fetchign resources over a netwrok.


**core concept, cache hit vs cache miss : **cache hit - requested data is found in the cache, system retrieves it instantly, bypassing the lsower main storage

cache miss - data is not in the cache, system must fetch it from the primary source (db), return to user anc write a copy into the cache for next time

**WHere caching happens ? **
- web browser caching : compuetr saves websites files (images, css logos) locally so pages load instantly when you click around or revisit a site
- <u>Content Delivery Network (CDN)</u> : geographically distributed servers cache static website content close to users, worldwide, reducing physical data travel time
- App/DB Caching : software tools like redi sor memcaches store frequent db query results in a server's ram (memory) rather than fetchign them from  a slower hard drive
- CPU Cachign : computer processes use tiny, ultra fast memory layers to store immminent instructions, avoiding slower system ram.

**Common eviction policies : **as cache memory is fast, also expensive and limited in size, when cache is full, must delete old data using spefic rules : 
- LRU (least recently used ) : discards the data that hasnt been accessed for the longest period of time
- LFU (least frequently used ) : discards the data that is requested the least number of times
- FIFO (first in first out) : discards the oldest data added to the cache, regardless of how often it is used

**Cache invalidation : hardest part **of caching is ensuring data stays accurate, if data changes from primary but cache isnt updated, users will see old, incorrect info (stale data). Developers use strategies like TIME - TO - LIVE(ttl, which  sets an automatic expiration timer on cached data, to ensure it refreshes periodically. MUST READ : AWS CACHING GUIDE.




**CONTENT DELIVERY NETWORK (CDN) : **globally distributed network of interconncted proxy servers that speed up the webpage loading times by cachign webiste content closer to where the users physically are. instead of forcing every global user to pull data from a single central host (the origin server), a CDN distributes a traffic load across hundreds of physical locations.


**How a CDN works?**
- **the origin : **you deploy your website or web application onti a central server
- **the edge network : **the CDN copies yor static files, images vids, html, css js to proxy servers positioned at the edge of the internet all over the world
- **user request : **when a user in tokyo visits site, cdn intercepts the req and instantly serves the cached files from a tokyo data center instead of routing the request all the way back to london

**Core benefits of CDN : reduces **latency - drastically slashes the physical distance data has to travel, eliminatign network transmission delays
- **lowers server burden : **as edge servers answer most requests, your origin server saves massive amoutnof compute power and bandwidth
- **mitigates ddos attacks : **large scale networks absord overhwleming psikes of malicious traffic before they can reach and crash main website

MUST READ : Cloudflare CDN




**DATABASE INDEXING **
**: **is a data structure technique used to quickly find and accress specific rows in a db table without searchign throguh every single row, acts exactly like the index of a book, 

**how indexing works under the hood ? **
when an index on the table column is created, db creates a separate highly organized pointer structure (most commonly B-Tree or HashMap).

- **the search** : run a query looking for a specific value (WHERE user_id = 4502)
- **index lookup** : db engine searches tiny, ordered index file first, because index is sorted, it finds the value almost instantly using efficient binary search
- **the pointer jump : **index tells the db exactly where that row lives on the physical hard drive, database jumps straight to that memory slot and retrievs the data


**Trade off : Read Speed vs Write Speed : **

while indexign makes fetchign data incredibly fast, it comes with a strict cost that developers must balance: 
- **slower writes : every time **we insert delete or update data in a table, the db has to update both the main table and recalculate the sorted index strcture
- **storage space : **indexes require additional disk space and memory to hold the pointer tables, if you index every colum blindly, your index files can easily become larger than actual data table

**Primary types of indexes : clustered index - **determines the physical, chronological order of data rows in the table, because data can only be physically sorted one way, a table can only have **one **clustered index (almost always assigned to the primary key)

**non-clustered index : **completely separate structure from the data rows, contaisn a sorted copy of the chosen column along with a physical pointer pointing back to thw row, can create multiple non clustered indexes on a single table

**composite index : **an index built on multiple columns combined (indexing last_name and first_name together) to speed up complex multi variable searches 



**DATABASES**
** : **organized electronic collection of structured data stored and accessed digitally from a computer system, unlike simple spreadsheet, database is specifically designed to securely hold massive volumes of information allow thousands of users to query or update data at the exact same time, and ensure that data remains accurate and uncorrupted. 

managed by a software app known as **DBMS (database management system) **which handles the complex background tasks of reading, writing and organizing the physcial files of a hard drive


**PRIMARY CATEGORIES OF DATABASE: **
modern software engineering divides databases into two main types based on how they structure data : 

- **RELATIONAL DATABASES (**sql) : store data in rigid, predefined tables consisting of rows and columns, similar to spreadsheets, use SQL(structured query language ) to manage data and highly optmised for complex trackign and transaction safely, examples include postgresql, mysql, sqlite

- **NON RELATIONAL DATABASES (noSql) : **these store data in flexible formats rather than struct tables, built to handle massuve scale, unstructured data and rapid architectural cahnges, common formats include doucments (mongodb), <u>key value pairs (Redis), wide columns(Cassandra) and graphs (Neo4).</u>

**4 core operations CRUD : **
- Create : insertign new data rows or documents into the system
- Read : searching filtering and retriveing existing records
- update : modifying details of records already saved in storage**​**
- delete permannelty : permanently removing records from the system

**why not just use an exce spreadsheet ?**
while excel excellent for individual analysis, completely fail at softwrae scale due to 3 main limitations : 
  - **concurrency  : **if 10000 people try to book a seat on a flight at the exact same time, a spreadhseet will look up or overwrite data, a database uses concurrency controls to process transactions safely without conflicts

- **scale **: spreadsheets slow down to a crawl after a few 100 thousand rows, db can seamlessly manage billions of rows across multiple connected hard drives

- **data integrity  : **databases enfore strict validation rules, for eg, a database can guarantee that a suer cannot accidentally type letters into a "Phoen number" or "Price" column
**must read : oracel db archi guide, review open source db design**


**RELATIONAL DATABASE **
**: **type of db storing organizifn data pts related to one another in rigid, predefined tables, this model organizes data into rows and column, where each row represnets a unique record (an instance), and each column represents a specifc attribute (a field). 

Consists of an **entity - relationship diagram (ERD), visually mapping out the structure of a relational database. **instead of showing actual data entries, diagram shows the blueprints for the tables, **attributes(columns) and how they connect to each other.**

**Attributes : **fields - individual text items listed inside each box, columns for that specific data row, **whenever a new passenger is added, the db requires these specific pieces of information for them**

**Records : **are not directly visible in this blueprint because it is just a template, a record is created only when actual data is typed into these tables. Like actually a passesnger 1 signs up, the whole row with all the real data entered into the fields / attributes, will together become a record. **The box in the erd is not a record, its a table.**

**Key structural features : **
- tables (entities) : each independent blue headed box represents a single table
- Primary keys (icon) : the top attribute in each table with a key icon **uniquely identifies every single record so they never get mixed up**
- **Relationships : **lines connceting the tables show how data in one table relates to another, for instance, the line bwteen passenger and booking ensures that abooking record is always linked to a specifc passenger. **Must read : crow foot's notation for db design**

**NOSQL DBS : **
**nosql aka,​ ​ **not only sql, are non relational dbs, unlike structured layout of rows columns and tables we see diagram, nosql dbs do not use rigid tables to organize information.

Instead they use flexible dynamic models designed to handle massive scale undormatted data and rapid structural changes

**4 types of no sql dbs - **depending on which kind of data we are storing
- document dbs : instead of sepaating a person's name, address, and bookings into different tables, this format groups everythign into a single "document" file.
    - a passenger and allt heir flight histroy is stored in one single file, each file can have completely different attributes without breakign the syste,
    - **mongodb**, couchbase

- Key-value stores : simplest form of database, acts like a giant dictionary where every piece fo data has a unique key linked directly to value
    - key user_101 -> value john doe
    - REDIS, amazon dynamodb

- Wide column (colum family) stores : traditional dbs look data line by line horizontally, wide oclumn dbs store data vertically in columns
    - how it works : format lets you process massive global datasets quickly because the db can bypass billions of rows and scan only the exact column fields it needs
    - apache cassandra

-  Graph Databases : these focus purely on the connections and relationships between data points 
    - data saved in circles (nodes) and lines(edges) , used heavily to spot patterns, like manual friends on a social network or tracking farudulent credit card activity
    - neo4j,,,, must read : mongodb nosql dbs

NOSQL DB FEATURES : 
- distributed computing 
- soaling 
- flexible schemas and rich query language
- ease of use for devs
- partition tolerance
- high availability

**base compliance : nosql dbs **are base compliant, basic availability soft state eventual consistency, basic availability is the ability of the system to tolerate a partial failure. soft state means that the system allows temporary inconsistencies before eventually achieveing consistency automatically over time.  also can be configured to provide **multidocument ACID compliance.**


**THRASHING : **
**critical **performance problem that occurs when an os spends more time swappign data in and out of memory than actually executin tasks, makes the computer freeze lag severly or become complete unresponsive

**how thrashing happens ? **when computer runs low on physical memory RAM, uses hdd or sdd for temporary extra memory, known as virtual memory. 
- memory full : open too many heavy apps, ram runs out of space
- page fault : cpu tries to execute a program, but the data it needs is not in the RAM, it has been moved to the hard drive, called page fault. (must read the knowledge academy article)
- Constant swapping : os pauses the app, copies a piece of datafrom ram to hard drive, and pulls the required data into the ram
- the Trap : because so many apps are open, every app immediately demands its data back, system gets stuck in a loop of continuously moving data back and forth between the RAM and the hard drive

**major causes of thrashing : **
- too many active programs (high multiprogramming) : loading more applications than the physical ram can comfortably hold
- insufficient ram : hardware simply does not have enough capacity to handle the working set (the active data) of software running on it
- Poor os management : sometimes, cpu usage drops because it is waiting on the hard drive, operating system mistakenly thinks the computer is idle, tries to start even more tasks to fix this, making the thrashing significantly worse. 
must read gfg thrashing guide

**how os stop thrashing : **
- working set model : os tracks exactly how many memory pages an active app regularly uses, total memory demanded by all apps exceeds available RAM, OS will pause suspend some programs entirely until resources free up
- Page fault frequency : os sets  aspeed limit for page faults, if an app triggers page faults too rapidly, os gives more ram frames to restrict other processes


**THREADS : **
smallest unit of execution within an operating system, often called the lightweight process,   think of a **Process** as an enitre running application and** Threads **as the individual workers inside the app runnign different tasks at the same time

**how threads work : **
- process : the kitchen, has its own rented space, water supply and master recipe book
- threads : individual chefs working inside that kitchen, all share the same space, sam eingredients, same tools but chef a is chopping smth, b is boiling smth, c is plating smth

as they are in the same room, they can talk to each other instantly, however if chef a accidentlally slips and knocks over the stove, whole kitchen stops working


**key characteristics of threads : **
- shared memory : threads belongign to the same porcess share the apps code, data and system resources , makes it incredibly fast for them to comunicate with one another
- independent execution : each thread has its own program counter (which instructiion to run next) , registers (to hold temp calculation), and stack (to track active function calls)
- Low overhead : creating or switching between threads takes significantly less time and computer power than starting an entirely new process

**why threads matter in system design : **
leverage threads to maximise hardware utlization and minimize response times for users
- concurrency : threads allow a single <u>system component</u> to handle thousands of simultaneous user requests
- resource efficiency : unlike separate processes, threads within the same process share memory space, making communication ebtween then incredibly fast
- asynchronous processing : systems can offload slow tasks (writing to db or calling to api) to bg threads, leaping the main application responsive

**key threading models : **
designign a distributed system or a backend service, must choose how your application handles threads : 
- thread per request : system assigns a dedicated thread to every incoming netweok request, model is straightforward but hits a hard ceilign because os threads cosnume significant memory and cpu overhead
- event driven / non blocking  : small pool of threads handles al incoming traffic using an event loop, when a request waits for data, the thread immediately moves to another task, maximising throughput
- virtual threads : modern alt where millions of ultra lightweight threads run on top of small pool of hevay os threads, giving us the simplicity of thread per request with theperformance fo event driven design

**common architectural challenges : **
- race conditions : two threads trying to modify the same piece of data at the exact same time, causing data corruption
- deadlocks : thread a is waiting for thread b to release a resource, while thread b is waiting for thread a, freezing that part of the system entirely
- thread starvation : low priority threads are perpetually denied cpu time because high priority threads consume all available resources
- context switching overhead : having too many ative threads forces the cpu to spend more time swappign between them than actually executing your code

**core solutions used by sys desns : **
- thread pools   : instead of creating new threads on the fly, systems remained a fixed queue of pre allocated threads to manage incomign workloads safely
- immutability   : designing data strutcures that cannot be changed after creation, eliminating the risk of race conditiosn entirely
- message queues   : decoupling thread execution by placing tasks into a queue (apache kafka or rabbitmqq) allowing bg worker threads to process them at their own pace









<u>​</u>
