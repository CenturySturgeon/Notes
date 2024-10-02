# Handy Stuff

Amazon Relational Database Service (RDS), can get you a database server with 24 TB of RAM. For example, stackoverflow.com in 2013 had over 10 million monthly unique visitors, but it only had 1 master database.

## Memory Basics

### Memory Units

| Power | Approx Value  | Short Name | Numeric Representation  (Bytes) | Number of 0s |
|-------|---------------|------------|---------------------------------|--------------|
| 10    | 1 Thousand    | 1 KB       | 1,000                           | 3            |
| 20    | 1 Million     | 1 MB       | 1,000,000                       | 6            |
| 30    | 1 Billion     | 1 GB       | 1,000,000,000                   | 9            |
| 40    | 1 Trillion    | 1 TB       | 1,000,000,000,000               | 12           |
| 50    | 1 Quadrillion | 1 PB       | 1,000,000,000,000,000           | 15           |

- **Note**: Everything is in American orders of magnitude (1 billion in Spanish isn't a billion but rather 1,000 millions etc.).

| Item                  | Size      |
|-----------------------|-----------|
| 1 Byte                | 8 bits    |
| 1 IPv4 Address        | 4 Bytes   |
| 1 Unix Timestamp      | 4 Bytes   |
| 1 IPv6 Address        | 16 Bytes  |


Keep in mind, if you ever hear *"Big Data"* in an interview they're talking about Terabytes [TB] or Petabytes [PB].

### Sizes Of Commonly Used Resources

| Item              | Size/Unit                            | Notes                                                          |
|-------------------|--------------------------------------|----------------------------------------------------------------|
| ASCII Character   | 1 byte                               | Standard ASCII uses 7 bits, but 1 byte is common.              |
| UTF-8 Character   | 1 to 4 bytes                         | Variable-length encoding.                                      |
| UUID              | 16 Bytes                             | Consists of a mix of numbers and letters.                      |
| Image (JPEG)      | ~500 KB to 5 MB (or more) per image  | Depends on resolution and compression.                         |
| Image (PNG)       | ~200 KB to 10 MB (or more) per image | Lossless compression, larger files.                            |
| Video (720p)      | ~1.5 GB per hour                     | Depends on bitrate and codec.                                  |
| Video (1080p)     | ~3 GB per hour                       | Higher resolution increases size.                              |
| Audio (MP3)       | ~1 MB per minute                     | Depends on bitrate (e.g., 128 kbps).                           |
| Email             | Varies [~20 KB for text only]        | Size can vary depending on content, attachments, and encoding. |
| Web Page (HTML)   | ~1 KB to 1 MB per page               | Depends on content and resources.                              |
| Book              | ~300 KB to 2 MB                      | Depends on formatting and length.                              |
| Ten Page Document | ~100 KB to 500 KB                    | Varies with images, formatting, and content.                   |


## Networks

### Estimated Round-Trip Times** (RTT):

| Distance Type                                    | Typical Latency        |
|--------------------------------------------------|------------------------|
| Within the same continent                        | 20 to 100 ms           |
| Intercontinental (e.g., North America to Europe) | 100 to 200 ms          |
| Around the world                                 | Exceeds 300 ms or more |


## DB Stuff

### Quorum Consensus

- **N**: The toal number of nodes.
- **W**: The number of nodes that need to acknowledge (return 201) when you perform a write operation.
- **R**: The number of nodes that need to be probed when you perform a Read operation. This is so you can compare their responses and use the most recent data.

- If `W + R > N`, strong consistency is guaranteed because there's an overlapping node that has the latest data to ensure consistency.

  | Configuration   | Description                                              |
  |-----------------|----------------------------------------------------------|
  | R = 1 and W = N | Optimized for a fast read                                |
  | W = 1 and R = N | Optimized for a fast write                               |
  | W + R > N       | Strong consistency guaranteed (Usually N = 3, W = R = 2) |
  | W + R <= N      | Strong consistency not guaranteed                        |

  - For your examples in the interview, use `N=3` for your examples as it's eassier to understand the table above.

### Consistency Models

| Consistency Model    | Description                                                                                                   |
|----------------------|---------------------------------------------------------------------------------------------------------------|
| Strong Consistency   | Any read operation returns the most updated value; clients never see out-of-date data.                        |
| Weak Consistency     | Subsequent read operations may not see the most updated value.                                                |
| Eventual Consistency | Given enough time, all updates are propagated, and all replicas become consistent (weak consistency variant). |

> Strong consistency is usually achieved by forcing a replica not to accept new reads/writes until every replica has agreed on current write. This approach is not ideal for highly available systems because it could block new operations

## APIs

### REST

#### Request Anatomy

1. Method
  
    | Method  | Description                                                   |
    |---------|---------------------------------------------------------------|
    | GET     | Retrieve data from the server.                                |
    | POST    | Submit data to the server, creating a resource.               |
    | PUT     | Update an existing resource or create it if it doesn't exist. |
    | DELETE  | Remove a resource from the server.                            |
    | PATCH   | Partially update an existing resource.                        |
    | HEAD    | Similar to GET, but retrieves only headers.                   |
    | OPTIONS | Describes the communication options for the target resource.  |

2. URL
    - **Protocol**: `http` or `https`.
    - **Domain**: The server's address (e.g., `api.example.com`).
    - **Path**: The specific resource (e.g., `/users/123`).
    - **Query Parameters** (optional): Key-value pairs for additional filtering (e.g., `?sort=asc&limit=10`).


3. Headers
    - **Content-Type**: Specifies the media type of the resource (e.g., `application/json`).
    - **Authorization**: Credentials for authenticating the request (e.g., `Bearer token`).
    - **Accept**: Indicates the media types that are acceptable for the response (e.g., `application/json`).

4. Body
    - **JSON**.
    - **XML**.
    - **Form Data**: Key-value pairs sent as form submissions.

- Example: 
  ```csharp
  [METHOD, URL, PROTOCOL]
  POST https://api.example.com/users HTTP/1.1

  [HEADERS]
  Content-Type: application/json
  Authorization: Bearer YOUR_JWT_TOKEN
  Accept: application/json

  [BODY]
  {
    "name": "John Doe",
    "email": "john.doe@example.com",
    "age": 30
  }
  ```

#### HTTP Status Codes

| Status Code Category | Description   | Examples                    |
|----------------------|---------------|-----------------------------|
| **1xx**              | Informational | 100 (Continue)              |
|                      |               | 101 (Switching Protocols)   |
| **2xx**              | Successful    | 200 (OK)                    |
|                      |               | 201 (Created)               |
|                      |               | 202 (Accepted)              |
| **3xx**              | Redirection   | 301 (Moved Permanently)     |
|                      |               | 307 (Temporary Redirect)    |
| **4xx**              | Client Error  | 400 (Bad Request)           |
|                      |               | 401 (Unauthorized)          |
|                      |               | 403 (Forbidden)             |
|                      |               | 404 (Not Found)             |
| **5xx**              | Server Error  | 500 (Internal Server Error) |
|                      |               | 502 (Bad Gateway)           |
|                      |               | 503 (Service Unavailable)   |




## Hashing and Consistent Hashing

### Hash Function Outputs

  - [Online Hash Function Comparer](https://md5calc.com/hash/sha256/LSKDJFHSFA)

  | Hash Function | Output                                                           |
  |---------------|------------------------------------------------------------------|
  | CRC32         | 747900d0                                                         |
  | SHA1          | ffb9e0aec8fefa6497076632823d7bb0704dff95                         |
  | SHA256        | 9b6e9d23eaf779fc30ec88e4ff7ee734528a4b5844234e0247c5ce7ef1a3fd0f |


### Re-Read
- Sloppy Quorums (chapter 6).
  * Instead of enforcing the quorum requirement, the system chooses the first W healthy servers for writes and first R healthy servers for reads on the hash ring. Offline servers are ignored.

- Hinted Handoff (chapter 6).
  * If a server is unavailable, another server will process requests temporarily. When the down server is up, changes will be pushed back to achieve data consistency.
  * Used to handle temprary (NOT PERMANENT) failures.

- Anti-entropy (chapter 6) [used for handling permanent node failures].
  * Uses Merkle trees for inconsistency detection and minimizing the amount of data transferred.
    > A hash tree or Merkle tree is a tree in which every non-leaf node is labeled with the hash of the labels or values (in case of leaves) of its child nodes. Hash trees allow efficient and secure verification of the contents of large data structures.

  * Understangind Merkle trees is going to be hard, but the main idea is that from the parent node of two merkle trees (one for each replica) you can compare their hashes and determine if they have different data. If the hashes don't match, then there's a conflict and you will recursivly do this for their children nodes until you find the conflicting data.

- Bloom filter (chapter 6 & 8)
  * The bloom filter is used to figure out which SSTables might contain the key.
  * (chapter 8) A bloom filter is a space-efficient probabilistic technique to test if an element is a member of a set. Refer to the reference material [2] for more details.

- **Epoch** (chapter 7)
  * The epoch is where you meassure time from (think of unix timestamps, their epoch is Jan x something).

### Fundamentals

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

"Sharding; the horizontal scaling of DBs"

> Sharding separates large databases into smaller, more easily managed parts called shards. Each shard shares the same schema, though the actual data on each shard is unique to the
shard.

> The most important factor to consider when implementing a sharding strategy is the choice of the sharding key. Sharding key (known as a partition key) consists of one or more columns that determine how data is distributed.

  * Choose a key that can evenly distribute data.

<details>
  <summary><h5 style="display: inline;">Latency Numbers Every Programmer Should Know</h5></summary><br>

[Latency Numbers Every Programmer Should Know](https://colin-scott.github.io/personal_website/research/interactive_latency.html)

This website is really useful so you can get an idea (it's a little outdated, 2020) of the latency (how much time it takes an operation to perform) when working with data.

![LatencyNumbers](../images/LatencyNumbers.jpg)

</details>


## Alex Xu

### Chapter 8 notes

- Hashing functions for tiny url
  - CRC32
  - MD5
  - SHA-1. 

## Doubts I Had

### Are all shards stored in a single server (like a group)?

> what I want to visualize is when a user requests data from the partitioned DB, do all shards have to be in the same server or can some be on other servers ? If all shards need to be on the same server, that would mean that if we scale to other servers then this setup (all shards needed to complete the whole data record) would have to be in each and every single one of them right?

#### Answer:

1. **Independent Shards**: In a properly designed sharded database, each shard typically resides on a different server. This is essential for scalability and performance. Each shard holds a distinct subset of the data, which allows for horizontal scaling—adding more servers to distribute the load.

2. **Data Retrieval**:
   - When a user requests data, the application needs to know which shard holds the relevant data. The routing mechanism (often based on a key or range) directs the request to the appropriate shard.
   - If all shards were on a single server, that server would become a bottleneck, limiting the benefits of sharding. 

3. **Scaling Out**:
   - If you scale out by adding more servers, each server can host one or more shards. The system can still function if some shards are distributed across different servers. This means that when you add servers, you don’t have to replicate all shards on each server.
   - Instead, you distribute the shards among the available servers. For example, if you have 4 shards and 4 servers, each server could host one shard. If you add more servers, you could redistribute shards across the new setup.

4. **Whole Data Records**: If a user needs data that spans multiple shards (for example, in a case where data is partitioned by user ID, and a request requires data from two different users), the application layer must handle combining that data from the respective shards. This means that it might need to query multiple servers.

#### Summary

In summary, not all shards need to be on the same server. In a well-designed sharding architecture, shards are typically distributed across multiple servers, allowing for better scalability and performance. Each server can independently manage its shard(s), and the application can route requests accordingly. This setup allows for efficient scaling without the need to replicate all shards on every server.






### Replication to shards that don't store the same keys

> How does partitioning and replication work together ? I mean if you have a data base and then you partition it into shards, because it got too big, how are shards replicated ? Are there multiple replicas of every shard ?

Partitioning and replication are key strategies in database design for scalability and fault tolerance.

#### Partitioning (Sharding)

- Sharding involves dividing a large dataset into smaller, more manageable pieces called shards. Each shard holds a subset of the data, allowing for horizontal scaling. For example, you might shard a user database by user ID ranges or geographic regions.

#### Replication

- Replication refers to creating copies of data to ensure availability and durability. Each shard can have one or more replicas.

#### How They Work Together

- Multiple Replicas per Shard: Typically, each shard has multiple replicas to handle failures and load balancing. For instance, if a shard is partitioned into three replicas (primary and two secondaries), all read and write operations can be directed to the primary, while reads can be distributed among secondaries.

- Consistency Models: Depending on the consistency requirements, replicas can be configured for different behaviors (e.g., eventual consistency, strong consistency).

- Data Distribution: When a write occurs, it's sent to the primary replica of the appropriate shard. The primary then replicates the change to its secondary replicas.

#### Summary

In a system with partitioning and replication:

  1. Each shard has its own set of replicas.
  2. The number of replicas can be adjusted based on fault tolerance needs.
  3. The system can handle more reads by distributing them across replicas while maintaining the integrity of the data across shards.


#### Follow-up

> Oh nice! So shards only replicate data to shards that "belong" to the same type ? (Meaning they hold the same keys for storage)

Yes, that's correct! Shards typically replicate data only within their own group or type. Each shard is responsible for a specific subset of keys, and replication occurs among replicas of that particular shard.

- Key Points:
  - Shard Ownership: Each shard holds a distinct portion of the dataset based on the sharding key. For example, if you're sharding by user ID, one shard might handle users 1-1000, while another handles users 1001-2000.

  - Local Replication: Replication is local to each shard, meaning that the replicas of a shard only contain the data for that shard. This ensures that replicas are always in sync with their primary shard.

  - Scalability: This approach allows you to scale your database horizontally while maintaining efficient data access and redundancy within each shard.


## Design Patterns

Design patterns are reusable solutions to common problems that occur in software design. They provide a template or blueprint for solving specific issues, making it easier to build systems that are flexible, maintainable, and scalable.

1. **Categories**: Design patterns are typically categorized into three main types:

   - **Creational Patterns**: Deal with object creation mechanisms, trying to create objects in a manner suitable to the situation. Examples include Singleton, Factory Method, and Abstract Factory.

   - **Structural Patterns**: Focus on how classes and objects are composed to form larger structures. Examples include Adapter, Composite, and Proxy.

   - **Behavioral Patterns**: Concerned with algorithms and the assignment of responsibilities between objects. Examples include Observer, Strategy, and Command.

2. **Not a Finished Product**: Patterns are not code that you can just plug into your application. They are guidelines or best practices that help developers think about the design of their systems.

3. **Facilitate Communication**: They provide a common vocabulary for developers, making it easier to discuss solutions to design problems.

4. **Promote Reusability**: By using established patterns, developers can avoid reinventing the wheel and can rely on proven solutions.

5. **Encourage Good Practices**: Many patterns encourage principles like separation of concerns, encapsulation, and adherence to SOLID principles, which help in creating cleaner, more maintainable code.

### Example: Singleton Pattern

To illustrate, consider the Singleton pattern. This pattern ensures that a class has only one instance and provides a global point of access to it. It's commonly used for managing shared resources, like database connections or configuration settings.

In summary, design patterns are valuable tools in software development that help streamline design processes and foster collaboration among developers by providing well-understood, reusable solutions to common challenges.

