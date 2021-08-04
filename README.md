# System Design for Web-Apps


## Working Components of Front-end Architecture

* Code
  * HTML5/WAI-ARIA
  * CSS/Sass Code standards and organization
  * Object-Oriented approach (how do objects break down and get put together)
  * JS frameworks/organization/performance optimization techniques
  * Asset Delivery - Front-end Ops
* Documentation
  * Onboarding Docs
  * Styleguide/Pattern Library
  * Architecture Diagrams (code flow, tool chain)
* Testing
  * Performance Testing
  * Visual Regression
  * Unit Testing
  * End-to-End Testing
* Process
  * Git Workflow
  * Dependency Management (npm, Bundler, Bower)
  * Build Systems (Grunt/Gulp)
  * Deploy Process
  * Continuous Integration (Travis CI, Jenkins)

## Web App System design considerations:

* Security (CORS)
* Using CDN
	* A content delivery network (CDN) is a system of distributed servers (network) that deliver webpages and other Web content to a user based on the geographic locations of the user, the origin of the webpage and a content delivery server.
	* This service is effective in speeding the delivery of content of websites with high traffic and websites that have global reach. The closer the CDN server is to the user geographically, the faster the content will be delivered to the user. 
	* CDNs also provide protection from large surges in traffic.
* Full Text Search
	* Using Sphinx/Lucene/Solr - which achieve fast search responses because, instead of searching the text directly, it searches an index instead.
* Offline support/Progressive enhancement
	* Service Workers
* Web Workers
* Server Side rendering
* Asynchronous loading of assets (Lazy load items)
* Minimizing network requests (Http2 + bundling/sprites etc)
* Developer productivity/Tooling
* Accessibility
* Internationalization
* Responsive design
* Browser compatibility



## Distributed Systems & Its 3 Principles

Any system which includes multiple components residing on multiple machines coordinating through some sort of mechanism like sending messages to achieve a common goal is a distributed system.

* Single responsibility principle

Each component present in System Design should have a single job to perform.

![image](https://user-images.githubusercontent.com/11299574/128066955-b91a4b63-7799-41a4-97a3-d8d190927d67.png)

 
* No single point of failure principle

The system should never have any component whose failure will result in the failure of the entire system.

![image](https://user-images.githubusercontent.com/11299574/128066991-5b0d72cc-76d9-4282-a212-f5bed865cde5.png)

 
* No bottleneck principle

Since we design for scalability our system should not have performance bottlenecks. 
Ideally we should horizontally scale our system to handle the large amounts of processing.

![image](https://user-images.githubusercontent.com/11299574/128067041-6ba354c3-4772-42db-8089-3649d6c39083.png)




## Guide for System Design

1. Requirement analysis
– Here we first discuss the functional requirements i.e. what this system should do. Then we discuss the non-functional requirements i.e. how the system should behave.
2. API design – Here we define the interfaces we expose to the outside world using which the communication happens. Here we have to define the name of the apis, the parameters it takes and the return values.
3. Define data model – It is a representation of object data, its association between different objects and the rules it should follow.
4. High level design – This depicts the required component blocks with arrows showing the data flow. The components can be load balancers, web servers, application servers, databases, caches or custom components performing some action like filtering, reading, processing , etc. The high level design shows how the data flows from an entry point to a database and vice versa.
5. Scale the design – This is necessary because today’s systems are generally large scale distributed systems. To process large data we need to add multiple machines since it is difficult or rather impossible for one single machine to do everything. You need to find all the bottlenecks and fix them.


## Concepts and Components 

### 1. Scaling

Large enterprises have large amounts of data. With increasing amounts of data the system should also grow to manage it effectively. This process of growing or shrinking of the system to handle data is called scaling.

Scaling of any system can be achieved by two ways.

#### Vertical Scaling : 
Vertical scaling means upgrading the hardware/software of the existing system. Adding more power to it more RAM, CPU’s and HDD. But with vertical scaling there is always a limit a max beyond which it cannot go higher.

#### Horizontal Scaling :
Horizontal scaling means adding multiple additional systems to improve the performance. Typically we might use several low end commodity hardware to save the cost.

These are some differences between them.

#### Horizontal Scaling

* Might need load balancers
* Resilient to system failures
* Data inconsistency
* Scales well 

#### Vertical Scaling

* Load balancer is not necessary
* Single point of failures
* Data consistency
* Has hardware limit for scaling


![image](https://user-images.githubusercontent.com/11299574/128064677-17203c0a-c37e-48de-88c5-2b0865ec9228.png)


### 2. Load Balancing

Load balancer helps distribute incoming traffic across servers or databases. 

There are 2 types of load balancers hardware and software. Hardware load balancers are generally expensive but very effective. 

You can use multiple load balancers to avoid single point of failure. They can be in active-active mode or active-passive mode.

Following algorithms are largely used for load balancing purpose.

* Round Robin 
* Least Loaded
* Session Based
* Hashing

![image](https://user-images.githubusercontent.com/11299574/128064760-3cb9473c-93d0-45e6-9b9d-a5de447d4911.png)

![image](https://user-images.githubusercontent.com/11299574/128064814-0046e8fb-950f-4930-a6c3-b056e241f0f6.png)

![image](https://user-images.githubusercontent.com/11299574/128064842-84353ee3-f75f-468e-adaf-811e9b0aed5f.png)


### 3. Caching

Caching is a concept where data is stored in fast memory for quick access. The cache is generally a temporary storage like RAM since it is faster than reading the data from HDD or a database.

There is a famous 80:20 rule which states that 20% of the data is accessed almost 80% of the time. So generally we try to keep that 20% data in the cache.

#### Cache Invalidation 

* Write-through cache: Data is written in cache and database at the same time.
* Write-around cache: Data is written in database only. Cache is marked as invalid. It is written later in cache.
* Write-back cache: Data is written in cache only. It is written later in db.

![image](https://user-images.githubusercontent.com/11299574/128065045-d69782c6-3dc6-4074-b31d-1b2e3b90038b.png)


#### Cache Eviction

* Least Recently Used (LRU)
* Most Recently Used (MRU)
* First In First Out (FIFO)
* Last In First Out (LIFO)
* Least Frequently Used (LFU)
* Random Replacement (RR)

![image](https://user-images.githubusercontent.com/11299574/128065084-6ce8880b-1c49-429f-8d4c-8a05079f4e87.png)

![image](https://user-images.githubusercontent.com/11299574/128065102-af84b434-d177-472f-a967-e8e651d6c6b5.png)

* Distributed Caching 

![image](https://user-images.githubusercontent.com/11299574/128065250-f6c3049b-7def-407a-aa50-20e61ef0974a.png)


### 4. Consistent Hashing

Consistent hashing is one of the techniques used to bake in scalability into the storage architecture of your system. 

In a distributed system, consistent hashing helps in solving following scenarios:

* To Provide elastic scaling (a term used to describe synamic adding/removing of servers based on usage load) for cache servers.
* Scale out a set of storage nodes like NoSQL databases.

### 5. Storage

#### Object Store

Object store or object-based storage is a storage architecture which manages data as objects unlike your regular hard disks which manages it as files in a file hierarchy system.

#### RAID

Redundant array of independent disks (RAID) is a way of storing the same data on multiple hard disks or solid state drives to protect it in case of failures. There is a RAID controller which handles all the operations and is responsible for improving performance while writing and protecting the data on multiple devices.

#### RAID Levels

RAID levels are nothing but different configurations. There are 6 standard levels of RAID from RAID 0 to RAID 5, then there are several combined RAID levels like RAID 10 and many non standard RAID levels which companies have developed for their own use. For the purpose of this section we will go through RAID 0 to RAID 5 and a combination RAID 10. These are good to know topics for design interview. You can ignore the other RAID levels safely.

* RAID 0 – Striping

![image](https://user-images.githubusercontent.com/11299574/128065290-f9f1b4c4-8eae-4925-9e33-c01cad07db53.png)

* RAID 1 – Mirroring

![image](https://user-images.githubusercontent.com/11299574/128065321-1f1a95c9-4789-442a-88ce-fac1381e95ee.png)

* RAID 2 – Bit-level striping with dedicated Hamming-code parity 

![image](https://user-images.githubusercontent.com/11299574/128065348-187a37ab-263f-477b-951c-00cad4ae359a.png)

* RAID 3 – Byte-level striping with a single parity disk

![image](https://user-images.githubusercontent.com/11299574/128065365-27317db2-4d7e-4987-8782-f71cfecb8fa1.png)

* RAID 4 – Block-level striping with a single parity disk 

![image](https://user-images.githubusercontent.com/11299574/128065388-d0e2b2d4-f525-4b4d-a938-4e36894cd9b7.png)

* RAID 5 – Striping with distributed parity

![image](https://user-images.githubusercontent.com/11299574/128065411-66e22a6c-3bf2-46b6-8deb-6d6094ae1a97.png)

* RAID 6 – Striping with double parity

![image](https://user-images.githubusercontent.com/11299574/128065429-bce5dd8d-2557-4736-9220-18e76311c4d2.png)

* RAID 10 – Combining striping and mirroring

![image](https://user-images.githubusercontent.com/11299574/128065470-3659ccbe-e97a-42ed-aa86-3436ee488ac8.png)



### 6. Database Concepts

A database is a collection of information that is organized so that it can be easily accessed, managed and updated. In this section you will get to know about various database concepts like CAP theorem, ACID properties, Consistency patterns and Sharding.

3 guarantees of a distributed system

* Consistency — A guarantee that every node in a distributed cluster returns the same, most recent, successful write.
* Availability — Every non-failing node returns a response for all read and write requests in a reasonable amount of time
* Partition Tolerant — The system continues to function in spite of network partitions. 

![image](https://user-images.githubusercontent.com/11299574/128065514-48e2a78f-58b8-4f40-831a-447f57214b29.png)


#### CAP theorem

CAP theorem states that it is impossible for a distributed software system to simultaneously provide more than two out of three of the following guarantees (CAP): Consistency, Availability, and Partition tolerance. While designing a distributed system we can pick up only 2 of the 3 options.

CAP theorem is one of the parameters used when choosing the database for your system.

![image](https://user-images.githubusercontent.com/11299574/128065535-d27c9185-0978-410d-b775-fa10d7024465.png)


#### ACID Properties

* Atomicity
* Consistency
* Isolation
* Durability

We know that a transaction is a single logical unit of work consisting of one or more instructions which accesses and possibly modifies the contents of a database. To maintain integrity of the database each transaction should be ACID compliant.

#### Database Replication

Database replication is the process of copying data from one database to one or more databases.

#### Consistency Patterns

Distributed databases that rely on replication for high availability, low latency or both, we need to make a trade-off between the read consistency vs throughput. There are 2 general consistency levels supported by most distributed databases. 

* Strong consistency
* Eventual consistency

#### Replication architectures

Single-leader architecture
Multi-leader architecture
No-leader architecture

![image](https://user-images.githubusercontent.com/11299574/128065634-377c71cf-2c2f-4332-8798-dee269575f79.png)


#### Sharding

Sharding a database is horizontal partitioning a database. 

##### Factors to be considered while sharding

* Data size
* Performance
* Latency
* Cost

##### Ways to shard the data

* Divide based on some column value
* Divide based on some algorithm or hash function
* Consistent hashing

![image](https://user-images.githubusercontent.com/11299574/128065650-884973ff-dea4-469a-b0c2-d3fe8f776212.png)


#### NoSQL and it’s types

A NoSQL database provides a mechanism for storage and retrieval of data that is modeled in means other than the tabular relations used in relational databases.

There are 4 main Nosql types

1. Key-value store

As the name suggests the data is saved into a key value pair. Some of the most famous in this category are Redis, Amazon’s Dynamo and Voldemort.

2. Column oriented database

Traditional databases are row oriented. All the columns of a row are stored together. A column-oriented stores data tables by column rather than by row. Some of the famous column oriented databases are Cassandra and HBase.

3. Document-based

Here we save the data into a form of documents. These documents should have some schema either fixed or unfixed and it can be expressed in json format. Some examples are MongoDB and CouchDB.

4. Graph-based

When the data is highly interconnected and it can be depicted as nodes and edges we can use graph based databases. The nodes can be entities and the edges can be relationships. An example of a graph based database is Neo4j.


### 7. Web Servers

* A web server is a dedicated server whose functionality is to serve web requests only.
* It serves HTML documents, images, CSS stylesheets, and JavaScript files.

### 8. Application servers

* An application server or app server is used to host applications. 
* These applications generally are the business logic of the system.
* An app server provides the environment both software and hardware to run them. 

### 9. Architectural patterns

1. Monolithic

In monolithic pattern the entire business logic is composed in one single component.

2. Layered

![image](https://user-images.githubusercontent.com/11299574/128063314-a77970ab-f42d-4702-be88-6868e508d108.png)

In the layered pattern the components are grouped into logical layers. Each request will go through the layers performing some specific tasks.

3. SOA – Service oriented architecture

![image](https://user-images.githubusercontent.com/11299574/128063248-9f0729e8-614f-4896-930c-cacd75a4e841.png)

SOA defines a way of making components reusable via service interfaces. In this pattern each component is actually a service performing some specific functionality.

4. Microservices architecture

![image](https://user-images.githubusercontent.com/11299574/128063274-3bfc9b7b-a4a2-43f0-a7e8-3a1a97a337a0.png)

Microservices architecture is a style which allows building an application as a collection of small independent services. Each independent service is called a microservice.

Some features of microservice are

* Highly maintainable and testable
* Loosely coupled
* Independently deployable
* Organized around business capabilities i.e. Single responsibility principle
* Owned by a small team

Most microservices based systems have some common components.

* API gateway
* Service discovery
* Service management

### 10. Message queues

![image](https://user-images.githubusercontent.com/11299574/128063523-e8c598fd-3592-4c55-8a0e-b44320307d8a.png)

Message queues are typically used to provide asynchronous communication between components in a system. 
We can divide the message queue into parts where each part serves a specific purpose. Messages belonging to some particular category can go into its respective part. 
Some examples of the products which provide message queues are Kafka, RabbitMQ and Azure service bus.

### 11. Communication models and Protocols

#### Communication models

* Push
Here sender actively sends the messages to receiver whenever a message is available.
* Pull
Here the receiver asks sender if a message is present. If it is present it pulls the message.

#### Communication Protocols

* Http

![image](https://user-images.githubusercontent.com/11299574/128063728-9e3a888f-145a-4fe2-a568-59d5e89fb45f.png)

* Long polling

![image](https://user-images.githubusercontent.com/11299574/128063775-ea0171d7-0948-44fc-9b5b-20332454db08.png)

* Websockets

![image](https://user-images.githubusercontent.com/11299574/128063835-50f84831-9593-4154-a428-0cf5634bac53.png)

### 12. Security

Basic concepts

* Authentication
* Authorization
* Encryption
* Integrity
* Symmetric encryption
* Asymmetric encryption
* Certificate
* Certification Authority(CA)
* Cross-Site Scripting(XSS)
* Denial of Service(DoS)
* Distributed Denial of Service(DDoS)

### 13. Content delivery network (CDN)

A content delivery network (CDN) refers to a geographically distributed group of servers which work together to provide fast delivery of Internet content.

### 14. Back-of-the-envelope calculations

Back-of-the-envelop estimations means the quick calculations you do on back of the envelop or on paper.

Question:

Estimate how many servers we need to serve read requests considering each server is capable of handling 7 requests per second. We have to serve a total traffic of 46 Million per day.

Answer: 
```
7 requests per second
7*60 = 420 requests per minute
420*60 requests per hour = 400 * 60 = 24000 per hour = 24K per hour
24K * 24 requests per day ≈ 30K*20 = 600K requests per day per server
We want to handle 46 Million requests per day which means 46M/600K = approx 45M/500K = 45M/0.5M = 45*2 = 90 servers.
```

Question:

Given 46 servers and 46 Million requests per day how much data does each server process per second?

Answer:
```
So 1 server will have 1 Million requests per day.
1 server will have 1 Million/24 requests per hour = 1000000/24 = 1000K/24 ≈ 1000K/25 = 40K requests per hour.
1 server will have 40K/60 requests per minute = 4K/6 = 4000/6 = 3600/6 = 600 requests per minute.
1 server will have 600/60 requests per second = 60/6 = 10 requests per second.
```

#### Cheat sheet

```
1 Bit
1 Byte = 8 bits
1 Kilobyte (KB) = 1024 Bytes ≈ 1000 Bytes
1 Megabyte (MB) = 1024 KB ≈ 1000 KB
1 Gigabyte (GB) = 1024 MB ≈ 1000 MB
1 Terabyte (TB) = 1024 GB ≈ 1000 GB
1 Petabyte (PB) = 1024 TB ≈ 1000 TB
1 Exabyte (EB) = 1024 PB ≈ 1000 PB
Kb vs KB: Serial communications and read/write devices use Kb (Kilo-bits) for data transfer ratings whereas storage devices use KB (Kilo-Byte) to rate their capacity.

1 KB(kilobyte) = 1024 bytes = 1024 * 8 bits = 8196 bits

1 Kb(kilobits) = 1024 bits = 1024/8 bytes = 128 bytes.
```


## Key questions to be known before designing a system

1) **Concurrency** 
* Do you understand threads, deadlock, and starvation? Do you know how to parallelize algorithms? Do you understand consistency and coherence?

2) **Networking**
* Do you roughly understand IPC and TCP/IP? Do you know the difference between throughput and latency, and when each is the relevant factor?

3) **Abstraction**
* You should understand the systems you’re building upon. Do you know roughly how an OS, file system, and database work? Do you know about the various levels of caching in a modern OS?

4) **Real-World Performance**
* You should be familiar with the speed of everything your computer can do, including the relative performance of RAM, disk, SSD and your network.

5) **Estimation**
* Estimation, especially in the form of a back-of-the-envelope calculation, is important because it helps you narrow down the list of possible solutions to only the ones that are feasible. Then you have only a few prototypes or micro-benchmarks to write.	

6) **Availability & Reliability**
*  Are you thinking about how things can fail, especially in a distributed environment? Do know how to design a system to cope with network failures? Do you understand durability?
