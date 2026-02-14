# **RTTM – Real-Time Telemetry Monitoring System**

RTTM is a scalable, microservice-based backend system** designed to ingest high-volume telemetry data, store raw data efficiently, perform scheduled aggregations, cache results, and serve analytics through REST APIs.

The system leverages Apache Kafka for ingestion, MongoDB for raw data, MySQL for aggregated metrics, Redis for caching, and Spring Cloud Eureka for service discovery, ensuring high availability and scalability.

---

## **Overview**

RTTM processes telemetry data from upstream producers in real time.
Raw data is ingested through Kafka, persisted for backup and processing, aggregated daily using scheduled jobs, cached for fast access, and exposed via APIs for dashboards and monitoring systems.

Key design goals:

* High-throughput ingestion
* Fault tolerance & data backup
* Daily aggregation and analytics
* Scalable microservices using service discovery
* Low-latency API responses using caching

---

## **Tech Stack**

| Component          | Technology              |
| ------------------ | ----------------------- |
| Backend            | Spring Boot (Java)      |
| Microservices      | Spring Cloud            |
| Service Discovery  | Eureka Server           |
| API Gateway        | Spring Cloud Gateway    |
| Message Broker     | Apache Kafka            |
| Raw Data Storage   | MongoDB                 |
| Aggregated Metrics | MySQL (JPA/Hibernate)   |
| Caching            | Redis                   |
| Scheduling         | Spring Scheduler        |
| Build Tool         | Maven                   |
| Containerization   | Docker & Docker Compose |

---

## **Core Features**

* Real-time telemetry ingestion using Kafka
* Raw data backup and persistence
* Daily scheduled aggregation of metrics
* MongoDB for high-volume raw telemetry storage
* MySQL for structured daily metrics
* Redis caching for fast API responses
* RESTful APIs for metrics, elements, and load balancing
* Eureka-based service discovery for microservices
* Horizontally scalable architecture

---

## **High-Level Architecture**

**Data Flow:**

```
Producer → Kafka → Adapter Service → MongoDB (Raw Data)
                                     ↓
                                Scheduler
                                     ↓
                            Aggregator Service
                                     ↓
                              MySQL (Metrics)
                                     ↓
                               Redis Cache
                                     ↓
                              REST APIs
                                     ↓
                               Dashboard
```

---

## **System Components**

### **Microservices**

| Service                    | Responsibility                              |
| -------------------------- | ------------------------------------------- |
| API Gateway                | Routes client requests to backend services  |
| Adapter / Consumer Service | Consumes Kafka messages and stores raw data |
| Aggregator Service         | Aggregates daily metrics                    |
| Element Service            | Manages telemetry elements                  |
| Load Balancer Service      | Handles load-balanced API calls             |
| Eureka Server              | Service registry & discovery                |

---

### **Controllers**

| Controller             | Endpoint            |
| ---------------------- | ------------------- |
| AggregatorController   | `/api/aggregator`   |
| ElementController      | `/api/element`      |
| LoadBalancerController | `/api/loadbalancer` |

---

### **Services**

* AggregatorService (impl)
* RawDataService (impl)
* KafkaMessageConsumerService
* RedisService
* ElementService (impl)
* LoadBalancerService (impl)

---

### **Databases**

| Database | Usage                    |
| -------- | ------------------------ |
| MongoDB  | Raw telemetry data       |
| MySQL    | Daily aggregated metrics |
| Redis    | Cached API responses     |

---

## **Entity Models**

### **RawData**

* id
* source
* deviceId
* payload
* timestamp

### **DailyMetric**

* id
* metricDate
* elementName
* count

### **Element**

* elementTypeId
* deviceType
* reportName
* deviceName

---

## **Setup Instructions**

### **Step 1: Clone the Project**

```bash
git clone https://github.com/ShrajnaR/admin-tool.git
git clone https://github.com/ShrajnaR/api gateway.git
git clone https://github.com/ShrajnaR/eureka-server.git

```

---

### **Step 2: Open in IDE**

* Open Eclipse / IntelliJ
* Import all services as **Maven Projects**
* Run:

```bash
mvn clean install
```

---

### **Step 3: Configure Application Properties**

Update `application.properties`:

* Kafka bootstrap servers
* MongoDB URI
* MySQL database name
* Username & password
* Redis host & port
* Eureka server URL

---

### **Step 4: Start Infrastructure (Docker)**

```bash
docker-compose up -d
```

Includes:

* Kafka & Zookeeper
* MongoDB
* MySQL
* Redis
* Eureka Server
* API Gateway
* Backend services

---

### **Step 5: Verify Services**

| Service          | URL                     |
| ---------------- | ----------------------- |
| Eureka Dashboard | `http://localhost:8761` |
| API Gateway      | `http://localhost:8080` |
| Health Check     | `/actuator/health`      |

---

## **Scheduler & Aggregation**

* Daily scheduler triggers aggregation jobs
* Reads raw data from MongoDB
* Computes daily metrics
* Stores results in MySQL
* Caches frequently accessed metrics in Redis

---

## **Caching Strategy**

* Redis used for:

  * Frequently accessed metrics
  * Reduced database load
* Cache refresh after aggregation job

---

## **Scalability & Fault Tolerance**

* Kafka partitions for parallel processing
* Eureka for dynamic service discovery
* Stateless services for horizontal scaling
* Database separation for optimized workloads

---

## **Future Enhancements**

* Real-time streaming analytics
* CI/CD pipeline integration
* Kubernetes deployment
* Advanced alerting & threshold engine
* UI dashboard with charts & monitoring
* Distributed tracing (Zipkin / Sleuth)

---

## **Author**

**Name:** Shrajna R
**GitHub:** https://github.com/ShrajnaR

---

## **License**

This project is licensed under the **MIT License**.

---

Just say **NEXT** 🚀
