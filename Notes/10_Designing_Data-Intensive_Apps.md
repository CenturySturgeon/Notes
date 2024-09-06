## Chapter 1: Reliable, Scalable, and Maintainable Applications

### Availability

Percentage of time a system or service is operational and accessible when needed. It measures how often the system is up compared to the total time it should be available.

- **Downtime Based on Availability**:
  | Availability | Downtime           |
  |--------------|--------------------|
  | 99%          | 3.65 days/year     |
  | 99.9%        | 8.77 hours/year    |
  | 99.99%       | 52.6 minutes/year  |
  | 99.999%      | 5.26 minutes/year  |
  | 100%         | 0 seconds/year     |

  Each additional nine decreases the downtime by an order of magnitude of roughly 10 times.

### Reliability

Measures how consistently and correctly a system performs its intended functions over time without failure.

- **Measurement**:
  - Often assessed using metrics such as Mean Time Between Failures (MTBF) or Mean Time to Failure (MTTF), which quantify how long the system performs correctly before encountering a failure.

### Redundancy

The inclusion of extra components or systems to ensure continued operation in the event of a failure.

- Redundancy Types
    | Type                      | Description                                                                                                                           |
    |---------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
    | **Hardware Redundancy**   | Spare hardware components (e.g., additional servers, power supplies, or network links) that can take over if primary components fail. |
    | **Data Redundancy**       | Replicating data across multiple storage devices or locations to protect against data loss.                                           |
    | **Geographic Redundancy** | Distributing resources across different locations or data centers to protect against site-specific failures.                          |



### Maintainability

Ensuring that various people (engineering and operations) can work on the system productively over time.

| **Factors**      | **Description**                                                         |
|------------------|-------------------------------------------------------------------------|
| **Operability**  | Make it easy for operations teams to keep the system running smoothly.  |
| **Simplicity**   | Make it easy for new engineers to understand the system.                |
| **Evolvability** | Make it easy for engineers to make changes to the system in the future. |


### Fault and Failure

- **Fault**: A deviation of one component from its specification.
- **Failure**: When the system as a whole stops providing the required service to the user.

### Rolling Upgrade

A method of upgrading a system without shutting it down or interrupting its operation.

### Throughput

The amount of work processed by a system or component in a given amount of time.

- Examples:
  - **Systems Performance**: Requests per second (requests/second)
  - **Networks**: Megabits per second (Mbps)
  - **Databases**: Queries per second (queries/second)

### Latency

The time delay between the initiation of a request and the beginning of a response.

### Service Time

The time it takes to process a request, including tasks like authorization and load balancing.

### Response Time

The total time from the initiation of a request until the entire response is received and processed. It encompasses both latency and service time.

- **Metrics**:
  - **Average Response Time**: Often reported as the arithmetic mean, but may not reflect the typical user experience.
  - **Percentiles**: Provide a better understanding of response times, with the median being the halfway point. Percentile algorithms include:
    - Forward Decay
    - T-Digest
    - HDRHistogram

### Scaling

- **Vertical Scaling**: *Scaling up* by improving the hardware of the hosting machine.
- **Horizontal Scaling**: *Scaling out* by adding more machines to handle increased load. Known as a shared-nothing architecture.

### SLA (Service Level Agreement)

Contracts that define the expected performance and availability of a service.

### Telemetry

Monitoring performance metrics and error rates. Essential for understanding system status after deployment.

### Load Parameters

- Examples: 
    - Requests per second.
    - Reads-to-writes ratio.

### Fan-out

- **Note**: Refer to page 29 for detailed information.

### Elastic Systems

Systems that can scale automatically.


## Chapter 2: Data Models and Query Languages

### Relational vs. Document Model

- **Pros and Cons**

  - **SQL Databases**:
    - Pros:
      - Better support for joins, and many-to-one and many-to-many relationships.
      - Reliable for complex transactions and strong consistency.
    - Cons:
      - Splitting a document-like structure into multiple tables can lead to cumbersome schemas and complex application code.

  - **NoSQL Databases**:
    - Pros:
      - Schema flexibility.
      - Better performance due to locality.
      - For some applications, closer to the data structures used by the application.
    - Cons:
      - Document model can become less appealing for applications with many-to-many relationships.

### Data Model

- **SQL Databases**:
  - Relational model with tables, rows, and columns.
  - Accessed via SQL queries.
  - Schema is predefined and changes can be complex.

- **NoSQL Databases**:
  - Varied models including document stores, key-value stores, column-family stores, and graph databases.
  - Flexible schema, allowing for adjustments and hierarchical or nested data structures.

### Schema Flexibility

- **SQL Databases**:
  - Fixed schema.
  - Schema changes require migrations, which can be time-consuming.

- **NoSQL Databases**:
  - Dynamic schema.
  - Easier to store different fields or structures in records without predefined schema changes.

### Consistency and Transactions

- **SQL Databases**:
  - Adhere to ACID (Atomicity, Consistency, Isolation, Durability) properties.
  - Ensure reliable transactions and consistency even in system failures.

- **NoSQL Databases**:
  - May prioritize availability and partition tolerance (CAP theorem) over strict consistency.
  - Often offer eventual consistency instead of strong consistency.
  - Multi-statement transactions might not be as robust.

### Scalability

- **SQL Databases**:
  - Typically scale vertically (adding resources to a single server).

- **NoSQL Databases**:
  - Designed to scale out horizontally (distributing data across multiple servers).
  - Can handle large volumes of data and high-velocity workloads more effectively.

### Query Language

- **SQL Databases**:
  - Use Structured Query Language (SQL).
  - SQL is powerful for complex queries involving multiple tables.

- **NoSQL Databases**:
  - Query mechanisms vary by database type.
  - Document stores might use JSON-based queries; key-value stores use simple key-based lookups.

### Use Cases

- **SQL Databases**:
  - Best for applications needing complex transactions, strong consistency, and well-defined schemas.
  - Examples: Financial systems, traditional enterprise applications.

- **NoSQL Databases**:
  - Ideal for scenarios where scalability, flexibility, and high performance are critical.
  - Examples: Real-time web applications, big data applications, content management systems.

### Document Storage

A document is usually stored as a single continuous string, encoded as JSON, XML, or a binary variant (e.g., MongoDB’s BSON). If your application often needs to access the entire document (e.g., to render it on a web page), there is a performance advantage due to this storage locality.

If data is split across multiple tables, as shown in Figure 2-1, multiple index lookups are required to retrieve it all. This can result in more disk seeks and longer retrieval times. The locality advantage is significant if large parts of the document are needed simultaneously.

### Imperative vs. Declarative Languages

- **Imperative Language**:
  - Specifies the exact operations in a particular order (e.g., JavaScript, Python).
  - Example: Line-by-line instructions on what to do.

- **Declarative Language**:
  - Specifies what the result should be, without detailing how to achieve it (e.g., CSS, React).

### MapReduce

- **Overview**:
  - A programming model for handling large amounts of data across many machines, popularized by Google.
  - A limited form of MapReduce is supported by some NoSQL datastores, including MongoDB and CouchDB, for read-only queries across many documents.
  - Combines `map` and `reduce` functions from functional programming languages.

- **Map Function**:
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

### Graph-Like Data Models

In scenarios where **many-to-many relationships** are prevalent, a graph-like data model can be particularly effective. This model consists of the following key components:

- **Vertices** (also known as **nodes** or **entities**):
  - Represent **individual objects** or **entities** in the graph.
  - Each vertex can contain attributes or properties that describe the entity it represents.
  - Examples: People, locations, products, or any distinct objects.

- **Edges** (also known as **relationships** or **arcs**):
  - Represent the **connections** or **relationships** between vertices.
  - Edges can be **directed** or **undirected**:
    - **Directed edges** have a direction, indicating a one-way relationship (e.g., A → B).
    - **Undirected edges** do not have a direction, indicating a mutual relationship (e.g., A ↔ B).
  - Each edge can also have attributes or properties that describe the relationship.

#### Key Characteristics

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

#### Triple Stores and SPARQL

- **Triple Stores**:
  - Triple Stores are a type of graph database designed to store and manage **RDF (Resource Description Framework)** data, represented as triples. Each triple consists of:
    - **Subject**: The entity being described.
    - **Predicate**: The property or relationship.
    - **Object**: The value or another entity related to the subject.
  - Triple stores are particularly suited for managing semantic data and ontologies.
  
  - **Examples of Triple Stores**:
    - Apache Jena
    - RDF4J
    - Virtuoso

- **SPARQL**:
  - **SPARQL** (SPARQL Protocol and RDF Query Language) is a query language specifically designed for querying RDF data. It allows users to perform complex queries to retrieve and manipulate data stored in triple stores.
  
  - **Basic SPARQL Query Structure**:
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

#### Additional Concepts

- **Normalization**:
  - In databases, normalization means to store the data in such a way that it is **unique** and not duplicated. For example, in LinkedIn, your profile has a city or location, but the database has separate tables for users and cities. If you update the city name in the cities table, all users with that city will have their data updated.

- **Schema-on-Read**:
  - XML databases don't have concrete schemas like relational databases. This doesn't mean they lack structure; the structure is implicit, as the application ensures data validity. Hence, "schema-on-read" is a more accurate term than "schema-less."

- **Heterogeneous Data**:
  - Data that does not follow the same structure across all records. Example: Chocolate chip cookies vary in shape and size.

- **Homogeneous Data**:
  - Data that follows the same structure or pattern across all records. It does not mean all records have identical information, but they adhere to a consistent format.

- **Declarative Language**:
  - Specifies what outcome you want without detailing the steps to achieve it.

- **Imperative Language**:
  - Specifies the exact steps needed to achieve the desired outcome.



## Chapter 3: Storage and Retrieval

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

  - B-trees break the database down into fixed-size blocks or pages, traditionally 4 KB in size (sometimes bigger), and read or write one page at a time. 

  - **Pages**: Each page can be identified using an address or location, which allows one page to refer to another—similar to a pointer, but on disk instead of in memory. We can use these page references to construct a tree of pages.

    - A *leaf page* is a page that no longer stores  references, but the values of the keys in its range.

    - **Branching factor**: The number of references to child pages in one page of the B-tree. It depends on the amount of space required to store the page references and the range boundaries, but typically it is several hundred.

    - If there isn’t enough free space in the leaf page to accommodate a new key-value, it is split into two half-full pages, and the parent page is updated to account for the new subdivision of key ranges.

  - **NOTE**: a B-tree with n keys always has a depth of O(log n). Most databases can fit into a B-tree that is three or four levels deep, so you don’t need to follow many page references to find the page you are looking for. (A four-level tree of 4 KB pages with a branching factor of 500 can store up to 256 TB.)

  - In order to make the database resilient to crashes, it is common for B-tree implementations to include an additional data structure on disk: a *write-ahead log* (also known as a redo log). 
    - **WAL**: *Write-ahead log*, An append-only file to which every B-tree modification must be written before it can be applied to the pages of the tree itself. When the database comes back up after a crash, this log is used to restore the B-tree back to a consistent state.

  - An additional complication of updating pages in place is that careful concurrency control is required if multiple threads are going to access the B-tree at the same time.
    - This is typically done by protecting the tree’s data structures with *latches* (lightweight locks).

  - **B-Tree Optimizations**
    - Instead of overwriting pages and maintaining a WAL for crash recovery, some databases (like LMDB) use a copy-on-write scheme.
    
    - We can save space in pages by not storing the entire key, but abbreviating it. Especially in pages on the interior of the tree, keys only need to provide enough information to act as boundaries between key ranges. Packing more keys into a page allows the tree to have a higher branching factor, and thus fewer levels.

    - In general, pages can be positioned anywhere on disk; there is nothing requiring pages with nearby key ranges to be nearby on disk.
      - Many B-tree implementations therefore try to lay out the tree so that leaf pages appear in sequential order on disk. However, it’s difficult to maintain that order as the tree grows.

    - Additional pointers have been added to the tree. For example, each leaf page may have references to its sibling pages to the left and right.

  - **B-Tree and LSM-Tree Comparisson**

    - As a rule of thumb:
      - LSM-trees are typically faster for writes.
      - B-trees are thought to be faster for reads.
      - Reads are typically slower on LSM-trees because they have to check several different data structures and SSTables at different stages of compaction (benchmarks are often inconclusive, read *'Comparing B-Trees and LSM-Trees'*).

    - **LSM-Tree Advantages**

      - A B-tree index must write every piece of data at least twice: once to the WAL, and once to the tree page itself.
      
      - Log-structured indexes also rewrite data multiple times due to repeated compaction and merging of SSTables. This effect—one write to the database resulting in multiple writes to the disk over the course of the database’s lifetime—is known as **write amplification**. 
        
        - It is of particular concern on SSDs, which can only overwrite blocks a limited number of times before wearing out.
      
      - In write-heavy applications, the performance bottleneck might be the rate at which the database can write to disk. In this case, *write amplification* has a direct performance cost:
        - The more that a storage engine writes to disk, the fewer writes per second it can handle within the available disk bandwidth. 
      
      - LSM-trees are typically able to sustain higher write throughput than B-trees, partly because they sometimes have lower write amplification, and partly because they sequentially write compact SSTable files rather than having to overwrite several pages in the tree.
        - This difference is particularly important on magnetic hard drives, where sequential writes are much faster than random writes.

      - LSM-trees can be compressed better, and thus often produce smaller files on disk than B-trees. 
        - B-tree storage engines leave some disk space unused due to fragmentation.

        - Since LSM-trees are not page-oriented and periodically rewrite SSTables to remove fragmentation, they have lower storage overheads, especially when using *leveled compaction*.
  
  - **Downsides of LSM-trees**

    - The compaction process can sometimes interfere with the performance of ongoing reads and writes.
      - B-trees can be more predictable as their writing overheads can be predicted (LSM-trees have scenarios where their operations have to wait while the disk completes a heavy operation).

    - On high write throughput, the disk’s finite write bandwidth needs to be shared between the initial write (logging and flushing a memtable to disk) and the compaction threads running in the background.

      - When writing to an empty database, the full disk bandwidth can be used for the initial write, but the bigger the database gets, the more disk bandwidth is required for compaction.

      - If write throughput is high and compaction is not configured carefully, it can happen that compaction cannot keep up with the rate of incoming writes.
        - The number of unmerged segments on disk keeps growing until you run out of disk space -> reads slow down as well.
    
    - An advantage of B-trees is that each key exists in exactly one place in the index, whereas a log-structured storage engine may have multiple copies of the same key in different segments.

  - There is no quick and easy rule for determining which type of storage engine is better for your use case, so it is worth testing empirically.

- **Other Indexing Structures**
  - So far we have only discussed key-value indexes, which are like a primary key index in the relational model. 
  
  - It is also very common to have secondary indexes. In relational databases, you can create several secondary indexes on the same table using the `CREATE INDEX` command.

  - Both B-trees and log-structured indexes can be used as secondary indexes.

- **Storing values within the index**
  - The key in an index is the thing that queries search for, but the value can be one of two things: it could be the actual row  in question, or it could be a reference to the row stored elsewhere.
    - The place where rows are stored is known as a __*heap file*__, and it stores data in no particular order.
  
  - The heap file approach is common because it avoids duplicating data when multiple secondary indexes are present.
    - Each index just references a location in the heap file, and the actual data is kept in one place.
  
  - When updating a value without changing the key, the heap file approach allows the record to be overwritten in place (if the new value isn't larger than the old one).

  - If the new value is larger, as it probably needs to be moved to a new location in the heap where there is enough space. 
    - Either all indexes need to be updated to point at the new heap location of the record, or a forwarding pointer is left behind in the old heap location.

    - In some situations, the extra hop from the index to the heap file is too much of a performance penalty for reads, so it can be desirable to store the indexed row directly within an index. 
      - This is known as a __*clustered index*__.

  - A compromise between a __*clustered index*__ (storing all row data within the index) and a __*nonclustered index*__ (storing only references to the data within the index) is known as a __*covering index*__ or __*index with included columns*__, which stores some of a table’s columns within the index. 
    - This allows some queries to be answered by using the index alone (in which case, the index is said to cover the query).
    - As with any kind of duplication of data, clustered and covering indexes can speed up reads, but they require additional storage and can add overhead on writes.

- **Multi-Column Indexes**
  - The indexes discussed so far only map a single key to a value.
    - That is *not sufficient* if we need to query multiple columns of a table (or multiple fields in a document) simultaneously.

  - The most common type of multi-column index is the __*concatenated index*__: combines several fields into one key by appending one column to another (the index definition specifies in which order the fields are concatenated).

    - This is like an old-fashioned paper phone book, which provides an index from (lastname, firstname) to phone number. 
      
      - Can be used to find all the people with a particular last name, or all the people with a particular lastname-firstname combination.
      
      - However, the index is useless if you want to find all the people with a particular first name.

  - Multi-dimensional indexes are a more general way of querying several columns at once, which is particularly important for geospatial data.

    - An interesting idea is that multi-dimensional indexes are not just for geographic locations. 

      - For example, on an ecommerce website you could use a three-dimensional index on the dimensions (red, green, blue) to search for products in a certain range of colors. 

      - In a database of weather observations you could have a two-dimensional index on (date, temperature) in order to efficiently search for all the observations during the year 2013 where the temperature was between 25 and 30°C. 

- **Full-text search and fuzzy indexes**

  - Previously discussed indexes don’t allow you to do is search for similar keys, such as misspelled words.
    - This is called __*fuzzy querying*__ and it requires different techniques.

    - Lucene is able to search text for words within a certain edit distance (an __*edit distance*__ of 1 means that one letter has been added, removed, or replaced).

    - Lucene uses a SSTable-like structure for its term dictionary. This structure requires a small in-memory index that tells queries at which offset in the sorted file they need to look for a key.

    - In Lucene, the in-memory index is a finite state automaton over the characters in the keys, similar to a trie.
      - This automaton can be transformed into a Levenshtein automaton, which supports efficient search for words within a given edit distance.

- **Keeping everything in memory**

  - Compared to main memory, disks are awkward to deal with. 
    - We tolerate this because disks have two significant advantages: 
      - They are durable (their contents are not lost if the power is turned off).
      - They have a lower cost per gigabyte than RAM.

  - As RAM becomes cheaper, the cost-per-gigabyte argument is eroded. Many datasets are simply not that big, so it’s quite feasible to keep them entirely in memory, potentially distributed across several machines. This has led to the development of __*in-memory*__ databases.
    - Memcached
    - Redis

  - Some in-memory key-value stores, such as Memcached, are intended for caching use only, where it’s acceptable for data to be lost if a machine is restarted.

  - Other in-memory databases aim for durability, which can be achieved with special hardware (such as battery-powered RAM), by writing a log of changes to disk, by writing periodic snapshots to disk, or by replicating the in-memory state to other machines.

  - When an in-memory database is restarted, it needs to reload its state, either from disk or over the network from a __*replica*__.
    - The disk is merely used as an append-only log for durability, and reads are served entirely from memory.

  - In-memoery DBs can be faster because they can avoid the overheads of encoding in-memory data structures in a form that can be written to disk.

  - __*Anti-caching*__ approach: works by evicting the least recently used data from memory to disk when there is not enough memory, and loading it back into memory when it is accessed again in the future.

**Transaction Processing or Analytics?**

  - **Transaction**: A group of reads and writes that form a logical unit.
    - A transaction needn’t necessarily have ACID properties. Transaction processing just means allowing clients to make low- latency reads and writes—as opposed to batch processing jobs, which only run periodically (for example, once per day).

  - **OLTP**: __*Online Transaction Processing*__ is an access pattern designed to handle a high volume of short online transaction requests, such as inserting, updating, and querying data. 
  
    - Focuses on:
      - Fast query processing.
      - Maintaining data integrity in multi-user environments.
      - Commonly used in applications like retail sales and banking.

  - **OLAP**: __*Online Analytics Processing*__ is an access pattern optimized for querying and analyzing large volumes of data. 
  
    - Supports complex queries and multidimensional analysis.
    - Often used for business intelligence, reporting, and data mining.

  - **OLTP VS. OLAP**
    | Property                 | Transaction Processing Systems (OLTP)             | Analytic Systems (OLAP)                   |
    |--------------------------|---------------------------------------------------|-------------------------------------------|
    | **Main read pattern**    | Small number of records per query, fetched by key | Aggregate over large number of records    |
    | **Main write pattern**   | Random-access, low-latency writes from user input | Bulk import (ETL) or event stream         |
    | **Primarily used by**    | End user/customer, via web application            | Internal analyst, for decision support    |
    | **What data represents** | Latest state of data (current point in time)      | History of events that happened over time |
    | **Dataset size**         | Gigabytes to terabytes                            | Terabytes to petabytes                    |
  
    - In the late 1980s and early 1990s, there was a trend for companies to stop using their OLTP systems for analytics purposes, and to run the analytics on a separate database instead. This separate database was called a __*data warehouse*__.

- **Data Warehousing**

  - A __*data warehouse*__, by contrast, is a separate database that analysts can query to their hearts’ content, without affecting OLTP operations.
    - Remember DB admins consider themselves guardians of the DB and don't want anyone messing with them.
    - The data warehouse contains a read-only copy of all the data from in all the various OLTP systems in the company.
    - **ETL**: __*Extract–Transform–Load*__ is a process where data is extracted from OLTP DBs using either a periodic data dump or a continuous stream of update, it then:
      - Transforms into an analysis-friendly schema.
      - Cleans it up.
      - Loads it into the data warehouse.

- **The divergence between OLTP databases and data warehouses**

- **Stars and Snowflakes: Schemas for Analytics**

- **Column-Oriented Storage**

  - The idea behind column-oriented storage is simple: don’t store all the values from one row together, but store all the values from each column together instead.

  - **Column Compression**
    - **Note**: Cassandra and HBase have a concept of column families, which they inherited from Bigtable. However, it is very misleading to call them column-oriented: within each column family, they store all columns from a row together, along with a row key, and they do not use column compression. Thus, the Bigtable model is still mostly row- oriented.

  - **Memory bandwidth and vectorized processing**
    - Besides reducing the volume of data that needs to be loaded from disk, column-oriented storage layouts are also good for making efficient use of CPU cycles. For example, the query engine can take a chunk of compressed column data that fits comfortably in the CPU’s L1 cache and iterate through it in a tight loop (that is, with no function calls). A CPU can execute such a loop much faster than code that requires a lot of function calls and conditions for each record that is processed. Column compression allows more rows from a column to fit in the same amount of L1 cache. Operators, such as the bitwise AND and OR described previously, can be designed to operate on such chunks of compressed column data directly. This technique is known as __*vectorized processing*__.

  - **Writing to Column-Oriented Storage**
    - Fortunately, we have already seen a good solution earlier in this chapter: LSM-trees. All writes first go to an in-memory store, where they are added to a sorted structure and prepared for writing to disk. It doesn’t matter whether the in-memory store is row-oriented or column-oriented. When enough writes have accumulated, they are merged with the column files on disk and written to new files in bulk. This is essentially what Vertica does.
  
  - **Aggregation: Data Cubes and Materialized Views**

    - **REDUCE THE NEXT ROWS:**

    - Another aspect of data warehouses that is worth mentioning briefly is materialized aggregates. As discussed earlier, data warehouse queries often involve an aggregate function, such as , , , , or in SQL. If the same aggregates are used by many different queries, it can be wasteful to crunch through the raw data every time. Why not cache some of the counts or sums that queries use most often?
    
    - One way of creating such a cache is a materialized view. In a relational data model, it is often defined like a standard (virtual) view: a table-like object whose contents are the results of some query. The difference is that a materialized view is an actual copy of the query results, written to disk, whereas a virtual view is just a shortcut for writing queries. When you read from a virtual view, the SQL engine expands it into the view’s underlying query on the fly and then processes the expanded query.

    - When the underlying data changes, a materialized view needs to be updated, because it is a denormalized copy of the data. The database can do that automatically, but such updates make writes more expensive, which is why materialized views are not often used in OLTP databases. In read- heavy data warehouses they can make more sense (whether or not they actually improve read performance depends on the individual case).

<iframe width="320" height="180" src="https://www.youtube.com/watch?v=BIlFTFrEFOI&t=64s" title="SQL Hash Indexes" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="1"></iframe>

- **Memtable**: An in-memory balanced tree data structure (for example, a red-black tree)

- **Bloom filter**: A memory-efficient data structure for approximating the contents of a set. It can tell you if a key does not appear in the database, and thus saves many unnecessary disk reads for nonexistent keys.

- **Compaction**: Compaction means throwing away duplicate keys in the log, and keeping only the most recent update for each key (very useful to avoid running out of space).

  - Each segment now has its own in-memory hash table, mapping keys to file offsets. In order to find the value for a key, we first check the most recent segment’s hash map; if the key is not present we check the second-most- recent segment, and so on. 
  
  - **Tombstone**: If you want to delete a key and its associated value, you have to append a special deletion record to the data file (sometimes called a tombstone). When log segments are merged, the tombstone tells the merging process to discard any previous values for the deleted key.

- **Storage engines**:
  - Log-structured:
  - Page-oriented:







#### Chapter 4. Encoding and Evolution

  - Backward compatibility
    - Newer code can read data that was written by older code.
    - Easy to achieve.

  - Forward compatibility
    - Older code can read data that was written by newer code.
    - Tricky to achieve.

  - Representational State Transfer (REST), and remote procedure calls (RPC), as well as message-passing systems such as actors and message queues.

  - **Formats for Encoding Data**

    - **Encoding**: The translation from the in-memory representation to a byte sequence (also known as __*serialization*__ or __*marshalling*__).

    - **Decoding**: The reverse of encoding, the translation from a byte sequence to the in-memory representation.
      - Parsing
      - Deserialization
      - Unmarshalling

    - **Language-Specific Formats**
      | Language | Serialization Method |
      |----------|----------------------|
      | Python   | Pickle               |
      | Java     | java.io.Serializable |
      | Ruby     | Marshal              |
      | Java     | Kryo (TPD)           |

    - **JSON, XML, and Binary Variants**

      - In XML and CSV, you cannot distinguish between a number and a string that happens to consist of digits (except by referring to an external schema). JSON distinguishes strings and numbers, but it doesn’t distinguish integers and floating-point numbers, and it doesn’t specify a precision.

        - integers greater than 253 cannot be exactly represented in an IEEE 754 double-precision floating-point number, so such numbers become inaccurate when parsed in a language that uses floating-point numbers (such as JavaScript). 

          - Twitter uses a 64-bit number to identify each tweet. The JSON returned by Twitter’s API includes tweet IDs twice, once as a JSON number and once as a decimal string.

      - JSON and XML have good support for Unicode character strings (i.e., human-readable text), but they don’t support binary strings (sequences of bytes without a character encoding).


      - CSV does not have any schema, so it is up to the application to define the meaning of each row and column.
    
    The difficulty of getting different organizations to agree on anything outweighs most other concerns.

    - **Binary encoding**

      - For data that is used only internally within your organization, there is less pressure to use a lowest-common-denominator encoding format.

      - JSON is less verbose than XML, but both still use a lot of space compared to binary formats. This observation led to the development of a profusion of binary encodings for JSON: 
        - (MessagePack, BSON, BJSON, UBJSON, BISON, and Smile, to name a few)
      - XML 
        - (WBXML and Fast Infoset, for example). 

    - **Thrift and Protocol Buffers**
      - Apache Thrift (FaceBook) and Protocol Buffers (protobuf) (Google) are binary encoding libraries.

      - Thrift and Protocol Buffers each come with a code generation tool that takes a schema definition like the ones shown here, and produces classes that implement the schema in various programming languages [18]. Your application code can call this generated code to encode or decode records of the schema.

    - **Field tags and schema evolution**

      - Removing a field is just like adding a field, with backward and forward compatibility concerns reversed. That means you can only remove a field that is optional (a required field can never be removed), and you can never use the same tag number again (because you may still have data written somewhere that includes the old tag number, and that field must be ignored by new code).

    - Read this subsection if you want to know what a tag is in this context.

  - **Datatypes and schema evolution**

    - What about changing the datatype of a field? That may be possible—check the documentation for details—but there is a risk that values will lose precision or get truncated. For example, say you change a 32-bit integer into a 64-bit integer. New code can easily read data written by old code, because the parser can fill in any missing bits with zeros. However, if old code reads data written by new code, the old code is still using a 32-bit variable to hold the value. If the decoded 64-bit value won’t fit in 32 bits, it will be truncated.

    - A curious detail of Protocol Buffers is that it does not have a list or array datatype, but instead has a `repeated` marker for fields (which is a third option alongside `required` and `optional`).
      - This has the nice effect that it’s okay to change an `optional` (single-valued) field into a `repeated` (multi-valued) field.

  - **Avro**
    - Apache Avro [20] is another binary encoding format that is interestingly different from Protocol Buffers and Thrift.
      - Avro also uses a schema to specify the structure of the data being encoded. It has two schema languages: one (Avro IDL) intended for human editing, and one (based on JSON) that is more easily machine-readable.

    - **But what is the writer’s schema?**
      - Read this and make good sumarized notes.

    - **Dynamically generated schemas**
      - Read this and make good sumarized notes.

  - **Dataflow Through Databases**
    Section talks about how you should write data to the DB in such a way that the future code shouldn't have trouble reading it. It also mentions an example where an ORM might be troublesom when updating DB records if the application code isn't updated (check the image 4-7). 

    Lastly, it talks about how __*snapshots*__ are saved for backup and how you could take advantage of the fact they're read only and use an encoder format like parquet for data-warehousing for analytics or use Avro to reduce the snapshot file size.
    - **DB migrations**: Rewriting data.

  - **Dataflow Through Services: REST and RPC**
    When communicating over a network there are a few different ways of arranging that communication. The most common arrangement is to have two roles:

    - Clients: Connect to the servers to make requests to that API.

    - Servers: Expose an API over the network.
      - Can be clients to other servers.

    - Service: The API exposed by the server.
      - Services can impose fine-grained restrictions on what clients can and cannot do (this is a way of encapsulation). 

    - **Ajax**: *Asynchronous Javascript and XML* is a technique where a client-side JavaScript application running inside a web browser can use XMLHttpRequest to become an HTTP client.
      - In this case, the server’s response is typically not HTML for displaying to a human, but rather data in an encoding that is convenient for further processing by the client-side application code (such as JSON). Although HTTP may be used as the transport protocol, the API implemented on top is application-specific, and the client and server need to agree on the details of that API.

      - A key design goal of a service-oriented/microservices architecture is to make the application easier to change and maintain by making services independently deployable and evolvable.
        - For example, each service should be owned by one team, and that team should be able to release new versions of the service frequently, without having to coordinate with other teams.
        - We should expect old and new versions of servers and clients to be running at the same time:
          - Data encoding used by servers and clients must be compatible across versions of the service API.

    - **SOA**: **Service Oriented Architecture** more recently refined and rebranded as __*microservices architecture*__:
      - Moreover, a server can itself be a client to another service (for example, a typical web app server acts as client to a database). This approach is often used to decompose a large application into smaller services by area of functionality, such that one service makes a request to another when it requires some functionality or data from that other service. This way of building applications has traditionally been called a **SOA**, more recently...

    - One service making requests to another service owned by the same organization, often located within the same datacenter, as part of a service-oriented/microservices architecture. (Software that supports this kind of use case is sometimes called **middleware**.)

    - There are two popular approaches to web services:

      - **REST**: *REpresentational State Transfer* is a design philosophy that builds upon the principles of HTTP.
        - Simple formats.
        - Using URLs for identifying resources .
        - Using HTTP features for cache control, authentication, and content type negotiation.
        - An API designed according to the principles of REST is called RESTful.

      - **SOAP**: *Simple Object Access Protocol is an XML-based protocol for making network API requests.
        - Aims to be independent from HTTP and avoids using most HTTP features.
        - It comes with a sprawling and complex multitude of related standards (the web service framework, known as WS) that add various features.
        - The API of a SOAP web service is described using an XML-based language called the *Web Services Description Language*, or __*WSDL*__.
          - WSDL enables code generation so that a client can access a remote service using local classes and method calls (which are encoded to XML messages and decoded again by the framework). 
          - **WSDL** is not designed to be human-readable.
        - Users of SOAP rely heavily on tool support, code generation, and IDEs.
      
      - **The problems with remote procedure calls (RPCs)**

        - **RPC**: Remote Procedure Call.
          - The RPC model tries to make a request to a remote network service look the same as calling a function or method in your programming language, within the same process (this abstraction is called *location transparency*).
          - The main focus of RPC frameworks is on requests between services owned by the same organization, typically within the same datacenter.

        - **Idempotence**:

        - Thrift and Avro come with RPC support included.
        - **gRPC** is an RPC implementation using Protocol Buffers.

      - **Data encoding and evolution for RPC**
        - We can make a simplifying assumption in the case of dataflow through services: it is reasonable to assume that all the servers will be updated first, and all the clients second. 
          - Thus, you only need backward compatibility on requests, and forward compatibility on responses.

        - The backward and forward compatibility properties of an RPC scheme are inherited from whatever encoding it uses:
          - Thrift, gRPC (Protocol Buffers), and Avro RPC can be evolved according to the compatibility rules of the respective encoding format.
          - In SOAP, requests and responses are specified with XML schemas. These can be evolved, but there are some subtle pitfalls [47].
          - RESTful APIs most commonly use JSON (without a formally specified schema) for responses, and JSON or URI-encoded/form-encoded request parameters for requests. Adding optional request parameters and adding new fields to response objects are usually considered changes that maintain compatibility.

        - Service compatibility is made harder by the fact that RPC is often used for communication across organizational boundaries, so the provider of a service often has no control over its clients and cannot force them to upgrade.
          - If a compatibility-breaking change is required, the service provider often ends up maintaining multiple versions of the service API side by side.


        - There is no agreement on how API versioning should work (i.e., how a client can indicate which version of the API it wants to use [48]). 
          - For RESTful APIs, common approaches are to use a version number in the URL or in the HTTP header. 
          - For services that use API keys to identify a particular client, another option is to store a client’s requested API version on the server and to allow this version selection to be updated through a separate administrative interface [49].

  - **Message-Passing Dataflow**
    - Asynchronous message-passing systems
      
      - Somewhere between RPC (one process sends a request over the network to another process and expects a response as quickly as possible) and databases (where one process writes encoded data, and another process reads it again sometime in the future).
         
         - They are similar to RPC in that a client’s request (usually called a message) is delivered to another process with low latency. 
         - They are similar to databases in that the message is not sent via a direct network connection, but goes via an intermediary called a message broker (also called a __*message queue*__ or __*message-oriented middleware*__), which stores the message temporarily.
      
      - **Message Broker Advantages over RPC**
        - It can act as a buffer if the recipient is unavailable or overloaded, and thus improve system reliability.

        - It can automatically redeliver messages to a process that has crashed, and thus prevent messages from being lost.

        - It avoids the sender needing to know the IP address and port number of the recipient.

        - It allows one message to be sent to several recipients.

        - It logically decouples the sender from the recipient (the sender just publishes messages and doesn’t care who consumes them).

        However, a difference compared to RPC is that message-passing communication is usually one-way: a sender normally doesn’t expect to receive a reply to its messages. It is possible for a process to send a response, but this would usually be done on a separate channel. 
        
        This communication pattern is __*asynchronous*__: the sender doesn’t wait for the message to be delivered, but simply sends it and then forgets about it.

      - **Message brokers**
        - RabbitMQ 
        - ActiveMQ 
        - HornetQ 
        - NATS
        - Apache Kafka

        - Usage:
          1. one process sends a message to a named queue or topic.
          2. The broker ensures that the message is delivered to one or more consumers of or subscribers to that queue or topic.
          3. There can be many producers and many consumers on the same topic.
        
        - A topic provides only one-way dataflow. However, a consumer may itself publish messages to another topic, or to a reply queue that is consumed by the sender of the original message (allowing a request/response dataflow, similar to RPC).

        - Message brokers typically don’t enforce any particular data model—a message is just a sequence of bytes with some metadata, so you can use any encoding format. If the encoding is backward and forward compatible, you have the greatest flexibility to change publishers and consumers independently and deploy them in any order.

        - If a consumer republishes messages to another topic, you may need to be careful to preserve unknown fields, to prevent the issue described previously in the context of databases.

      - **Distributed actor frameworks**

        - Read and synthetizee...

         - The actor model is a programming model for concurrency in a single process. Rather than dealing directly with threads (and the associated problems of race conditions, locking, and deadlock), logic is encapsulated in actors. Each actor typically represents one client or entity, it may have some local state (which is not shared with any other actor), and it communicates with other actors by sending and receiving asynchronous messages. Message delivery is not guaranteed: in certain error scenarios, messages will be lost. Since each actor processes only one message at a time, it doesn’t need to worry about threads, and each actor can be scheduled independently by the framework.

### Part II

  - **shared-memory architecture**: All the components can be treated as a single machine 
    - Many CPUs, many RAM chips, and many disks can be joined together under one operating system, and a fast interconnect allows any CPU to access any part of the memory or disk.
      - The problem with a shared-memory approach is that the cost grows faster than linearly: a machine with twice as many CPUs, twice as much RAM, and twice as much disk capacity as another typically costs significantly more than twice as much.
        - And due to bottlenecks, a machine twice the size cannot necessarily handle twice the load.

  - **shared-disk architecture**: Uses several machines with independent CPUs and RAM, but stores data on an array of disks that is shared between the machines, which are connected via a fast network.
    - This architecture is used for some data warehousing workloads, but contention and the overhead of locking limit the scalability of the shared-disk approach.

  - **Shared Nothing Architectures**: Each machine or virtual machine running the database software is called a node. Each node uses its CPUs, RAM, and disks independently. Any coordination between nodes is done at the software level, using a conventional network.
    - No special hardware is required by a shared-nothing system, so you can use whatever machines have the best price/performance ratio.
  
  - **Replication Versus Partitioning**
    - **Replication**: Keeping a copy of the same data on several different nodes, potentially in different locations. Replication provides redundancy: if some nodes are unavailable, the data can still be served from the remaining nodes. 
      - Replication can also help improve performance.
    
    - **Partitioning (Sharding)**: Splitting a big database into smaller subsets called partitions so that different partitions can be assigned to different nodes (also known as sharding).
