# Instructions on Starting Kafka

1. Create *zookeeper-logs* directory (`mkdir zookeeper-logs`)
2. Modify `config/zookeeper.properties` *dataDir* to point to `zookeeper-logs` (full path)
3. Run Zookeeper  
	Unix: `/bin/zookeeper-server-start.sh kafka/config/zookeeper.properties`
	Windows: `/bin/windows/zookeeper-server-start.bat config/zookeeper.properties`
    
4. Create 3 directories, one for each Kafka broker logs: 
`mkdir kafka-logs-0` 
`mkdir kafka-logs-1` 
`mkdir kafka-logs-2` 
5. Create 2 copies of  `config/server.properties` and name them `config/server-1.properties` and `config/server-2.properties`. Rename the original `config/server.properties` to `config/server-0.properties`. 
6. Change each configuration file's *log.dirs* to point to the corresponding `kafka-logs-X` directory.
7. In  `server-1.properties` uncomment the `#listeners=PLAINTEXT://:9092` and change the port to `9093`
8. In  `server-2.properties` uncomment the `#listeners=PLAINTEXT://:9092` and change the port to `9094`
9. Run 3 Kafka brokers pointing to the corresponding properties files:
Unix: 
`bin/kafka-server-start.sh /config/server-0.properties &`
`bin/kafka-server-start.sh /config/server-1.properties &`
`bin/kafka-server-start.sh /config/server-2.properties &`
Windows: 
`bin/windows/kafka-server-start.bat /config/server-0.properties &`
`bin/windows/kafka-server-start.bat /config/server-1.properties &`
`bin/windows/kafka-server-start.bat /config/server-2.properties &`
10. Create ***valid-transactions*** Kafka topic: `bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 3 --partitions 3 --topic valid-transactions`
11. Create **suspicious-transactions** Kafka topic: `bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 3 --partitions 2 --topic suspicious-transactions`
