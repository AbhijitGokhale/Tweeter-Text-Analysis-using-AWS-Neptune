# Tweeter-Text-Analysis-using-AWS-Neptune
Graphs can represent the interrelationships of real-world entities in many ways, in terms of actions, ownership, parentage, purchase choices, personal connections, family ties, and so on.

**Project Demo Video:** https://video.syr.edu/media/t/1_n773smyp

## Why Graph?
* Graph databases are optimized to store and query the relationships between data items.*
* They store data items as vertices of the graph, and the relationships between them as edges. Each edge has a type and is directed from one vertex (the start) to another (the end). Relationships can be called predicates as well as edges, and vertices are also sometimes referred to as nodes. In so-called property graphs, both vertices and edges can have additional properties associated with them too.*

![image](https://user-images.githubusercontent.com/84480824/206961686-6addc8e9-0d40-4352-a7db-d393898c690d.png)

* The edges are shown as named arrows, and the vertices represent specific people and hobbies that they connect.
* A simple traversal of this graph can tell you what Justin's friends like.
* Graphs can represent the interrelationships of real-world entities in many ways, in terms of actions, ownership, parentage, purchase choices, personal connections, family ties, and so on.

## AWS Neptune:
* Amazon Neptune is a fast, reliable, fully managed graph database service that makes it easy to build and run applications that work with highly connected datasets.
* The core of Neptune is a purpose-built, high-performance graph database engine. This engine is optimized for storing billions of relationships and querying the graph with milliseconds latency.
* Neptune supports the popular graph query languages Apache TinkerPop Gremlin, the W3C’s SPARQL, and Neo4j's open Cypher, enabling you to build queries that efficiently navigate highly connected datasets.
* Neptune powers graph use cases such as recommendation engines, fraud detection, knowledge graphs, drug discovery, and network security. 

## Key Features
* High performance and Scalability
* High Availability and Durability
* Query Support - Apache TinkerPop Gremlin, the W3C’s SPARQL, and Neo4j's open Cypher
* Highly Secure
* Fully Managed
* Fast Parallel Bulk Data Loading
* Cost Effectiveness - Pay only for what you use 

## Architecture

![image](https://user-images.githubusercontent.com/84480824/206962202-0e99413c-e9e0-4d29-8c2d-706d41145c6e.png)

* Fault Tolerance is achieved by replicating data 6 times across 3 availability zones. One instance acts as the master. Therefore, it is an ACID model with immediate consistency. We can replicate data up to 15 times.
• Data is stored using Lock-free optimistic algorithm. Data is considered durable when at least 4/6 copies acknowledge the write. For read, it uses 3/6 quorum model.
• Storage is self-healing storage that uses peer-to-peer replication. Storage is striped across 100s of volumes with each being 10GB. The storage is a log-structured distributed storage layer and it passes incremental log records from compute layer to storage layer.
• Data is continuously backed up to S3 in real time, using storage nodes. Maximum retention period is of 35 days. Neptune also uploads logs to S3 every 5 minutes.
• Compute nodes on replicas do not need to write. This provides improved read performance.

![image](https://user-images.githubusercontent.com/84480824/206962298-f500c965-9047-496a-a004-61f35c5f4f35.png)

• It has a cluster end point for writing data to the cluster and reader endpoint for reading data from the cluster.
• As any replicas are added or removed, the reader end point is kept up to date.
• All nodes share a storage volume that is auto scalable.
• In case of a failover, a replica is automatically promoted to be the new master. Failover to a replica typically takes about 30-120 seconds.

## Example Use Cases

* **Knowledge graphs** – Knowledge graphs let us organize and query all kinds of connected information to answer general questions. Using a knowledge graph, we can add topical information to product catalogs, and model diverse information such as is contained in Wikidata.

* **Identity graphs** – In a graph database, we can store relationships between information categories such as customer interests, friends, and purchase history, and then query that data to make recommendations which are personalized and relevant. For example, we can use a graph database to make product recommendations to a user based on which products are purchased by others who follow the same sport and have a similar purchase history. Or we can identify people who have a friend in common but don’t yet know each other and make a friendship recommendation. Graphs of this kind are known as identity graphs and are widely used for personalizing interactions with users.

* **Fraud graphs** – This is a common use for graph databases. They can help us track credit card purchases and purchase locations to detect uncharacteristic use, or to detect if a purchaser is trying to use the same email address and credit card as was used in a known fraud case. They can let us check for multiple people associated with a personal email address, or multiple people in different physical locations who share the same IP address. Consider the following graph. It shows the relationship of three people and their identity-related information. Each person has an address, a bank account, and a social security number. However, we can see that Matt and Justin share the same social security number, which is irregular and indicates possible fraud by one of them. A query to a fraud graph can reveal connections of this kind so that they can be reviewed.

* **Scientific research** – With a graph database, you can build applications that store and navigate scientific data and even sensitive medical information using encryption at rest. For example, you can store models of disease and gene interactions. You can search for graph patterns within protein pathways to find other genes that might be associated with a disease. You can model chemical compounds as a graph and query for patterns in molecular structures. You can correlate patient data from medical records in different systems. You can topically organize research publications to find relevant information quickly. 

* **Regulatory rules** – You can store complex regulatory requirements as graphs, and query them to detect situations where they might apply to your day-to-day business operations. 

* **Network topology and events** – A graph database can help us manage and protect an IT network. When we store the network topology as a graph, we can also store and process many kinds of events on the network. We can answer questions such as how many hosts are running a given application. We can query for patterns that might show that a given host has been compromised by a malicious program, and query for connection data that can help trace the program to the original host that downloaded it.
