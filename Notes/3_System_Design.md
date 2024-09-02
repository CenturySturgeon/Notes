### Fundamentals

#### Chapter 1 Reliable, Scalable, and Maintainable Applications

- **Availability**: Percentage of time a system or service is operational and accessible when needed. It is a measure of how often the system is up and running compared to the total time it should be available.

  - Two nines '**99%**' Availability means the service is down around 3.65 days a year.
  - Every aditional nine decreases the downtime by an order of magnitude of roughly 10 times:

    | Availability | Downtime           |
    |--------------|--------------------|
    | 99%          | 3.65 days/year     |
    | 99.9%        | 8.77 hours/year    |
    | 99.99%       | 52.6 minutes/year  |
    | 99.999%      | 5.26 minutes/year  |
    | 100%         | 0 seconds/year     |
 

- **Reliability**: Measures how consistently and correctly a system performs its intended functions over time without failure. It indicates the system's ability to operate without errors or breakdowns when in use.
  
  - *Measurement*: Often assessed using metrics such as Mean Time Between Failures (MTBF) or Mean Time to Failure (MTTF). These metrics quantify how long the system performs correctly before encountering a failure.

- **Redundancy**: Redundancy refers to the inclusion of extra components or systems to ensure that a system can continue to operate in the event of a failure. It is a design approach that involves adding duplicate resources to increase reliability and availability.

  - *Hardware Redundancy*: Adding spare hardware components (e.g., additional servers, power supplies, or network links) that can take over if primary components fail.
  - *Data Redundancy*: Replicating data across multiple storage devices or locations to protect against data loss.
  - *Geographic Redundancy*: Distributing resources across different locations or data centers to protect against site-specific failures.

- **Maintainability**: Over time, many different people will work on the system (engineering and operations, both maintaining current behavior and adapting the system to new use cases), and they should all be able to work on it productively.
  - Operability: Make it easy for operations teams to keep the system running smoothly.
  - Simplicity: Make it easy for new engineers to understand the system.
  - Evolvability: Make it easy for engineers to make changes to the system in the future

- **Fault**: One component of the system deviating from its spec.

- **Failiure**: When the system as a whole stops providing the required service to the user

- Rolling upgrade:

- **Throughput**: The amount of work processed by a system or component in a given amount of time. It's a measure of how efficiently a system performs its tasks. Examples:
  - Systems performance: Requests per second (requests/second)
  - Networks: Megabits per second (Mbps)
  - Databases: Queries per second (queries/second)

- **Latency**: Refers to the time delay between the initiation of a request and the beginning of a response. It’s a measure of the delay experienced by a request or action within a system or network.

- **Service time**: The time it takes to process the request (authorization, load balancing, etc.).

- **Response time**: Response time is the total time it takes from the initiation of a request until the entire response is received and processed. It encompasses the latency as well as the service time.

  - It’s common to see the average response time of a service reported. (Strictly speaking, the term “average” doesn’t refer to any particular formula, but in practice it is usually understood as the arithmetic mean: given n values, add up all the values, and divide by n.) However, the mean is not a very good metric if you want to know your “typical” response time, because it doesn’t tell you how many users actually experienced that delay.

  - Usually it is better to use percentiles. If you take your list of response times and sort it from fastest to slowest, then the median is the halfway point: for example, if your median response time is 200 ms, that means half your requests return in less than 200 ms, and half your requests take longer than that.

    - There are algorithms that can calculate a good approximation of percentiles at minimal CPU and memory cost:
      - forward decay
      - t-digest
      - HdrHistogram. 

- Vertical scaling: Systems *'scaling up'* increase their ability to process more requests by improving the hardware of the hosting machine.

- Horizontal scaling: Systems *'scaling out'* increase their ability to process more requests by adding more machines to handle them.

Distributing load across multiple machines is also known as a shared-nothing architecture.

- **SLA (Service Level Agreement)**: Contracts that define the expected performance and availability of a service 

- **Telemetry**: Monitoring things like performance metrics and error rates. Once the rocket leaves the ground, telemetry is important to know what's going on 

- **Load parameters**: request per second, reads to writes ratio, etc.

- **Fan-out**: Read page 29.

- **Elastic Systems**: Those that can scale automatically.


#### Chapter 2 Data Models and Query Languages

- **Relational VS. Document Model**
  - Pros and Cons
    - **SQL Databases**:
      -  Better support for joins, and many-to-one and many-to-many relationships.
      - Splitting a document-like structure into multiple tables can lead to cumbersome schemas and unnecessarily complicated application code.

    - **NoSQL Databases**:
      - Schema flexibility.
      - Better performance due to locality.
      - For some applications it is closer to the data structures used by the application.
      - If your application does use many-to-many relationships, the document model becomes less appealing

  - Data Model
    - **SQL Databases**: 
      - Relational model with tables, rows, and columns.
      - Accessed via SQL queries.
      - Schema is predefined and changes can be complex.
    
    - **NoSQL Databases**:
      - Varied models including document stores, key-value stores, column-family stores, and graph databases.
      - Flexible schema, allowing for adjustments and hierarchical or nested data structures.

  - Schema Flexibility
    - **SQL Databases**:
      - Fixed schema.
      - Schema changes require migrations, which can be time-consuming.
    
    - **NoSQL Databases**:
      - Dynamic schema.
      - Easier to store different fields or structures in records without predefined schema changes.

  - Consistency and Transactions
    - **SQL Databases**:
      - Adhere to ACID (Atomicity, Consistency, Isolation, Durability) properties.
      - Ensure reliable transactions and consistency even in system failures.
    
    - **NoSQL Databases**:
      - May prioritize availability and partition tolerance (CAP theorem) over strict consistency.
      - Often offer eventual consistency instead of strong consistency.
      - Multi-statement transactions might not be as robust.

  - Scalability
    - **SQL Databases**:
      - Typically scale vertically (adding resources to a single server).
      
    - **NoSQL Databases**:
      - Designed to scale out horizontally (distributing data across multiple servers).
      - Can handle large volumes of data and high-velocity workloads more effectively.

  - Query Language
    - **SQL Databases**:
      - Use Structured Query Language (SQL).
      - SQL is powerful for complex queries involving multiple tables.
      
    - **NoSQL Databases**:
      - Query mechanisms vary by database type.
      - Document stores might use JSON-based queries; key-value stores use simple key-based lookups.

  - Use Cases
    - **SQL Databases**:
      - Best for applications needing complex transactions, strong consistency, and well-defined schemas.
      - Examples: financial systems, traditional enterprise applications.
      
    - **NoSQL Databases**:
      - Ideal for scenarios where scalability, flexibility, and high performance are critical.
      - Examples: real-time web applications, big data applications, content management systems.

A document is usually stored as a single continuous string, encoded as JSON, XML, or a binary variant thereof (such as MongoDB’s BSON). If your application often needs to access the entire document (for example, to render it on a web page), there is a performance advantage to this storage locality.

If data is split across multiple tables, like in Figure 2-1, multiple index lookups are required to retrieve it all, which may require more disk seeks and take more time. The locality advantage only applies if you need large parts of the document at the same time.

- **Imperative VS. Declarative Languages**:
  - Imperative Language: Tells the computer to perform certain operations in a certain order, like JS or Python. You tell the code line by line what to do.
  - Declarative Language: You specify the pattern of the data you want, but not how to achieve that goal (like CSS or react).

**MapReduce**
  - Programming model for handling large amounts of data across many machines, popularized by Google.
    - A limited form of MapReduce is supported by some NoSQL datastores, including MongoDB and CouchDB, as a mechanism for performing read-only queries across many documents.
    - MapReduce is neither a declarative query language nor a fully imperative query API, but somewhere in between: the logic of the query is expressed with snippets of code, which are called repeatedly by the processing framework.
    - It is based on the `map` (also known as *collect*) and `reduce` (also known as *fold* or *inject* ) functions that exist in many functional programming languages:
      ```Python
      # Map
      # Applies a given function to all items in an iterable (like a list) and returns an iterator that produces the results
      
      # Define a function to be applied to each element
      def square(x):
          return x * x
      numbers = [1, 2, 3, 4, 5]
      # Apply the function to each item in the list using map
      squared_numbers = map(square, numbers)
      # Convert the map object to a list and print it
      print(list(squared_numbers))  # Output: [1, 4, 9, 16, 25]

      # Reduce
      # Applies a binary function (a function that takes two arguments) cumulatively to the items of an iterable, from left to right, so as to reduce the iterable to a single value.
      from functools import reduce
      # Define a function to be used for reduction
      def add(x, y):
          return x + y
      numbers = [1, 2, 3, 4, 5]
      # Apply the function cumulatively using reduce
      sum_of_numbers = reduce(add, numbers)

      print(sum_of_numbers)  # Output: 15
      ```
  - The `map` and `reduce` functions are somewhat restricted in what they are allowed to do. They must be pure functions, which means they only use the data that is passed to them as input, they cannot perform additional database queries, and they must not have any side effects.

Graph-Like Data Models

In scenarios where **many-to-many relationships** are prevalent in your data, a graph-like data model can be particularly effective. This model consists of the following key components:

- **Vertices** (also known as **nodes** or **entities**):
  - Represent **individual objects** or **entities** in the graph.
  - Each vertex can contain attributes or properties that describe the entity it represents.
  - Examples include people, locations, products, or any distinct objects.

- **Edges** (also known as **relationships** or **arcs**):
  - Represent the **connections** or **relationships** between vertices.
  - Edges can be **directed** or **undirected**:
    - **Directed edges** have a direction, indicating a one-way relationship (e.g., A → B).
    - **Undirected edges** do not have a direction, indicating a mutual relationship (e.g., A ↔ B).
  - Each edge can also have attributes or properties that describe the relationship.

- Key Characteristics

  - **Flexible Schema**:
    - Graph models do not require a rigid schema, allowing the addition of new types of relationships or entities without altering existing data.

  - **Efficient Traversal**:
    - Graph databases are optimized for traversing and querying relationships between vertices, making them suitable for applications requiring complex queries over interconnected data.

  - **Use Cases**:
    - Social networks (e.g., users, friends, and interactions)
    - Recommendation systems (e.g., users and products)
    - Fraud detection (e.g., transactions and accounts)
    - Network and IT infrastructure (e.g., servers, connections, and configurations)

- Examples

  - **Social Network**:
    - **Vertices**: Users
    - **Edges**: Friendships, messages, posts

  - **Recommendation System**:
    - **Vertices**: Users, Products
    - **Edges**: Purchases, ratings, reviews

Triple Stores and SPARQL

- **Triple Stores**

  Triple Stores are a type of graph database designed to store and manage **RDF (Resource Description Framework)** data, which is represented as triples. Each triple consists of:
  - **Subject**: The entity being described.
  - **Predicate**: The property or relationship.
  - **Object**: The value or another entity related to the subject.

  Triple stores are particularly suited for applications that require the management of semantic data and ontologies.

  **Examples of Triple Stores**:
  - Apache Jena
  - RDF4J
  - Virtuoso

- **SPARQL**

  **SPARQL** (SPARQL Protocol and RDF Query Language) is a query language specifically designed for querying RDF data. It allows users to perform complex queries to retrieve and manipulate data stored in triple stores.

  **Basic SPARQL Query Structure**:
  - **SELECT**: Specifies the variables to return.
  - **WHERE**: Contains the pattern to match in the data.
  - **FILTER**: (Optional) Refines the results based on conditions.

  - **Example Query**:
    ```sparql
      PREFIX ex: <http://example.org/>

      SELECT ?person ?email
      WHERE {
        ?person ex:hasEmail ?email .
        FILTER (CONTAINS(?email, "@example.com"))
      }
    ```


- **Normalization**: Apparently, in DBs normalization means to store the data in such a way that it is [unique] not duplicated. Like in LinkedIn  your profile has a city or location, the db tables have a table for your user (id, name, last_name, city_id)  and a table for cities (id, city_name, etc.) making it so that if you update the city name in the cities table, all users will have their city updated.

- **Schema-on-read**: XML DBs don't have concrete schemas like relational DBs. That doesn't mean they don't have a structure (it's implicit since the app ensures the data is valid and has a certain structure) but the DB itself doesn't. Hence schema-on-read instead of the incorrect "schema-less".

- **Heterogeneous data**: data that is not following the same structure across all records. Like chocolate chip cookies, they're not exactly the same, they have different shapes and sizes.

- **Homogeneous data**: Data that has the same  structure (following a pattern, it doesn't mean it's all exactly the same info) across all records.

- **Declarative language**: You tell the outcome you want

- **Imperative language**: You specify the steps to achieve the outcome you want





#### Chapter 3: Storage and Retrieval

- **Log**: An append-only sequence of records. Many databases internally use a log, which is an append-only data file.
  - Application Logs: These are the types of logs you know, the file that has all the records of what's going on in an application.
  - DB Log: Some DBs use an internal append-only log to keep track of its records.
    - NOTE: Remember the example of the world's simplest DB where it uses bash commands to append data in a hasmpap way and searches for the most recent occurence of the key. This way you'll immediatly remember what a log is in this context:

      ```Bash
      db_set() {
        echo "$1, $2" >> database
      }
      db_get() {
        grep "^$1," database | sed -e 's/^$1,//" | tail -n 1
      } 
      ```

- **Index**: An additional structure that is derived from the primary data. It allows you to search records faster in the DB with the downside of slowing down writes.

  - **Hash Indexes**: Let’s say our data storage consists only of appending to a file, as in the preceding example. Then the simplest possible indexing strategy is this: keep an in-memory hash map where every key is mapped to a byte offset in the data file—the location at which the value can be found.
    - Think of the leetcode problem 'Encode and decode a string' and you'll get it.
  
  - **SSTables and LSM-Trees**

    - *Sorted String Tables* are similar as the log files (append only files) used in the *Hash Indexes* example with just one extra detail: the format of the segment files require that the sequence of key-value pairs is sorted by key and each key only appears once within each merged segment file (the compaction process already ensures that).

      - Merging segments is simple and efficient, even if the files are bigger than the available memory. The approach is like the one used in the mergesort algorithm.

      - In order to find a particular key in the file, you no longer need to keep an index of all the keys in memory. You still need an in-memory index to tell you the offsets for some of the keys, but it can be sparse: one key for every few kilobytes of segment file is sufficient, because a few kilobytes can be scanned very quickly. 
        - Remember the book's example: You need a key between to keys that are in the in-memory index, so you just use the first key's offset and search from there.

      - Since read requests need to scan over several key-value pairs in the requested range anyway, it is possible to group those records into a block and compress it before writing it to disk.
    
    - *Log-Structured Merge-Tree*: Storage engines that are based on this principle of merging and compacting sorted files are often called LSM storage engines.

    - **strategies to determine the order and timing of how SSTables are compacted and merged.**

      - Size-tiered compaction: In size-tiered compaction, newer and smaller SSTables are successively merged into older and larger SSTables.
        - Cassandra
        -  HBase
      
      - Leveled compaction: In leveled compaction, the key range is split up into smaller SSTables and older data is moved into separate “levels,” which allows the compaction to proceed more incrementally and use less disk space.
        - LevelDB
        - RocksDB
        - Cassandra

    - Since data is stored in sorted order, you can efficiently perform range queries (scanning all keys above some minimum and up to some maximum), and because the disk writes are sequential the LSM-tree can support remarkably high write throughput.
  
  - **B-Trees**
    - Like SSTables, B-trees keep key-value pairs sorted by key, which allows efficient key-value lookups and range queries. But that’s where the similarity ends: B-trees have a very different design philosophy.
    


<iframe width="320" height="180" src="https://www.youtube.com/watch?v=BIlFTFrEFOI&t=64s" title="SQL Hash Indexes" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="1"></iframe>

- **Memtable**: An in-memory balanced tree data structure (for example, a red-black tree)

- **Bloom filter**: is a memory-efficient data structure for approximating the contents of a set. It can tell you if a key does not appear in the database, and thus saves many unnecessary disk reads for nonexistent keys.

- **Compaction**: Compaction means throwing away duplicate keys in the log, and keeping only the most recent update for each key (very useful to avoid running out of space).

  - Each segment now has its own in-memory hash table, mapping keys to file offsets. In order to find the value for a key, we first check the most recent segment’s hash map; if the key is not present we check the second-most- recent segment, and so on. 
  
  - **Tombstone**: If you want to delete a key and its associated value, you have to append a special deletion record to the data file (sometimes called a tombstone). When log segments are merged, the tombstone tells the merging process to discard any previous values for the deleted key.

- **Storage engines**:
  - Log-structured:
  - Page-oriented:













<details>
  <summary><h4 style="display: inline;">Functional vs Non-Functional Requirements</h4></summary><br>

| Functional Requirements                                                                                       | Non-Functional Requirements                                                                                             |
|---------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| A functional requirement defines a system or its component.                                                   | A non-functional requirement defines the quality attribute of a software system.                                        |
| It specifies “What should the software system do?”                                                            | It places constraints on “How should the software system fulfill the functional requirements?”                          |
| Functional requirement is specified by User.                                                                  | Non-functional requirement is specified by technical peoples e.g. Architect, Technical leaders and software developers. |
| It is mandatory.                                                                                              | It is not mandatory.                                                                                                    |
| It is captured in use case.                                                                                   | It is captured as a quality attribute.                                                                                  |
| Defined at a component level.                                                                                 | Applied to a system as a whole.                                                                                         |
| Helps you verify the functionality of the software.                                                           | Helps you to verify the performance of the software.                                                                    |
| Functional Testing like System, Integration, End to End, API testing, etc are done.                           | Non-Functional Testing like Performance, Stress, Usability, Security testing, etc are done.                             |
| Usually easy to define.                                                                                       | Usually more difficult to define.                                                                                       |
| **Example**                                                                                                   | **Example**                                                                                                             |
| 1) Authentication of user whenever he/she logs into the system.                                               | 1) Emails should be sent with a latency of no greater than 12 hours from such an activity.                              |
| 2) System shutdown in case of a cyber attack.                                                                 | 2) The processing of each request should be done within 10 seconds                                                      |
| 3) A Verification email is sent to user whenever he/she registers for the first time on some software system. | 3) The site should load in 3 seconds when the number of simultaneous users are > 10000                                  |

</details>

### Napkin Math

- **1 Byte** = **8 bits** 
- **1 IPV4** Addresss = **4 Bytes**
- **1 IPV6** Address = **16 Bytes**
- **1 Unix Timestamp** = **4 Bytes**
- SSD: Solid State Drive

<details>
  <summary><h5 style="display: inline;">Latency Numbers Every Programmer Should Know</h5></summary><br>

[Latency Numbers Every Programmer Should Know](https://colin-scott.github.io/personal_website/research/interactive_latency.html)

This website is really useful so you can get an idea (it's a little outdated, 2020) of the latency (how much time it takes an operation to perform) when working with data.

![LatencyNumbers](../images/LatencyNumbers.jpg)

</details>

#### Concepts I Found Interesting

<details>
  <summary><h5 style="display: inline;">CPU Cache Mutex Lock/Unlock</h5></summary><br>

In the context of CPU cache, mutex lock and unlock operations typically refer to synchronization mechanisms used in multi-threaded programming to control access to shared resources.

1. Mutex Lock:

- When a thread wants to access a shared resource (such as a region of memory or a data structure) that is cached in CPU cache, it first acquires a mutex lock associated with that resource.
- Acquiring a mutex lock ensures that only one thread can access the shared resource at a time. If the resource is already locked by another thread, the thread attempting to lock it will wait until the lock is released.

2. Mutex Unlock:

- Once a thread has finished using the shared resource, it releases the mutex lock by invoking the unlock operation.
- Releasing the mutex lock allows other threads to acquire the lock and access the shared resource.
- Mutex locks and unlocks help prevent race conditions and ensure that concurrent access to shared resources is properly coordinated, thereby avoiding data corruption and inconsistency.

In the context of CPU cache, when a thread acquires a mutex lock before accessing a shared resource that resides in the cache, it ensures that only one thread can access that resource at a time, even if multiple threads are running concurrently on different CPU cores. This helps maintain data integrity and consistency in multi-threaded applications.

</details>

### Software Technologies You Should Know

<details>
  <summary><h4 style="display: inline;">Redis</h4></summary><br>

![Redis](../images/Redis.jpg)

Redis, **RE**mote **DI**ctionary **S**erver, is an open-source, in-memory data structure store used as a database, cache, and message broker. It supports various data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs, geospatial indexes, and streams. Redis is known for its high performance, flexibility, and rich set of features.

##### Key Features:

- **In-Memory Storage**: Redis primarily stores data in RAM, which allows for extremely fast data access and retrieval.
- **Data Structures**: It supports various data structures, enabling users to store and manipulate data efficiently.
- **Persistence**: Redis offers different persistence options to ensure data durability, including snapshotting and append-only file (AOF) persistence.
- **Replication and High Availability**: Redis supports replication and clustering, allowing for data redundancy and high availability.
- **Pub/Sub Messaging**: Redis can be used as a message broker through its publish/subscribe functionality.
- **Lua Scripting**: Users can extend Redis functionality using Lua scripting.
- **Transactions**: Redis supports transactions, allowing users to execute a group of commands as a single atomic operation.

##### Alternatives:

1. **Memcached**: Memcached is a distributed memory caching system that also stores key-value pairs. It is known for its simplicity and high-performance caching capabilities.

4. **Amazon DynamoDB**: DynamoDB is a fully managed NoSQL database service provided by Amazon Web Services (AWS). It offers seamless scalability, high performance, and built-in security features.

</details>

<details>
  <summary><h4 style="display: inline;">Elastic Search</h4></summary><br>

![Redis](../images/Redis.jpg)

</details>











### Designing Systems & Components
<details>
  <summary><h4 style="display: inline;">Rate Limiter</h4></summary><br>

##### Requirements

1. Take 1 Billion (1x10^9 or 1,000,000,000) users.
2. Must be as general use as possible (multiple services use it).

Components you ended up using:
- Reddis: Sorted sets 
- Memcache
- Consistent Hashing

##### Algorithms

###### Fixed Window Algorithm for Rate limiters

We set a fix window of time, lets say every minute a user can send 100 requests, so everytime a new minute encompasses we refresh his available requests total to 100.

- Benefit: Since we're storing counts inside of the key value store in our memory, this is a very simplistic approach to take. We don't have to take into account when the requests were made exactly, we just care that they happened in the window -> we would just need to include the minute when checking for the availability.

- Issue with refresh rate of the algorithm: With a requests/per minute of a 100; if the user sends a request at 0:59 and then at 1:00 the valid window refreshes, the user could send another 100 requests at 1:01: in total 200 requests in a matter of 2 seconds

###### Sliding window

Any time a user makes a request we check if it is inside the invalid window, every second we shift this valid window by one second so the user can't take advantage of the refresh rate of the fixed window Algo.

- Benefit: Here we're checking if the user has expired his total amout of requests in the previous 60 seconds so we don't have the same refresh rate issue as the Fixed widow.

- Downside: We have to store the exact time-stamp when the user attempted to perform his requests. This increases our memory requirements since one Unix timestamp per request per user:

$4 \text{ Bytes} \times \text{Max\_No.Of\_Requests} \times \text{No\_Of\_Users} -> 4 * 100 * 1000000000 = 400GB$ 

##### Other Algorithms

- Token bucket
- Sliding Window Counter (Balance between Fixed Window and Sliding Window Algorithms)

##### Data Schemas

**Identify User and his count**
key -> Value
User_Id/Ip -> Count (Enforces count using rule)
*Redis can set data to expire

**Identify rule (youtube rate limiter rules may be different than gmail's)**

**Rule DB Schema**
| Parameeter | Type |
|----------|----------|
| Id   | String   |
| API To forward the request to   | Cell 4   |
| Operation/Endpoint   | String   |
| TimeUnit   | String   |
| Request   | Int   |

</details>
