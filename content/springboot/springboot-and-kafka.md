---
title: "Springboot and Kafka"
date: 2024-02-03T08:33:43+05:30
draft: false
tags:
  - springboot
  - kafka
---

As part of this article, we will see how to integrate Kafka with Springboot. You should at least know basics of Springboot and Kafka concepts.

Let's start with what is kafka.

> Kafka is event streaming platform. It is used for building real-time data pipelines and streaming applications. It is horizontally scalable, fault-tolerant, and extremely fast. It is used for building real-time data pipelines and streaming applications. It is horizontally scalable, fault-tolerant, and extremely fast.

## Setting up Kafka

There are two parts in setting up Kafka one is setting up Producer and other is setting up Consumer.

### Setting up Producer

To set up producer, you need to have Kafka installed. You can download Kafka from [here](https://kafka.apache.org/downloads).
After doing this you need to add dependency in your 'build.gradle' file.

```groovy
implementation 'org.springframework.kafka:spring-kafka'
```

After adding this dependency, you need to add configuration in your 'application.properties' file.

```properties
spring.kafka.producer.bootstrap-servers=localhost:9092
```
After this you need to create a producer class.

```kotlin
import org.springframework.kafka.core.KafkaTemplate
import org.springframework.stereotype.Service

@Service
class Producer(val kafkaTemplate: KafkaTemplate<String, String>) {

    fun sendMessage(message: String) {
        kafkaTemplate.send("test", message)
    }
}
```

### Setting up Consumer

To set up consumer, you need to have following configuration in your 'application.properties' file.

```properties
spring.kafka.consumer.bootstrap-servers=localhost:9092
spring.kafka.consumer.group-id=group_id
```

After this you need to create a consumer class.

```kotlin
import org.springframework.kafka.annotation.KafkaListener
import org.springframework.stereotype.Service

@Service
class Consumer {

    @KafkaListener(topics = ["test"], groupId = "group_id")
    fun consume(message: String) {
        println("Consumed message: $message")
    }
}
```

Above example can further be optimized by moving the topic and group id to 'application.yaml' file.

```yaml
kafka:
  topic: test
  group-id: group_id
```

And using these we can modify the consumer class.

```kotlin
import org.springframework.beans.factory.annotation.Value
import org.springframework.kafka.annotation.KafkaListener
import org.springframework.stereotype.Service

@Service
class Consumer(@Value("\${kafka.topic}") val topic: String, @Value("\${kafka.group-id}") val groupId: String) {

    @KafkaListener(topics = ["\${kafka.topic}"], groupId = "\${kafka.group-id}")
    fun consume(message: String) {
        println("Consumed message: $message")
    }
}
```
