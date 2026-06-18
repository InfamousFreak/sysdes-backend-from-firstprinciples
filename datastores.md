**DATASTORES:**
**highly **space efficient, probablistic data sturcture used to test whether an element is a member of a set, instead giivng us a definitive yes or no, bloom filter trades absolute certainty for extreme speed and minimal memory usage, when query it about an item, it returns 1 of 2 answers : 
- definitely not in the set (100% accurate)
- possibly in the set(small calculable chance of a false positive)

**how it works behind the scenes ? **
a bloom filter is structurally simple : it consists of a bit array of size m (all initially set to 0) and k different independent hash functions

- adding an item : system runs the item through all k hash functions, each hash function outputs a specific position index in the bit array, system changes the bits at those indices to 1
- checking an item : to check if an item exists, the system hashes it using the same k funcs, checks all those array positions 
          - any of those bits are still 0, item definitely does not exist in the set
          - all of those bits are 1, item might exist, **also possible that **combination of other prev items happened to turn those exact bits to 1, causes a **false positive**




**BLOOM FILTERS: **
Bloom filter is a space efficient, probabilistic data structure used in datastores to rapidly test whether an element is a** member of a set. **It serves as a fast, in memory pre filter to prevent expensive disk I/O operations by immediately identifying data that definitely does not exist.

**The core rules of responses: **
when querying a bloom filter for a key (like a user ID or db row) it can only provide 2 answers: 
- definitely not : 100% not in the datastore, no disk lookup required
- probably yes : item might be in the datatsore, system must now search the disk to confirm

as it is probabilistic, bloom filters suffer false positives, but they guarantee **zero false negatives **(never mistakenly say an item absent if it is probably present).

**why use bloom filters : **
LOG-structured Merge Tree (LSM-tree) datastores, such as Apache Cassandra, scyllaDB, rocksDB, Google Bigtable, data is written sequentially to immutable disk files called SSTables

w/o a bloom filter, searching for a non existent key would force the database to read every single SSTable file on the disk to ensure the key is truly missing. by placing a tiny bloom filter in RAM for each SSTable, the db can skip reading almost all files that do not contain key, reduicng disk read amplification drastically 

**hash functions : **uses k independent uniform cryptographic or non cryptographic hash functions, when writing a data key, the key is run through all k hash fucntions, each function outputs an array index, and the bits of those positions are turned to 1.

**lookup : **to check for a key, it is run through the same hash functions, if **any **of the bits at the resulting indices are 0, the item was never inserted, if all are 1, indicates a match 

structural tradeoffs : 
  - extremely lwo memory : require no more thna ~10 bits per element to maintain tiny 1% false positive rate, completely independent of how large the actual data keys are
  - no deletions : standard bloom filters do not support deleting data, Turning a 1 back to 0 might accidentally delete other keys that share that hashed bit index
  - Degradation Over Time : as more elements are inserted into the datatsore, more bits become 1, false positive rate steadily increases until the filter becomes ineffective and must be rebuilt (often done during compaction)

**VALKEY AND REDIs: **utilize bloom filters as a dedicated probabilistic data type layer to quickly screen for fraudulent credit cardss or taken usernames wihtout inflating primary cache size






**DATA REPLICATION : **the process of storing copies of same data across multiple distinct physical servers or nodes, while bloom filters optimize performnace on a single node by reducing disk lookups, data relication ensures the entire system achieves high availability, fault tolerance, and durability across a network

**core purpose of data replication : **solves 3 critical infra problems
- fault tolerance : if one server crashes or a hard drive fails, the database keeps running because other servers hold identical copies of the data
- low latency : by placing replicas in different geographic regions, clients can read data from the server physically closest to them
- read scalability : multiple sevrers can handle read requests simultaneously, prveenting a single machien from becoming a performance bottleneck

**how replication works with LSM trees and bloom filters : **
in distributed datatsores like apachw cassandra, data replication operates in lockstep with local storage engine: 
- **the request : **a cleitn writes a new record to the cluster
- **the routing : **db assigns the recoed to s apecific group of nodes based on a replication factor
- **local storage : **when each node receives its assigned copy, it writes the record to its local LSM tree memory space and commits it to disk logs
- **bloom filter updates : **as these nodes flush data to disk into sstables, each replica node independently generates its own local bloom filters to speed up future read queries on that specific machine

**key concepts in replication architecture : **
- replication technologies : 
            - **leader - follower : **one designated node handles all data writes and replicates them to follower nodes, follower nodes only serve read traffic 
            - **leaderless : **any node can accept write or read requests, nodes coordinate with each other using consensus or quorum mech to ensure data validity

- synchornous vs aysnchornous replication : 
            - synchronous : the db waits for all replicas to confirm they have saved the data before telling the client the write was successful, guarantess **zero data loss **but increases latency
            - **asynchronous : **the main node confirms the write to the client immediately, then copoies the data to other replicas in the backgroud, this is **incredibly fast **but risks minor data loss if the main node crashes before bg copying finishes

- consistency and quorums : 
            - in leaderless datastores, replication uses quorousm to balance speed and accuracy, if you have 3 replicas, a write quorum of 2 means at least 2 nodes must successfully store the data before the write completes, 
                       A matching read quorum of 2 ensures that when reading data, system queries at least 2 replicas to compare timemstamps and return the most up to date version




**HOW ARE NOSQL DBS OPTIMIZED: **
optimized by priortizing horizontal scalaability, predictable latency and high write throughput over the stirtc relational guarantees of traditional SQL systems. They trade complex ACID transactions and runtime JOIN operations for specialized storage formats, localized data layouts and memory cached shortcuts.
