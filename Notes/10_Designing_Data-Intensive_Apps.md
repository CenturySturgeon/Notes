# Part I

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

### Log

- An append-only sequence of records.
    - Many databases internally use a log, which is an append-only data file.

  - **Application Logs**:
    - These logs record events and activities within an application.
    - Example: Log files capturing user interactions, errors, or system events.

  - **DB Log**:
    
    - Some databases use an internal append-only log to track records.
    
    - **Note**: Consider the example of the world's simplest database using bash commands, which illustrates how a log can be used in this context:
      ```bash
        db_set() {
            echo "$1, $2" >> database
        }
        
        db_get() {
            grep "^$1," database | sed -e 's/^$1,//' | tail -n 1
        }
      ```
    
    - In this example:
      - `db_set` appends a record (key-value pair) to the `database` file.
      - `db_get` retrieves the most recent value associated with a key from the `database` file.

  - **Understanding Logs**:
    - Logs are essential for tracking changes and maintaining a history of operations in databases.
    - The append-only nature of logs ensures that all changes are recorded sequentially, which aids in data recovery and consistency.

### Database Indexing Structures

- **Index**: An additional structure derived from the primary data. It allows faster record searches in the database but can slow down writes.

#### Hash Indexes

- **Hash Indexes**: 
  - Imagine our data storage involves only appending to a file. The simplest indexing strategy is to maintain an in-memory hash map where each key maps to a byte offset in the data file, indicating where the value can be found.
  - This is similar to the LeetCode problem *'Encode and Decode Strings'*.

#### SSTables and LSM-Trees

- **Sorted String Tables (SSTables)**:
  - Similar to log files used in the *Hash Indexes* example, but with an added detail: segment files are sorted by key, and each key appears only once within each merged segment file (ensured by the compaction process).
  - Merging segments is efficient, akin to the merge sort algorithm, even if the files are larger than available memory.
  - To find a key, you don't need an index of all keys in memory; a sparse in-memory index is sufficient. For example, if you need a key between two in-memory index keys, use the offset of the first key and search from there.
  - Since read requests involve scanning several key-value pairs, grouping records into a block and compressing it before writing to disk is possible.

- **Log-Structured Merge-Tree (LSM-Tree)**:
  - LSM storage engines are based on merging and compacting sorted files.

- **Compaction Strategies**:
  - **Size-Tiered Compaction**: Newer, smaller SSTables are merged into older, larger SSTables.
    - Used by: Cassandra, HBase
  - **Leveled Compaction**: Splits the key range into smaller SSTables and moves older data into separate levels, allowing more incremental compaction and less disk space usage.
    - Used by: LevelDB, RocksDB, Cassandra

- **Advantages**:
  - Sorted data supports efficient range queries, and sequential disk writes enable high write throughput.

#### B-Trees

- **B-Trees**:
  - Like SSTables, B-trees keep key-value pairs sorted by key, enabling efficient lookups and range queries. However, B-trees differ significantly in design.

- **Structure**:
  - B-trees use fixed-size blocks or pages (traditionally 4 KB) and read or write one page at a time.
  - **Pages**: Identified using an address, allowing pages to refer to other pages (similar to pointers but on disk).
    - **Leaf Page**: Stores values of the keys in its range without references.
    - **Branching Factor**: Number of references to child pages. Typically several hundred.

- **Operations**:
  - If a leaf page cannot accommodate a new key-value pair, it splits into two pages, and the parent page is updated.

- **Note**:
  - A B-tree with `n` keys has a depth of `O(log n)`. Most databases fit into a B-tree that's three or four levels deep, handling up to 256 TB with a branching factor of 500.

- **Write-Ahead Log (WAL)**:
  - **WAL**: An append-only file where every B-tree modification is written before being applied to the pages. This log restores the B-tree to a consistent state after a crash.

- **Concurrency Control**:
  - Managed with *latches* (lightweight locks) to prevent concurrent access issues.

- **Optimizations**:
  - **Copy-On-Write**: Some databases (e.g., LMDB) use this instead of overwriting pages and maintaining a WAL.
  - **Abbreviated Keys**: Store shorter keys in pages to save space and increase branching factor.
  - **Page Layout**: Aim to lay out leaf pages sequentially on disk, though maintaining this order can be challenging.
  - **Additional Pointers**: Leaf pages may include references to neighboring sibling pages.

- **Comparison with LSM-Trees**:
  - **Rule of Thumb**:
    - LSM-trees are generally faster for writes.
    - B-trees are typically faster for reads.
  - **Advantages of LSM-Trees**:
    - Write amplification: B-trees write data at least twice (WAL and page), while LSM-trees can reduce this through compaction.
    - Better write throughput, particularly on magnetic hard drives due to sequential writes.
    - More effective compression and lower storage overhead, especially with leveled compaction.

  - **Downsides of LSM-Trees**:
    - Compaction can interfere with performance, especially on high write throughput.
    - Disk bandwidth for initial writes and compaction may become a bottleneck.
    - Multiple copies of the same key across segments can occur.

#### Other Indexing Structures

- **Key-Value Indexes**: As discussed, similar to a primary key index in the relational model.
- **Secondary Indexes**: Can be created using the `CREATE INDEX` command in relational databases. Both B-trees and log-structured indexes can serve as secondary indexes.

#### Storing Values within the Index

- **Heap File**:
  - The index's key is used for queries, while the value can be:
    - The actual row data.
    - A reference to the row stored elsewhere in a *heap file*, which maintains data in no particular order.

- **Clustered Index**:
  - Stores the indexed row directly within the index, optimizing read performance but potentially increasing storage and write overhead.

- **Covering Index**:
  - Stores some columns of a table within the index, allowing queries to be answered by the index alone. This reduces read times but increases storage and write overhead.

#### Multi-Column Indexes

- **Concatenated Index**:
  - Combines several fields into one key by appending columns, e.g., (lastname, firstname). Useful for queries involving multiple fields in a specific order.

- **Multi-Dimensional Indexes**:
  - Generalize querying multiple columns, important for geospatial data and other multi-dimensional queries.
    - Examples:
      - Ecommerce: Search products by color (RGB dimensions).
      - Weather Database: Search for temperature observations within a range on specific dates.

### Full-Text Search and Fuzzy Indexes

- Traditional indexes do not support searching for similar keys, such as misspelled words.
- This is known as **fuzzy querying**, which requires different techniques.
- **Lucene**:
    - Lucene allows searching for words within a certain **edit distance**. For instance, an edit distance of 1 means that one letter has been added, removed, or replaced.
    - It uses an SSTable-like structure for its term dictionary. This structure includes a small in-memory index that helps locate the offset in the sorted file where a key can be found.
    - Lucene’s in-memory index is a finite state automaton over the characters in the keys, similar to a trie.
    - This automaton can be converted into a **Levenshtein automaton**, which supports efficient search for words within a given edit distance.

#### Keeping Everything in Memory

  - Compared to main memory, disks are more cumbersome to deal with. We use disks because:
    - They are **durable** (data is not lost if the power is turned off).
    - They have a **lower cost per gigabyte** compared to RAM.
  
  - As RAM prices decrease, the cost argument for disks diminishes. Many datasets are manageable within RAM, making it feasible to keep them entirely in memory, sometimes distributed across multiple machines. This has led to the development of **in-memory databases**.
    - Examples: 
        - Memcached
        - Redis
  - Some in-memory key-value stores, like **Memcached**, are designed solely for caching, where data loss upon restart is acceptable.
  
  - Other in-memory databases focus on **durability** through:
    - Special hardware (e.g., battery-powered RAM),
    - Writing a log of changes to disk,
    - Periodic snapshots to disk,
    - Replicating the in-memory state to other machines.
  
  - When an in-memory database restarts, it reloads its state from disk or over the network from a **replica**.
    - The disk acts as an append-only log for durability, while reads are served entirely from memory.
  
  - **In-memory DBs** can be faster as they avoid the overhead of encoding data structures for disk storage.
  
  - **Anti-Caching**: Evicts the least recently used data from memory to disk when memory is insufficient, and reloads it into memory when accessed again.

#### Transaction Processing or Analytics?

- **Transaction Processing vs. Analytics**:
  
  - **Transaction**: A logical unit of reads and writes. Transactions do not necessarily need to have ACID properties but should allow low-latency reads and writes.
    - Unlike batch processing jobs, which run periodically (e.g., once per day).
  
  - **OLTP** (*Online Transaction Processing*):
    - Designed to handle a high volume of short online transactions (inserts, updates, queries).
    - Focuses on:
      - Fast query processing,
      - Maintaining data integrity in multi-user environments.
    - Commonly used in applications like retail sales and banking.
  
  - **OLAP** (*Online Analytics Processing*):
    - Optimized for querying and analyzing large volumes of data.
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



### Data Warehousing

A **data warehouse** is a separate database designed for querying by analysts without affecting OLTP operations.
- Database administrators often prefer not to have analysts interacting with OLTP databases directly.
- The data warehouse contains a read-only copy of data from various OLTP systems within the company.
- **ETL** (*Extract–Transform–Load*):
    - Data is extracted from OLTP databases using either periodic data dumps or continuous updates.
    - The data is then:
      - Transformed into an analysis-friendly schema,
      - Cleaned up,
      - Loaded into the data warehouse.

#### The Divergence Between OLTP Databases and Data Warehouses

- **OLTP vs. Data Warehousing**:
  - OLTP databases are optimized for fast, real-time transaction processing and maintain data integrity.
  - Data warehouses are optimized for complex queries and data analysis, supporting historical data and large-scale data processing.

#### Stars and Snowflakes: Schemas for Analytics

- **Star Schema**: Central fact tables connected to dimension tables in a star-like pattern. Useful for straightforward querying.
- **Snowflake Schema**: A more normalized form of the star schema where dimension tables are split into multiple related tables. This reduces redundancy but can complicate queries.

#### Column-Oriented Storage

In column-oriented storage, values from each column are stored together rather than values from each row.
  
  - **Column Compression**:
    - **Note**: Systems like Cassandra and HBase use column families, but they store columns together within each family and do not use column compression extensively. Thus, they are primarily row-oriented.

  - **Memory Bandwidth and Vectorized Processing**:
    - Column-oriented storage reduces the volume of data loaded from disk and enhances CPU efficiency.
    - Column data can fit in the CPU’s L1 cache, allowing for faster processing through **vectorized processing**.
    - **Vectorized processing** involves executing operations on chunks of compressed column data directly, improving performance.

  - **Writing to Column-Oriented Storage**:
    - **LSM-trees** are effective for writing to column-oriented storage. Writes first go to an in-memory store and are then merged with column files on disk.
    - This method is utilized by systems like Vertica.

  - **Aggregation: Data Cubes and Materialized Views**:
    - **Materialized Views**:
      - Used to cache frequently queried aggregates, reducing the need to recompute them each time.
      - Unlike virtual views, materialized views store actual copies of query results on disk.
      - Updates to the underlying data require refreshing materialized views, which can make writes more expensive but beneficial for read-heavy data warehouses.

<!-- <iframe width="320" height="180" src="https://www.youtube.com/watch?v=BIlFTFrEFOI&t=64s" title="SQL Hash Indexes" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="1"></iframe> -->

- **Memtable**:
  - An in-memory balanced tree data structure, such as a red-black tree, used to manage writes before they are flushed to disk.

- **Bloom Filter**:
  - A memory-efficient data structure used to approximate the contents of a set.
  - It can indicate if a key does not exist in the database, reducing unnecessary disk reads for non-existent keys.

- **Compaction**:
  - Involves removing duplicate keys and retaining only the most recent update for each key to avoid running out of space.
  - Each segment has an in-memory hash table mapping keys to file offsets.
    - To find a key’s value, the most recent segment’s hash map is checked first, followed by older segments if necessary.
  
  - **Tombstone**:
    - A special deletion record appended to the data file to mark a key for deletion.
    - During log segment merges, tombstones instruct the merging process to discard any previous values for the deleted key.

## Storage Engines

- **Log-Structured**:
    - Optimized for write-heavy workloads with mechanisms like LSM-trees.
- **Page-Oriented**:
    - Focuses on reading and writing data in fixed-size pages, often used in traditional B-tree-based systems.








## Chapter 4. Encoding and Evolution

- **Backward Compatibility**
    - Newer code can read data that was written by older code.
        - Relatively easy to achieve.

- **Forward Compatibility**
    - Older code can read data that was written by newer code.
        - Tricky to achieve.

- **REST** 
    - Representational State Transfer
- **RPC**
    - Remote Procedure Calls

- **Message-Passing Systems**: Includes actors and message queues.

### Formats for Encoding Data

- **Encoding**: The translation from the in-memory representation to a byte sequence (also known as __*serialization*__ or __*marshalling*__).

- **Decoding**: The reverse of encoding, translating from a byte sequence to the in-memory representation.
  - Parsing
  - Deserialization
  - Unmarshalling

- **Language-Specific Formats**:
  | Language | Serialization Method     |
  |----------|--------------------------|
  | Python   | Pickle                   |
  | Java     | `java.io.Serializable`   |
  | Ruby     | Marshal                  |
  | Java     | Kryo (TPD)               |

- **JSON, XML, and Binary Variants**:
  - **JSON and XML**:
    - XML and CSV do not inherently distinguish between numbers and strings of digits (except through external schemas).
    - JSON distinguishes strings and numbers but does not differentiate between integers and floating-point numbers, nor does it specify precision.

      - **Precision Issues**: Integers greater than 2^53 cannot be exactly represented in an IEEE 754 double-precision floating-point number, leading to inaccuracies when parsed in languages using floating-point numbers (e.g., JavaScript).
        - **Example**: Twitter uses a 64-bit number for tweet IDs. Their API returns tweet IDs as both a JSON number and a decimal string to handle precision issues.

  - **Unicode Support**:
    - JSON and XML support Unicode character strings (human-readable text) but do not natively support binary strings (sequences of bytes without a character encoding).

  - **CSV**:
    - CSV lacks a schema, so the meaning of each row and column must be defined by the application.

- **Binary Encoding**
  - When data is used only internally within an organization, there is less pressure to use a lowest-common-denominator encoding format.
  
  - **Comparison with JSON and XML**:
    - JSON is less verbose than XML, but both formats still use more space compared to binary formats.

    - This has led to the development of various binary encodings for JSON, including:
      - MessagePack
      - BSON
      - BJSON
      - Smile
    
    - For XML, examples of binary encodings include:
      - WBXML
      - Fast Infoset

- **Thrift and Protocol Buffers**
  - **Apache Thrift** (developed by Facebook) and **Protocol Buffers (protobuf)** (developed by Google) are binary encoding libraries.
  - Both Thrift and Protocol Buffers provide code generation tools that:
    - Take a schema definition and produce classes that implement the schema in various programming languages.
    - Allow application code to call the generated code to encode or decode records based on the schema.

- **Field Tags and Schema Evolution**
  - **Removing Fields**:
    - Removing a field involves similar backward and forward compatibility concerns as adding a field, but with reversed implications.
    - You can only remove a field if it is optional (required fields cannot be removed).
    - Once a tag number is used, it should not be reused to avoid conflicts with existing data that might include the old tag number.

  - **Further Reading**:
    - For additional details on what a tag is in this context, refer to the subsection on tag definitions.

### Datatypes and Schema Evolution

  - **Changing Data Types**:
    - Changing the datatype of a field might be possible but can result in loss of precision or truncation. For example:
      - Changing a 32-bit integer to a 64-bit integer:
        - **New Code**: Can read data written by old code since it can handle the extra bits by filling them with zeros.
        - **Old Code**: Uses a 32-bit variable, so if it reads a 64-bit value, it may be truncated if the value exceeds 32 bits.

  - **Protocol Buffers**:
    - Protocol Buffers do not have a dedicated list or array datatype but use a `repeated` marker for fields.
      - This allows converting an `optional` (single-valued) field into a `repeated` (multi-valued) field without issues.

- **Avro**
    - Apache Avro is another binary encoding format that differs from Protocol Buffers and Thrift.
    - Avro uses schemas to define data structures and supports two schema languages:
      - **Avro IDL**: Intended for human editing.
      - **JSON-Based Schema**: More machine-readable.

  - **Writer’s Schema**:
    - For details on the writer’s schema, refer to the specific subsection.

  - **Dynamically Generated Schemas**:
    - For details on dynamically generated schemas, refer to the specific subsection.

### Dataflow Through Databases

Section talks about how you should write data to the DB in such a way that the future code shouldn't have trouble reading it. It also mentions an example where an ORM might be troublesom when updating DB records if the application code isn't updated (check the image 4-7). 

Lastly, it talks about how __*snapshots*__ are saved for backup and how you could take advantage of the fact they're read only and use an encoder format like parquet for data-warehousing for analytics or use Avro to reduce the snapshot file size.
- **DB migrations**: Rewriting data.

- **Dataflow Through Services: REST and RPC**

  - **Communication Roles**:
    - **Clients**: Connect to servers to make API requests.
    - **Servers**: Expose APIs over the network and may act as clients to other servers.

  - **Services**:
    - The API exposed by the server can impose restrictions on what clients can do, serving as a form of encapsulation.

  - **Ajax**:
    - *Asynchronous JavaScript and XML*: A technique where client-side JavaScript applications use XMLHttpRequest to act as HTTP clients.
      - The server response is typically data in a format like JSON for further client-side processing.
      - The API implemented on top is application-specific, and both client and server must agree on API details.

  - **Service-Oriented Architecture (SOA)**:
    - **Microservices Architecture**: A refined version of SOA.
      - Services should be independently deployable and evolvable, allowing teams to release new versions frequently without coordination with others.
      - Expect old and new versions of servers and clients to run simultaneously, requiring compatible data encoding across service API versions.

  - **Middleware**:
    - Software that supports service-to-service communication within the same organization, often within the same datacenter, is referred to as middleware.

### Popular Approaches to Web Services

  - **REST (REpresentational State Transfer)**:
    - A design philosophy built upon HTTP principles.
    - Key Characteristics:
      - Simple formats.
      - Uses URLs to identify resources.
      - Leverages HTTP features for cache control, authentication, and content type negotiation.
    - An API designed according to REST principles is called RESTful.

  - **SOAP (Simple Object Access Protocol)**:
    - An XML-based protocol for network API requests.
    - Key Characteristics:
      - Aims to be independent of HTTP and avoids using most HTTP features.
      - Includes a complex array of related standards (the web service framework known as WS) for additional features.
      - The API is described using an XML-based language called **WSDL (Web Services Description Language)**.
        - **WSDL** allows for code generation so clients can interact with remote services using local classes and methods, which are encoded to XML messages and decoded by the framework.
        - **WSDL** is not designed for human readability.
      - SOAP relies heavily on tool support, code generation, and IDEs.

  - **RPC (Remote Procedure Call)**:
    - RPC attempts to make remote network service requests resemble function or method calls in your programming language, within the same process (this abstraction is known as *location transparency*).
    - Focuses primarily on requests between services owned by the same organization, typically within the same datacenter.

  - **RPC Implementations**:
    - **Thrift and Avro**: Both come with built-in RPC support.
    - **gRPC**: An RPC implementation using Protocol Buffers.

  - **Data Encoding and Evolution for RPC**:
    - Simplifying Assumption:
      - It is reasonable to assume servers are updated before clients. Thus, backward compatibility is needed for requests, and forward compatibility is needed for responses.
    - Compatibility Properties:
      - **Thrift, gRPC (Protocol Buffers), and Avro RPC**: Evolve according to the compatibility rules of their respective encoding formats.
      - **SOAP**: Requests and responses are specified with XML schemas, which can be evolved, but subtle pitfalls exist.
      - **RESTful APIs**: Typically use JSON (without a formal schema) for responses, and JSON or URI-encoded/form-encoded parameters for requests. Adding optional parameters and new fields to responses usually maintains compatibility.

    - **Challenges**:
      - RPC is often used across organizational boundaries, making it difficult for the service provider to control client upgrades.
      - Compatibility-breaking changes often require maintaining multiple versions of the API side by side.

    - **API Versioning**:
      - No universal agreement on API versioning methods.
      - Common Approaches:
        - **RESTful APIs**: Version numbers in the URL or HTTP headers.
        - **API Keys**: Store requested API versions on the server and manage version selection through an administrative interface.

### Message-Passing Dataflow

- **Asynchronous Message-Passing Systems**:
    - These systems are situated between RPC (where one process sends a request to another process expecting a quick response) and databases (where one process writes data and another reads it later).
    
    - **Characteristics**:
      - Similar to RPC in that messages (requests) are delivered with low latency.
      - Similar to databases in that messages are sent through an intermediary called a message broker (or message queue, or message-oriented middleware), which temporarily stores the messages.
    
    - **Message Broker Advantages Over RPC**:

      - **Buffering**: Acts as a buffer if the recipient is unavailable or overloaded, improving system reliability.
      - **Automatic Redelivery**: Redelivers messages if the process has crashed, preventing message loss.
      - **Address Independence**: The sender does not need to know the recipient’s IP address and port number.
      - **Broadcasting**: Allows a single message to be sent to multiple recipients.
      - **Decoupling**: Logically decouples the sender from the recipient; the sender just publishes messages without needing to know who will consume them.
    
    - **Communication Pattern**:
      - Typically one-way: the sender does not expect a reply to the message, although responses can be sent on a separate channel.
      - Asynchronous: The sender does not wait for the message to be delivered but sends it and proceeds.

  - **Message Brokers**:
    - **Examples**:
      - RabbitMQ
      - ActiveMQ
      - HornetQ
      - NATS
      - Apache Kafka
    
    - **Usage**:
      1. A process sends a message to a named queue or topic.
      2. The broker ensures that the message is delivered to one or more consumers/subscribers.
      3. Multiple producers and consumers can interact with the same topic.
    
    - **Topics and Dataflow**:
      - A topic provides one-way dataflow, but a consumer can publish messages to another topic or a reply queue, enabling request/response patterns similar to RPC.
    
    - **Data Model**:
      - Message brokers do not enforce a specific data model; messages are sequences of bytes with metadata. Flexible encoding formats can be used as long as they are backward and forward compatible.
    
    - **Message Republishing**:
      - If a consumer republishes messages to another topic, care must be taken to preserve unknown fields to avoid issues similar to those in databases.

  - **Distributed Actor Frameworks**:
      - The actor model is a concurrency model within a single process. Instead of managing threads directly, logic is encapsulated in actors.
     
      - **Actor Characteristics**:
        - Each actor represents a client or entity with local state (not shared with other actors).
        - Actors communicate through asynchronous messages.
        - Message delivery is not guaranteed; messages may be lost in certain error scenarios.
        - Actors process one message at a time, avoiding threading issues, and can be scheduled independently by the framework.
    
    - **Further Reading**:
      - For a detailed understanding, refer to resources on distributed actor frameworks and their implementation.

### Additional concepts
- **Idempotence**:
    - Refers to operations where repeating the operation has the same effect as performing it once. (Details are not covered in this section but are important for RPC operations.)


# Part II

## Shared-Memory Architecture

All the components can be treated as a single machine 
  - Many CPUs, many RAM chips, and many disks can be joined together under one operating system, and a fast interconnect allows any CPU to access any part of the memory or disk.

    - The problem with a shared-memory approach is that the cost grows faster than linearly: a machine with twice as many CPUs, twice as much RAM, and twice as much disk capacity as another typically costs significantly more than twice as much.
      
    - And due to bottlenecks, a machine twice the size cannot necessarily handle twice the load.

## Shared-Disk Architecture
Uses several machines with independent CPUs and RAM, but stores data on an array of disks that is shared between the machines, which are connected via a fast network.

  - This architecture is used for some data warehousing workloads, but contention and the overhead of locking limit the scalability of the shared-disk approach.

- **Shared Nothing Architectures
Each machine or virtual machine running the database software is called a node. Each node uses its CPUs, RAM, and disks independently. 
  - Any coordination between nodes is done at the software level, using a conventional network.
  - No special hardware is required by a shared-nothing system, so you can use whatever machines have the best price/performance ratio.

## Replication Versus Partitioning (Sharding)

  - **Replication**: Keeping a copy of the same data on several different nodes, potentially in different locations. Replication provides redundancy: if some nodes are unavailable, the data can still be served from the remaining nodes. 
    - Replication can also help improve performance.
  
  - **Partitioning (Sharding)**: Splitting a big database into smaller subsets called partitions so that different partitions can be assigned to different nodes (also known as sharding).
