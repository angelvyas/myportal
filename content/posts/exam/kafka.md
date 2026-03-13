---
title: 'practise'
date: 2025-12-09
draft:  true
featured: false  
description: "networks"
thumbnail: "/posts/exam/images/smile.png"
featureImage: "/posts/exam/images/smile.png" 
shareImage: "/posts/exam/images/smile.png"
author: "Angel Vyas"
tags:
    - general
categories:     
    - general
---

kafka in wsl home folder</br>
cd ~/kafka_2.13-3.8.0</br>
bin/zookeeper-server-start.sh config/zookeeper.properties</br>
bin/kafka-server-start.sh config/server.properties</br>
nano ~/kafka_2.13-3.8.0/config/server.properties</br>
# Listen on all network interfaces</br>
listeners=PLAINTEXT://0.0.0.0:9092</br>

# Advertise WSL IP so Windows IntelliJ can connect
advertised.listeners=PLAINTEXT://<WSL-IP>:9092</br>
hostname -I</br>
cd ~/kafka_2.13-3.8.0</br>
bin/kafka-server-start.sh config/server.properties</br>
bin/kafka-console-producer.sh --topic test-topic --bootstrap-server <WSL-IP>:9092</br>


props.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, "172.22.144.1:9092");</br>

### INTELLIJ CODE

package org.example;

import org.apache.kafka.clients.consumer.ConsumerConfig;
import org.apache.kafka.clients.consumer.ConsumerRecord;
import org.apache.kafka.clients.consumer.ConsumerRecords;
import org.apache.kafka.clients.consumer.KafkaConsumer;

import java.time.Duration;
import java.util.Collections;
import java.util.Properties;

public class Main {

    public static void main(String[] args) {

        // Kafka consumer configuration
        Properties props = new Properties();
        props.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, "172.20.191.167:9092");

        // Use a unique consumer group to always read from beginning
        props.put(ConsumerConfig.GROUP_ID_CONFIG, "my-group-" + System.currentTimeMillis());

        props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringDeserializer");
        props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringDeserializer");
        props.put(ConsumerConfig.AUTO_OFFSET_RESET_CONFIG, "earliest");

        // Create consumer
        KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);

        // Subscribe to a topic
        consumer.subscribe(Collections.singletonList("test-topic"));

        System.out.println("Kafka Consumer started. Waiting for messages...");

        // Add shutdown hook to close consumer gracefully
        Runtime.getRuntime().addShutdownHook(new Thread(() -> {
            System.out.println("Closing consumer...");
            consumer.close();
        }));

        // Poll loop
        while (true) {
            ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(1000));
            for (ConsumerRecord<String, String> record : records) {
                System.out.println("Received: " + record.value() +
                        " | Partition: " + record.partition() +
                        " | Offset: " + record.offset());
            }
        }
    }
}



### pom.xml

### "<project xmlns="http://maven.apache.org/POM/4.0.0""""
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>kafka_consumer</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.apache.kafka</groupId>
            <artifactId>kafka-clients</artifactId>
            <version>3.5.1</version>
        </dependency>
    </dependencies>

</project>


## 1	Installation of kafka on windows and running the kafka server and zookeeper.Creating a topic
installation on ubuntu

```bash
cd ~
wget https://downloads.apache.org/kafka/3.8.0/kafka_2.13-3.8.0.tgz
tar -xvzf kafka_2.13-3.8.0.tgz
cd kafka_2.13-3.8.0
```
start zookeeper
```
bin/zookeeper-server-start.sh config/zookeeper.properties
```
start kafka server
```
bin/kafka-server-start.sh config/server.properties

creating a topic
```
cd ~/kafka_2.13-3.8.0
bin/kafka-topics.sh --create --topic demo --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
```

check that topic exists
```
bin/kafka-topics.sh --list --bootstrap-server localhost:9092
```