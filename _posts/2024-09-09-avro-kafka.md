---
layout: post
title: "Simple Avro Schema Registry with Spring Boot"
author: "Leonardo Marques"
categories: software
tags: [kafka, java, api, docker]
image: avro-kafka.png
---

# Simple Avro Schema Registry with Spring Boot

|
[Avro](https://avro.apache.org/docs/1.11.1/getting-started-java/)
|
[Schema Registry](https://docs.confluent.io/platform/current/schema-registry/index.html)
|
[kafka](https://developer.confluent.io/courses/apache-kafka/events/)
|
[Spring Boot](https://developer.confluent.io/courses/spring/apache-kafka-intro/)
|

## Docker-Compose

```
version: '3.6'
services:
  zookeeper:
    image: confluentinc/cp-zookeeper:7.1.0
    platform: linux/amd64
    hostname: zookeeper
    container_name: zookeeper
    ports:
      - "2181:2181"
    environment:
      ZOOKEEPER_CLIENT_PORT: 2181
      ZOOKEEPER_TICK_TIME: 2000

  broker:
    image: confluentinc/cp-server:7.1.0
    platform: linux/amd64
    hostname: broker
    container_name: broker
    depends_on:
      - zookeeper
    ports:
      - "9092:9092"
      - "9101:9101"
    environment:
      KAFKA_BROKER_ID: 1
      KAFKA_ZOOKEEPER_CONNECT: 'zookeeper:2181'
      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: PLAINTEXT:PLAINTEXT,PLAINTEXT_HOST:PLAINTEXT
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://broker:29092,PLAINTEXT_HOST://localhost:9092
      KAFKA_METRIC_REPORTERS: io.confluent.metrics.reporter.ConfluentMetricsReporter
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
      KAFKA_GROUP_INITIAL_REBALANCE_DELAY_MS: 0
      KAFKA_CONFLUENT_LICENSE_TOPIC_REPLICATION_FACTOR: 1
      KAFKA_CONFLUENT_BALANCER_TOPIC_REPLICATION_FACTOR: 1
      KAFKA_TRANSACTION_STATE_LOG_MIN_ISR: 1
      KAFKA_TRANSACTION_STATE_LOG_REPLICATION_FACTOR: 1
      KAFKA_JMX_PORT: 9101
      KAFKA_JMX_HOSTNAME: localhost
      KAFKA_CONFLUENT_SCHEMA_REGISTRY_URL: http://schema-registry:8081
      CONFLUENT_METRICS_REPORTER_BOOTSTRAP_SERVERS: broker:29092
      CONFLUENT_METRICS_REPORTER_TOPIC_REPLICAS: 1
      CONFLUENT_METRICS_ENABLE: 'true'
      CONFLUENT_SUPPORT_CUSTOMER_ID: 'anonymous'

  schema-registry:
    image: confluentinc/cp-schema-registry:7.1.0
    platform: linux/amd64
    hostname: schema-registry
    container_name: schema-registry
    depends_on:
      - broker
    ports:
      - "8081:8081"
    environment:
      SCHEMA_REGISTRY_HOST_NAME: schema-registry
      SCHEMA_REGISTRY_KAFKASTORE_BOOTSTRAP_SERVERS: 'broker:29092'
      SCHEMA_REGISTRY_LISTENERS: http://0.0.0.0:8081
```

## pom.xml

```
<repositories>
		<repository>
			<id>confluent</id>
			<url>https://packages.confluent.io/maven/</url>
		</repository>
	</repositories>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.kafka</groupId>
			<artifactId>spring-kafka</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.kafka</groupId>
			<artifactId>spring-kafka-test</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.apache.avro</groupId>
			<artifactId>avro</artifactId>
			<version>1.11.1</version>
		</dependency>
		<!-- https://mvnrepository.com/artifact/io.confluent/kafka-avro-serializer -->
		<dependency>
			<groupId>io.confluent</groupId>
			<artifactId>kafka-avro-serializer</artifactId>
			<version>7.7.0</version>
		</dependency>
		<!-- https://mvnrepository.com/artifact/io.confluent/kafka-schema-registry-client -->
		<dependency>
			<groupId>io.confluent</groupId>
			<artifactId>kafka-schema-registry-client</artifactId>
			<version>7.7.0</version>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
			<plugin>
				<groupId>org.apache.avro</groupId>
				<artifactId>avro-maven-plugin</artifactId>
				<version>1.11.1</version>
				<executions>
					<execution>
						<phase>generate-sources</phase>
						<goals>
							<goal>schema</goal>
						</goals>
						<configuration>
							<sourceDirectory>${project.basedir}/src/main/resources/schemas/</sourceDirectory>
							<outputDirectory>${project.basedir}/src/main/java/</outputDirectory>
						</configuration>
					</execution>
				</executions>
			</plugin>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-compiler-plugin</artifactId>
				<configuration>
					<source>1.8</source>
					<target>1.8</target>
				</configuration>
			</plugin>
		</plugins>
	</build>
```

## Application.yaml

```
spring:
  application:
    name: AvroLearning

  kafka:
    bootstrap-servers:
      - "localhost:9092"
    producer:
      key-serializer: "org.apache.kafka.common.serialization.StringSerializer"
      value-serializer: "io.confluent.kafka.serializers.KafkaAvroSerializer"
      properties:
        schema:
          registry:
            url: "http://localhost:8081"

    consumer:
      group-id: "consumer-stock-history"
      key-deserializer: "org.apache.kafka.common.serialization.StringDeserializer"
      value-deserializer: "io.confluent.kafka.serializers.KafkaAvroDeserializer"
      autoOffsetRest: "earliest"
      properties:
        schema:
          registry:
            url: "http://localhost:8081"
        specific:
          avro:
            reader: "true"

avro:
  topic:
    name: "com.example.avro.v1"
```

## StockHistory.avsc
```
{
  "type": "record",
  "name": "StockHistory",
  "namespace": "com.example.avro.v1",
  "fields": [
    {
      "name": "tradeId",
      "type": "int",
      "default": 0
    },
    {
      "name": "tradeQuantity",
      "type": "int",
      "default": 0
    },
    {
      "name": "tradeMarket",
      "type": ["null", "string"],
      "default": null
    },
    {
      "name": "stockName",
      "type": ["null", "string"],
      "default": null
    },
    {
      "name": "tradeType",
      "type": ["null", "string"],
      "default": null
    },
    {
      "name": "price",
      "type": "float",
      "default": 0.0
    },
    {
      "name": "amount",
      "type": "float",
      "default": 0.0
    }
  ]
}
```

## KafkaAvroProducer

```java
@Service
public class KafkaAvroProducer {

    @Value("${avro.topic.name}")
    private String topicName;

    @Autowired
    private KafkaTemplate<String, StockHistory> kafkaTemplate;

    public void send(StockHistory stockHistory) {
        CompletableFuture<SendResult<String, StockHistory>> future =
                kafkaTemplate.send(topicName, String.valueOf(stockHistory.getTradeId()), stockHistory);

        future.thenAcceptAsync(
                result -> {
                    System.out.println("Avro message successfully produced");
                }
        ).exceptionallyAsync(
                err -> {
                    System.out.println("Message failed to produce");
                    return null;
                }
        );
    }
}
```

## StockHistoryModel

```java
public class StockHistoryModel {
    private int tradeQuantity;
    private String tradeMarket;
    private String stockName;
    private String tradeType;
    private float price;
    private float amount;

    // Constructor, Getter and Setter
```

## KafkaAvroController

```java
@RestController
public class KafkaAvroController {

    @Autowired
    private KafkaAvroProducer kafkaAvroProducer;

    @PostMapping("/sendStockHistory")
    public void sendStockHistory(@RequestBody StockHistoryModel model) {
        StockHistory stockHistory = StockHistory.newBuilder().build();
        stockHistory.setStockName(model.getStockName());
        stockHistory.setTradeType(model.getTradeType());
        stockHistory.setPrice(model.getPrice());
        stockHistory.setAmount(model.getAmount());
        stockHistory.setTradeId(new Random(1000).nextInt());
        stockHistory.setTradeMarket(model.getTradeMarket());
        stockHistory.setTradeQuantity(model.getTradeQuantity());

        kafkaAvroProducer.send(stockHistory);
    }
}
```

## KafkaAvroConsumer

```java
@Service
public class KafkaAvroConsumer {

    @KafkaListener(topics = "${avro.topic.name}", containerFactory = "kafkaListenerContainerFactory")
    public void read(ConsumerRecord<String, StockHistory> record) {
        String key = record.key();
        StockHistory history = record.value();

        System.out.println("Avro message for key: { "+ key +" }, value: { "+ history +" }");
    }
}
```

## kafkaConfig

```java
@Configuration
public class KafkaConfig {

    @Bean
    public ConcurrentKafkaListenerContainerFactory<String, StockHistory> kafkaListenerContainerFactory(KafkaProperties kafkaProperties) {
        ConcurrentKafkaListenerContainerFactory<String, StockHistory> factory = new ConcurrentKafkaListenerContainerFactory<>();
        factory.setConsumerFactory(defaultConsumerFactory(kafkaProperties));
        return factory;
    }

    private ConsumerFactory<String, StockHistory> defaultConsumerFactory(KafkaProperties kafkaProperties) {
        Map<String, Object> consumerProps = kafkaProperties.buildConsumerProperties(null);
        return new DefaultKafkaConsumerFactory<>(consumerProps);
    }
}
```

---

---> [Code Repository](https://github.com/Sukuna963/Avro_Schema_Registry)