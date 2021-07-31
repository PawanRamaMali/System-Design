# Pragmatic-Systems-Design-for-Web-Apps



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

### 2. Load Balancing

Load balancer helps distribute incoming traffic across servers or databases. 

There are 2 types of load balancers hardware and software. Hardware load balancers are generally expensive but very effective. 

You can use multiple load balancers to avoid single point of failure. They can be in active-active mode or active-passive mode.

Following algorithms are largely used for load balancing purpose.

* Round Robin 
* Least Loaded
* Session Based
* Hashing


### 3. Caching

Caching is a concept where data is stored in fast memory for quick access. The cache is generally a temporary storage like RAM since it is faster than reading the data from HDD or a database.

There is a famous 80:20 rule which states that 20% of the data is accessed almost 80% of the time. So generally we try to keep that 20% data in the cache.

#### Cache Invalidation 

* Write-through cache: Data is written in cache and database at the same time.
* Write-around cache: Data is written in database only. Cache is marked as invalid. It is written later in cache.
* Write-back cache: Data is written in cache only. It is written later in db.


#### Cache Eviction

* Least Recently Used (LRU)
* Most Recently Used (MRU)
* First In First Out (FIFO)
* Last In First Out (LIFO)
* Least Frequently Used (LFU)
* Random Replacement (RR)