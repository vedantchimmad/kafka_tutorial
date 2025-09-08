# Apache Kafka

---

## 📌 Introduction
Apache Kafka is an **open-source distributed event streaming platform** used for building **real-time data pipelines and streaming applications**.  
It is designed to handle **high throughput, fault tolerance, and scalability** while enabling **publish-subscribe** messaging at scale.

---

## ⚡ Key Features
- ⚡ **High Throughput**: Capable of processing millions of events per second.
- 📈 **Scalable**: Easily scales horizontally by adding more brokers.
- 💾 **Durable**: Stores streams of records in a distributed, replicated log.
- 🛡️ **Fault-Tolerant**: Data is replicated across brokers for reliability.
- ⏱️ **Real-time Processing**: Integrates with stream processing frameworks (e.g., Spark, Flink, Kafka Streams).

---

## 🏗️ Kafka Architecture

### 🔑 Components
1. 📝 **Producer**
    - Applications that publish (write) data to Kafka topics.
    - Example: IoT device sending sensor data.

2. 👨‍💻 **Consumer**
    - Applications that subscribe (read) data from Kafka topics.
    - Example: Fraud detection system processing transactions.

3. 📂 **Topic**
    - Logical channel where records are stored and categorized.
    - Data inside a topic is divided into **partitions**.

4. 🔀 **Partition**
    - Each topic is split into partitions to support parallel processing and scalability.
    - Each partition is an **ordered, immutable sequence of records**.

5. 🖥️ **Broker**
    - Kafka server that stores data and serves client requests.
    - A Kafka cluster is made up of multiple brokers.

6. 🦉 **ZooKeeper (Legacy, being replaced by KRaft)**
    - Manages cluster metadata and leader election.
    - Newer versions (Kafka 2.8+) can run **without ZooKeeper** using **KRaft mode**.

---

## 🔄 Kafka Workflow
1. 📝 **Producers** send data to Kafka topics.
2. 📂 **Topics** are divided into **partitions** across brokers.
3. 👨‍💻 **Consumers** subscribe to topics and read data.
4. 🛡️ Kafka ensures **fault-tolerance** by replicating partitions across brokers.

---

## 🛠️ Use Cases
- 📊 **Real-Time Analytics** (e.g., financial fraud detection)
- 📝 **Log Aggregation** (centralized event collection)
- 🔄 **Stream Processing** (ETL pipelines, real-time dashboards)
- 🏗️ **Event-Driven Architectures** (microservices communication)
- 🔌 **Data Integration** (moving data between databases, storage, and systems)

---

## 🚀 Example: Producer and Consumer in Python

```python
# Producer Example
from kafka import KafkaProducer

producer = KafkaProducer(bootstrap_servers='localhost:9092')
producer.send('test-topic', b'Hello Kafka!')
producer.flush()

# Consumer Example
from kafka import KafkaConsumer

consumer = KafkaConsumer('test-topic',
                         bootstrap_servers='localhost:9092',
                         auto_offset_reset='earliest',
                         group_id='test-group')

for message in consumer:
    print(f"Received: {message.value.decode('utf-8')}")
````

---

## 📊 Kafka vs Traditional Messaging Systems

| Feature            | Kafka (⚡)                          | Traditional MQ (📦 RabbitMQ, ActiveMQ) |
| ------------------ | ---------------------------------- | -------------------------------------- |
| Throughput         | ⚡ Very High                        | 📦 Moderate                            |
| Storage            | 💾 Persistent (disk-based log)     | 🛑 Usually in-memory                   |
| Scalability        | 📈 Horizontal, partition-based     | 🔒 Limited                             |
| Ordering Guarantee | 🔀 Within partition                | 📦 Queue-based                         |
| Use Case           | 🔄 Event streaming, data pipelines | 📬 Task scheduling, async processing   |

---
## ⚖️ Key Differences

| Feature / Aspect        | 🗂️ **Autoloader (Databricks)**                          | ⚡ **Apache Kafka**                                |
|--------------------------|----------------------------------------------------------|---------------------------------------------------|
| **Type**                | File-based streaming ingestion                          | Event streaming platform (publish-subscribe model) |
| **Source**              | Cloud storage (S3, ADLS, GCS, etc.)                     | Producers (apps, microservices, IoT devices, etc.) |
| **Data Format**         | CSV, JSON, Parquet, Avro, Delta, etc.                   | Events/records (byte array, JSON, Avro, Protobuf) |
| **Use Case**            | Incremental loading of new/changed files                | Real-time event/message streaming & processing    |
| **Trigger Mode**        | Batch (micro-batch) / Continuous                        | Real-time (low-latency streaming)                 |
| **Schema Evolution**    | ✅ Supports schema inference & evolution                 | ❌ Manual handling (schema registry required)      |
| **Integration**         | Tight integration with **Databricks + Delta Lake**       | Integrates with multiple systems (Spark, Flink, DBs) |
| **Scalability**         | Depends on cloud storage scalability                    | Horizontally scalable via partitions and brokers  |
| **Fault Tolerance**     | ✅ Handled by cloud storage durability                   | ✅ Replication across brokers                     |
| **Best Fit Scenario**   | When data is arriving as **files in cloud storage**      | When data is **event-driven and continuous**      |

