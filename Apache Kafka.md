Apache Kafka
==============

- Distributed Streaming Platform
1. Creating real-time datastreams
2. Processing  "  "

realtime - milliseconds

Model: 
------
- Adopted Pub/Sub Messaging system architecture

Publisher --> [ Broker ] --> Subscriber

	Producer  -> 			 -> [ ConsumerA 
	Producer  -> 			 ->   ConsumerA2 ] Consumer GroupA
	Producer  -> [ Broker]   -> Consumer 
	Producer  -> 			 -> Consumer 
	Producer  -> 			 -> Consumer 

Note: Producers & Consumers are decoupled 


history:
--------
- Likedin - opensourced in 2011
- Started as DataItegration Solution
- But evolved to Streaming Platform


1. Server software - Kafka Broker
2. Client API - Kafka Java library
	a) Producer API
	b) Consumer API

+ 

1. Kafka Connect 
2. Kafka Streams
3. KSQL - licensed 


Terminologies
--------------

1. Producer 
	--> sends Message Record (for kafka it is array of bytes )
2. Consumer 
3. Broker
4. Cluster 
5. Topic
	--> Uniqe name for DataStream
6. Partitions
	--> we decide per topic
7. Offset
	--> sequnence id of message per partitioning
8. Consumer Groups
	--> group of consumers
	--> to share work loads
	--> they divide work
	--> ONE PARTITION only read by ONE CONSUMER at a time
		[ to avoid duplicate reads ]



To locate a message
--------------------
- Topic Name -> Partition Number -> Offset Number


Kafka Connect
=============
- kafka connect contains predefined code (just configure)


	DB --[ Kafka connect ] -- Kafka - [ Kafka connect ] -- hdfs

		  (src connector)				(sink connector)

Note: 
- [ Kafka connect ] can also be clustered

src connectors
--------------
Realtional Databases
Teradata
IOT Hubs
Salesforce
Twtitter
Reddit

sink connectors
---------------
File system
colud storage
Hadoop storage
Elastic Search
Cassandra
MongoDB
Google Firebase


what if i need custom connect ?
-------------------------------
 - Implement two Java classes

Kafka connect framework

a. Src Connector
	1. SourceConnector
	2. SourceTask
b. Sink Connector
	1. SinkConnector
	2. SinkTask




Do kafka connect allow Transformations ?
----------------------------------------
Yes, both at src and sink connectors

example:   
- add new fields
- filter/rename fields
- mask fieds with a null value
- change the record key
- route the record to different kafka topics


Kafka connect Architecture
==========================

Kafka connect runs 1 or more workers (called workgroup)

-start workers with same group id
-realiability
-loadbalance 

1. Worker 
	- works like container
2. Connector
	- connects
	- split mgmt
3. Task

what happens:
--------------
copy JDBC connector 
configure
decide degree of parallelism 
task connects to src send to worker


Kafka Streams
=============

what is stream data ?
--------------------
DataStreams  - no definite starting or ending
often infinite and ever growing
sequence of data in small packet

ex:
----

sensors
log entires
click streams
trasactions
data feeds


Kafak Streams
-------------
- Java/Scala Library
- Input must be kafka topic
- deploy anywhere
- out of box parallel processing , scalability and fault tolerance

kafka Streams offers
----------------------
- working with streams/tables
- Gouping and continuously updating aggregates
- Join streams, tables 
- windowing capability
- Flexible Time shemes 
	- Event time 
	- Processing time
	- Late comers
	- High watermark
	- Exctly-once processing etc
- Interactive Query - Serving other microservices
- Using testing tools

Kafka Streams architectute
==========================

		DataSource --> [ kafka cluster ]

					    - Topic-T1
					    	partition-1
					    	partition-2 
					    - Topic-T2
					    	partition-1
					    	partition-2
					    	partition-3


KSQL
====
SQL interface
Interactive Mode 
Headless Mode  -> for prod ENV



KSQL components
---------------

KSQL Server
	1. KSQL engine
	2. REST interface

3. KSQL Client (CLI/UI) 


KSQl allows you
---------------
select
windowing
group 
join two topics



Kafka installation
==================
1. Open Source 
2. Commercial Distribution - confluent.io
3. Managed Service - confluent,amazon,aiven.io












