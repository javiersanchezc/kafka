# kafka
repos de kafka
ruta de kafka 
https://drive.google.com/file/d/1KFMtGsOaU_sJwBFiScRZn-lmo9A8bgbl/view?usp=drive_link

extract the zip file
copy the properties files and place it in config folder in kafka extract
change the location in bat files as per your extracted kafka location



Make sure you are inside the bin/windows directory.

Start Zookeeper and Kafka Broker

 

Start up the Zookeeper.

zookeeper-server-start.bat ..\..\config\zookeeper.properties

 

Start up the Kafka Broker.

kafka-server-start.bat ..\..\config\server.properties

 

How to create a topic ?

kafka-topics.bat --create --topic test-topic -zookeeper localhost:2181 --replication-factor 1 --partitions 4

 

How to instantiate a Console Producer?

Without Key

kafka-console-producer.bat --broker-list localhost:9092 --topic test-topic

 

With Key

kafka-console-producer.bat --broker-list localhost:9092 --topic test-topic --property "key.separator=-" --property "parse.key=true"

 

How to instantiate a Console Consumer?

Without Key

kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test-topic --from-beginning

 

With Key

kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test-topic --from-beginning -property "key.separator= - " --property "print.key=true"

 

With Consumer Group

kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test-topic --group <group-name>


[martes 10:18 a. m.] Siva Sreenivasa Rao D

Make sure you are inside the bin/windows directory.

 

List the topics in a cluster

kafka-topics.bat --zookeeper localhost:2181 --list

 

Describe topic

The below command can be used to describe all the topics.

kafka-topics.bat --zookeeper localhost:2181 --describe

 

The below command can be used to describe a specific topic.

kafka-topics.bat --zookeeper localhost:2181 --describe --topic <topic-name>

 

Alter the min insync replica

kafka-topics.bat --alter --zookeeper localhost:2181 --topic library-events --config min.insync.replicas=2

 

Delete a topic

kafka-topics.bat --zookeeper localhost:2181 --delete --topic <topic-name>

 

How to view consumer groups

kafka-consumer-groups.bat --bootstrap-server localhost:9092 --list

 

Consumer Groups and their Offset

kafka-consumer-groups.bat --bootstrap-server localhost:9092 --describe --group console-consumer-27773

 

Viewing the Commit Log

kafka-run-class.bat kafka.tools.DumpLogSegments --deep-iteration --files /tmp/kafka-logs/test-topic-0/00000000000000000000.log



Setting Up Multiple Kafka Brokers

The first step is to add a new server.properties.

 

We need to modify three properties to start up a multi broker set up.

 

broker.id=<unique-broker-d>

listeners=PLAINTEXT://localhost:<unique-port>

log.dirs=/tmp/<unique-kafka-folder>

 

Example config will be like below.

broker.id=1

listeners=PLAINTEXT://localhost:9093

log.dirs=/tmp/kafka-logs-1

 

Starting up the new Broker

Provide the new server.properties thats added.

kafka-server-start.bat ..\..\config\server-1.properties

kafka-server-start.bat ..\..\config\server-2.properties


