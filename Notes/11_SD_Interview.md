# Components



## Relational DBs

- ![PostgreSQL](../images/SD_Interview/Postgres.png)

- Joins
- Indexes
- Transactions

## NoSQL DBs

    - ![DynamoDB | MongoDB | Graph | Column](../images/SD_Interview/Nosql.png)

    - Key-Value
        - Fast Access.
        - Simple Model.

    - Document
        - Schemaless.
        - Versatile.

    - Graph
        - Relationships.
        - Effective Retrieval.

    - Column
        - High performance for writes.
        - Easy to remember: Instead of writing rows it literally writes columns.

## Blob Storage

- ![Amazon S3](../images/SD_Interview/BlobStorage.png)

- Services (like __*Amazon S3*__, __*Google Cloud Storage*__) where you upload a file and you get back a *link* to access it.
    - Has file access restrictions.
    - Good scalability (used by Netflix for example).
    - Often combined with CDNs to get fast downloads world wide.

## Search Optimized DBs**
- ![ElasticSearch](../images/SD_Interview/ElasticSearch.png)

- Document Search like __*Elastic Search*__| __*AWS OpenSearch*__.

- Key Concepts
    - **Tokenization**: Breaking a piece of text into individual words.

    - **Stemming**: (like removing the stem of flowers) Reducing words to their root form. This allows you to match different forms of the same word.

    - **Fuzzy Search**: The ability to find results that are similar to a given search term.
        
        - Tolerates slight mispellings.
        
        - Edit distance calculation.
            - Measures how many letters need to be changed, added, or removed to transform one word into another.

    - **Inverted Index**: Instead of having a key matching like in a country matching several records, you have a work with a list of all the documents it appears in (think of the elastic search context).

        ```yaml
            {
                "word1": [doc1, doc2, doc3],
                "word2": [doc2, doc3, doc4],
                "word3": [doc1, doc3, doc4]
            }
        ```

## API Gateway

- ![Kong | AWS API GW](../images/SD_Interview/ApiGateway.png)

- Microservice responsible for: 

    - Routing incoming requests and returning responses.
    - Authentication
    - Rate limiting
    - Logging.

- Examples:
    - AWS API Gateway
    - Kong
    - Apigee

## Load Balancer**

- ![NGINX](../images/SD_Interview/NGINX.png)

- Distributes work across your system.

- In an interview, it can be redundant to draw a load balancer in front of every service.
    
    - Instead, either omit a load balancer from your design altogether or add one only to the front of the design as an abstraction.

- Examples

    - AWS Elastic Load Balancer
    - NGINX
    - HAProxy

## Queue

- ![Kafka](../images/SD_Interview/Kafka.png)

- You send requests to queues and you then forget about them. Then the __*workers*__, who are working at their own pace, take the requests from the queue and return the response.

    - Be careful of introducing queues into synchronous workloads.

- **Use Cases**

    - **Buffer** for Bursty Traffic: In Uber if the traffic (requests) gets to high, your petition for a ride gets pushed into a queue where you'll timely wait for your turn for a driver.

    - **Distribute Work** Across a System: In a cloud-based photo processing service, queues can be used to distribute expensive image processing tasks.

- Remember Producer/Consumer (Topics) Architecture.

- **Important Notes**

    - **Message Ordering**: Most queues are *FIFO*, but others like __Kafka__ offer more complex ordering like priority based or smthn.

    - **Retry Mechanisms**: Queues attempt to redeliver a message a certain number of times before considering it a failure.
        - The time between attempts and the number of retries is configurable.

    - **Dead Letter Queues**: You use them to store messages that failed to be processed to later check why.
        - Useful for debugging and auditing.

    - **Scaling with Partitions**: Queues can be partitioned across multiple servers so that they can scale to handle more messages. Each partition can be processed by a different set of workers. Just like databases, you will need to specify a partition key to ensure that related messages are stored in the same partition.

    - **Backpressure**: Backpressure is a way of slowing down the production of messages when the queue is overwhelmed. This helps prevent the queue from becoming a bottleneck in your system. 
        - For example, if a queue is full, you might want to reject new messages or slow down the rate at which new messages are accepted, potentially returning an error to the user or producer.

- Examples

    - Kafka
    - SQS (Managed by AWS)

## Streams

- Useful for scenarios where you're processing vast amounts of data in real-time or supporting complex processing scenarios, such as event sourcing.

    - Event sourcing is a technique where changes in application state are stored as a sequence of events. These events can be replayed to reconstruct the application's state at any point in time.

- Unlike message queues, streams can retain data for a configurable period of time, allowing consumers to read and re-read messages from the same position or from a specified time in the past.

- **Good Choice For**:
    - __When you need to process large amounts of data in real-time__: Imagine designing a system for a social media platform where you need to display real-time analytics of user engagements (likes, comments, shares) on posts. You can use a stream to ingest high volumes of engagement events generated by users across the globe. A stream processing system (like Apache Flink or Spark Streaming) can process these events in real-time to update the analytics dashboard.

    - __When you need to support complex processing scenarios like event sourcing__: Consider a banking system where every transaction (deposits, withdrawals, transfers) needs to be recorded and could affect multiple accounts. Using event sourcing with a stream like Kafka, each transaction is an event that can be stored, processed, and replayed. This setup not only allows for real-time processing of transactions but also enables the bank to audit transactions, rollback changes, or reconstruct the state of any account at any point in time by replaying the events.
- Useful for scenarios where you're processing vast amounts of data in real-time or supporting complex processing scenarios, such as event sourcing.

    - Event sourcing is a technique where changes in application state are stored as a sequence of events. These events can be replayed to reconstruct the application's state at any point in time.

- Unlike message queues, streams can retain data for a configurable period of time, allowing consumers to read and re-read messages from the same position or from a specified time in the past.

- **Good Choice For**:
    - __When you need to process large amounts of data in real-time__: Imagine designing a system for a social media platform where you need to display real-time analytics of user engagements (likes, comments, shares) on posts. You can use a stream to ingest high volumes of engagement events generated by users across the globe. A stream processing system (like Apache Flink or Spark Streaming) can process these events in real-time to update the analytics dashboard.

    - __When you need to support complex processing scenarios like event sourcing__: Consider a banking system where every transaction (deposits, withdrawals, transfers) needs to be recorded and could affect multiple accounts. Using event sourcing with a stream like Kafka, each transaction is an event that can be stored, processed, and replayed. This setup not only allows for real-time processing of transactions but also enables the bank to audit transactions, rollback changes, or reconstruct the state of any account at any point in time by replaying the events.
- Useful for scenarios where you're processing vast amounts of data in real-time or supporting complex processing scenarios, such as event sourcing.

    - Event sourcing is a technique where changes in application state are stored as a sequence of events. These events can be replayed to reconstruct the application's state at any point in time.

- Unlike message queues, streams can retain data for a configurable period of time, allowing consumers to read and re-read messages from the same position or from a specified time in the past.

- **Good Choice For**:
    - __When you need to process large amounts of data in real-time__: Imagine designing a system for a social media platform where you need to display real-time analytics of user engagements (likes, comments, shares) on posts. You can use a stream to ingest high volumes of engagement events generated by users across the globe. A stream processing system (like Apache Flink or Spark Streaming) can process these events in real-time to update the analytics dashboard.

    - __When you need to support complex processing scenarios like event sourcing__: Consider a banking system where every transaction (deposits, withdrawals, transfers) needs to be recorded and could affect multiple accounts. Using event sourcing with a stream like Kafka, each transaction is an event that can be stored, processed, and replayed. This setup not only allows for real-time processing of transactions but also enables the bank to audit transactions, rollback changes, or reconstruct the state of any account at any point in time by replaying the events.

    - __When you need to support multiple consumers reading from the same stream__: In a real-time chat application, when a user sends a message, it's published to a stream associated with the chat room. This stream acts as a centralized channel where all chat participants are subscribers. As the message is distributed through the stream, each participant (consumer) receives the message simultaneously, allowing for real-time communication. This is a great example of a publish-subscribe pattern, which is a common use case for streams.
- Useful for scenarios where you're processing vast amounts of data in real-time or supporting complex processing scenarios, such as event sourcing.

    - Event sourcing is a technique where changes in application state are stored as a sequence of events. These events can be replayed to reconstruct the application's state at any point in time.

- Unlike message queues, streams can retain data for a configurable period of time, allowing consumers to read and re-read messages from the same position or from a specified time in the past.

- **Good Choice For**:
    - __When you need to process large amounts of data in real-time__: Imagine designing a system for a social media platform where you need to display real-time analytics of user engagements (likes, comments, shares) on posts. You can use a stream to ingest high volumes of engagement events generated by users across the globe. A stream processing system (like Apache Flink or Spark Streaming) can process these events in real-time to update the analytics dashboard.

    - __When you need to support complex processing scenarios like event sourcing__: Consider a banking system where every transaction (deposits, withdrawals, transfers) needs to be recorded and could affect multiple accounts. Using event sourcing with a stream like Kafka, each transaction is an event that can be stored, processed, and replayed. This setup not only allows for real-time processing of transactions but also enables the bank to audit transactions, rollback changes, or reconstruct the state of any account at any point in time by replaying the events.

    - __When you need to support multiple consumers reading from the same stream__: In a real-time chat application, when a user sends a message, it's published to a stream associated with the chat room. This stream acts as a centralized channel where all chat participants are subscribers. As the message is distributed through the stream, each participant (consumer) receives the message simultaneously, allowing for real-time communication. This is a great example of a publish-subscribe pattern, which is a common use case for streams.
- Useful for scenarios where you're processing vast amounts of data in real-time or supporting complex processing scenarios, such as event sourcing.

    - Event sourcing is a technique where changes in application state are stored as a sequence of events. These events can be replayed to reconstruct the application's state at any point in time.

- Unlike message queues, streams can retain data for a configurable period of time, allowing consumers to read and re-read messages from the same position or from a specified time in the past.

- **Good Choice For**:
    - __When you need to process large amounts of data in real-time__: Imagine designing a system for a social media platform where you need to display real-time analytics of user engagements (likes, comments, shares) on posts. You can use a stream to ingest high volumes of engagement events generated by users across the globe. A stream processing system (like Apache Flink or Spark Streaming) can process these events in real-time to update the analytics dashboard.

    - __When you need to support complex processing scenarios like event sourcing__: Consider a banking system where every transaction (deposits, withdrawals, transfers) needs to be recorded and could affect multiple accounts. Using event sourcing with a stream like Kafka, each transaction is an event that can be stored, processed, and replayed. This setup not only allows for real-time processing of transactions but also enables the bank to audit transactions, rollback changes, or reconstruct the state of any account at any point in time by replaying the events.

    - __When you need to support multiple consumers reading from the same stream__: In a real-time chat application, when a user sends a message, it's published to a stream associated with the chat room. This stream acts as a centralized channel where all chat participants are subscribers. As the message is distributed through the stream, each participant (consumer) receives the message simultaneously, allowing for real-time communication. This is a great example of a publish-subscribe pattern, which is a common use case for streams.

- Things you should know about streams

    - **Scaling with Partitioning**: In order to scale streams, they can be partitioned across multiple servers. Each partition can be processed by a different consumer, allowing for horizontal scaling.
        
        - You'll need to provide a partition key.
    
    - **Multiple Consumer Groups**: Streams can support multiple consumer groups, allowing different consumers to read from the same stream independently. This is useful for scenarios where you need to process the same data in different ways. For example, in a real-time analytics system.
    
    - **Replication**: In order to support fault tolerance streams can replicate data across multiple servers.
    
    - **Windowing**: A way of grouping events together based on time or count. This is useful for scenarios where you need to process events in batches, such as calculating hourly or daily aggregates of data. 
        
        - Think about a real-time dashboard that shows mean delivery time per region over the last 24 hours.

- Examples
    - Apache Flink
    - Spark Streaming
    - Kafka
    - Kinesis (Managed by AWS)


## Distributed Lock

Traditional ACID DBs use transaction locks to keep data consistent, which is great for ensuring that while one user is updating a record, no one else can update it, but they're not designed for longer-term locking. 


- Distributed locks are perfect for situations where you need to lock something across different systems or processes for a reasonable period of time. 

    * They're often __implemented using__ a distributed key-value store like __*Redis*__ or __*Zookeeper*__.

    * You can use a key-value store to store a lock and then use the atomicity of the key-value store to ensure that only one process can acquire the lock at a time.

- Another handy feature of distributed locks is that they can be set to expire after a certain amount of time (what if the process crashes?).

- **System Examples**

    - **E-Commerce Checkout System**: Lock high demand items for a period of time during checkout.

    - **Ride-Sharing Matchmaking**: When a rider requests a ride, the system can lock a nearby driver, preventing them from being matched with multiple riders simultaneously. This lock can be held until the driver confirms or declines the ride or until a certain amount of time has passed.

    - **Distributed Cron Jobs**: For systems that run scheduled tasks (cron jobs) across multiple servers, a distributed lock ensures that a task is executed by only one server at a time.

    - **Online Auction Bidding System**: In an online auction, a distributed lock can be used during the final moments of bidding to ensure that when a bid is placed in the last seconds, the system locks the item to prevent other users biding at the item at the same time.

- **Things you should know**

    - **Locking Mechanisms**: One common implementation uses Redis and is called `Redlock`. Redlock uses multiple Redis instances to ensure that a lock is acquired and released in a safe and consistent manner.

    - **Lock Expiry**: Distributed locks can be set to expire after a certain amount of time. This is important for ensuring that locks don't get stuck in a locked state if a process crashes or is killed.

    - **Locking Granularity**: You can lock a single resource or a group of resources. 
        * You might want to lock a single ticket in a ticketing system or you might want to lock a group of tickets.
    
    - **Deadlocks**: Deadlocks can occur when two or more processes are waiting for each other to release a lock. Think about a situation where two processes are trying to acquire two locks at the same time:
        
        * One process acquires lock A and then tries to acquire lock B, while the other process acquires lock B and then tries to acquire lock A.

## Distributed Caches

A cache is just a server, or cluster of servers, that stores data in memory. They're great for storing data that's expensive to compute or retrieve from a database.

    * Lower the latency, scale the system.

- **Use Cases**

    - **Save Aggregated Metrics**: When a user requests a dashboard, the platform can retrieve the calculated analytics and data from the cache instead of recomputing it, reducing latency.

    - **Reduce Number of DB Queries**: User sessions are often stored in a cache to reduce the load on the database.
        
        * When a user logs in, the system can store their session data in the cache, allowing the system to quickly retrieve the data when the user makes a request.

        * Important for systems with lots of users.

    - **Speed Up Expensive Queries**: Remember the twitter landing page example.

        * This is a complex query that requires joining multiple tables and filtering by multiple columns. Instead, you can run the query once, store the results in a distributed cache, and then retrieve the results from the cache when a user requests them.

            - Remember the fan-out solution: They slowed writes for users but by caching user's landing pages reading is way faster.

- **Things you should know**

    - **Eviction Policies**: Determine which items to remove from cache when full.

        1. Least Recently Used (**LRU**): Evicts the least recently accessed items first.
        2. First In, First Out (**FIFO**): Evicts items in the order they were added.
        3. Least Frequently Used (**LFU**): Removes items that are least frequently accessed.

    - **Cache Invalidation Strategy**: Strategy to ensure that the data in your cache is up to date.

        * If you are designing Ticketmaster and caching popular events, then you'll need to invalidate an event in the cache if the event in your Database was updated (like the venue changed).

    - **Cache Write Strategy**: Ensure data is written to cache consistently.

        - **Write-Through** Cache: Writes data to both the cache and the underlying datastore simultaneously. Ensures consistency but can be slower for write operations.

        - **Write-Around** Cache: Writes data directly to the datastore, bypassing the cache. This can minimize cache pollution but might increase data fetch times on subsequent reads.
        
        - **Write-Back** Cache: Writes data to the cache and then asynchronously writes the data to the datastore. This can be faster for write operations but can lead to data loss if the cache is not persisted to disk.

- **REMEMBER**

    * Modern caches have many different *datastructures* you can leverage, they are not just simple key-value stores.

    * Be explicit about what data you are storing in the cache, including the data structure you're using.

- **Redis**
    
    - Strings
    - Hashes
    - Lists
    - Sets
    - Sorted sets
    - Bitmaps
    - Hyperloglogs

- **Memcached**

    - Strings
    - Binary objects.


## CDN

A content delivery network (CDN) is a type of cache that uses distributed servers to deliver content to users based on their geographic location.

CDNs are often used to deliver static content like images, videos, and HTML files, but they can also be used to deliver dynamic content like API responses.

> CDNs are often used to deliver static content like images, videos, and HTML files, but they can also be used to deliver dynamic content like API responses.

- The most common application of a CDN in an interview is to cache static media assets like images and videos.

- **Things you should know**
    
    - **CDNs are not just for static assets**: They can store *dynamic content*. This is especially useful for content that is accessed frequently, but changes infrequently. 
        * For example, a blog post that is updated once a day can be cached by a CDN.

    - **CDNs can be used to cache API responses**: If you have an API that is accessed frequently, you can use a CDN to cache the responses.

    - **Eviction policies**: Like other caches, CDNs have eviction policies that determine when cached content is removed.
        * You can set a time-to-live (TTL) for cached content, or you can use a cache invalidation mechanism to remove content from the cache when it changes.

- CloudFlare
- Amazon CloudFront
    - Caching, DDoS protection, and web application firewalls.

# Common Patterns

