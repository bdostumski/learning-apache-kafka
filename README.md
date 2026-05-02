<div align="center">

# 🚀 Learning Apache Kafka

<img src="https://upload.wikimedia.org/wikipedia/commons/0/05/Apache_kafka.svg" alt="Apache Kafka Logo" width="120"/>

> A hands-on Spring Boot project for learning **Apache Kafka** — covering producers, consumers, custom serialization, and REST-based message publishing.

[![Java](https://img.shields.io/badge/Java-17-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)](https://www.java.com)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.0.3-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)](https://spring.io/projects/spring-boot)
[![Apache Kafka](https://img.shields.io/badge/Apache%20Kafka-3.0.3-231F20?style=for-the-badge&logo=apache-kafka&logoColor=white)](https://kafka.apache.org/)
[![Maven](https://img.shields.io/badge/Maven-Build-C71A36?style=for-the-badge&logo=apache-maven&logoColor=white)](https://maven.apache.org/)

</div>

---

## 📖 About

This project is a practical learning resource for integrating **Apache Kafka** with **Spring Boot**. It demonstrates how to configure a Kafka producer and consumer from scratch, serialize/deserialize custom Java objects using JSON, and expose a REST API to publish messages to a Kafka topic.

---

## ✨ Features

- ⚙️ **Custom Kafka Producer** — Configured with `KafkaTemplate` and `JsonSerializer` for sending custom `Message` objects
- 👂 **Kafka Consumer / Listener** — Uses `@KafkaListener` with `ConcurrentKafkaListenerContainerFactory` to consume messages from a topic
- 🔄 **JSON Serialization** — Custom objects serialized/deserialized using Spring Kafka's `JsonSerializer` & `JsonDeserializer`
- 🌐 **REST API** — `POST /api/v1/messages` endpoint to publish messages to the `syscomz` Kafka topic
- 🏃 **CommandLineRunner** — On startup, automatically sends 100 test messages to Kafka to verify the setup
- 🔧 **Trusted Package Configuration** — Consumer factory explicitly trusts `com.syscomz` for safe deserialization

---

## 🗂️ Project Structure

```
learning-apache-kafka/
├── src/
│   └── main/
│       ├── java/com/syscomz/
│       │   ├── KafkaApplication.java        # Entry point + CommandLineRunner (sends 100 messages on startup)
│       │   ├── KafkaListeners.java          # @KafkaListener consumer for the "syscomz" topic
│       │   ├── Message.java                 # Custom message record/model
│       │   ├── MessageController.java       # REST controller — POST /api/v1/messages
│       │   ├── MessageRequest.java          # Request DTO
│       │   └── config/
│       │       ├── KafkaProducerConfig.java # Producer factory + KafkaTemplate bean
│       │       └── KafkaConsumerConfig.java # Consumer factory + listener container factory
│       └── resources/
│           └── application.properties       # Kafka bootstrap server config
├── pom.xml
└── README.md
```

---

## 🛠️ Tech Stack

| Technology | Version | Purpose |
|---|---|---|
| Java | 17 | Programming Language |
| Spring Boot | 3.0.3 | Application Framework |
| Spring Web | 2.7.6 | REST API |
| Spring Kafka | 3.0.3 | Kafka Integration |
| Apache Maven | Latest | Build Tool |

---

## ⚡ Getting Started

### Prerequisites

- ☕ **Java 17+**
- 🐳 **Docker** (recommended for running Kafka locally)
- 📦 **Apache Maven** or use the included `mvnw` wrapper

### 1. Start Apache Kafka

The easiest way is via Docker:

```bash
docker run -d --name kafka \
  -p 9092:9092 \
  -e KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper:2181 \
  bitnami/kafka:latest
```

Or use a `docker-compose.yml` with Zookeeper + Kafka.

### 2. Clone the Repository

```bash
git clone https://github.com/bdostumski/learning-apache-kafka.git
cd learning-apache-kafka
```

### 3. Run the Application

```bash
./mvnw spring-boot:run
```

On startup, `CommandLineRunner` will automatically send **100 messages** to the `syscomz` topic. Watch the console for consumer output:

```
Listener received data: Hello kafka 0 :)
Listener received data: Hello kafka 1 :)
...
```

### 4. Publish a Message via REST

```bash
curl -X POST http://localhost:8080/api/v1/messages \
  -H "Content-Type: application/json" \
  -d '{"message": "Hello from REST!"}'
```

---

## 🔌 API Reference

| Method | Endpoint | Description | Body |
|--------|----------|-------------|------|
| `POST` | `/api/v1/messages` | Publish a message to Kafka | `{ "message": "your text" }` |

---

## ⚙️ Configuration

| Property | Default | Description |
|----------|---------|-------------|
| `spring.kafka.bootstrap-servers` | `localhost:9092` | Kafka broker address |

---

## 📚 Key Concepts Explored

- **Kafka Topics** — Messages are published to and consumed from the `syscomz` topic
- **Producer Configuration** — `ProducerFactory` with `StringSerializer` (key) + `JsonSerializer` (value)
- **Consumer Configuration** — `ConsumerFactory` with `StringDeserializer` + `JsonDeserializer` with trusted packages
- **Listener Container Factory** — `ConcurrentKafkaListenerContainerFactory` for concurrent message processing
- **Custom Object Messaging** — Sending and receiving a custom `Message` record with a timestamp

---

## 📄 License

This project is open source and available for learning purposes.

---

<div align="center">
Made with ❤️ for learning Apache Kafka with Spring Boot
</div>
