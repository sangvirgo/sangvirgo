Nguyen Luu Tan Sang


Backend Engineer · Java · Spring Boot · Microservices





  I build production-grade distributed systems — from microservice architecture and real-time geospatial engines to high-concurrency databases. My focus is on correctness under load, clean domain boundaries, and systems that scale.







  📍 Vietnam  |  📧 tansang06092004@gmail.com




---

## 🛠️ Tech Stack

**Languages:** Java (primary) · C++ · JavaScript · Python · Shell Script

**Backend:** Spring Boot 3 · Spring Cloud (Eureka, Config, Gateway, OpenFeign) · Spring Security · Resilience4j

**Databases:** PostgreSQL + PostGIS · MySQL 8 · MongoDB (Replica Set) · Redis

**Payments & Auth:** VNPay · JWT · OAuth2 (Google, GitHub)

**Infrastructure:** Docker · Docker Compose · Maven

**Frontend:** React · Next.js · Tailwind CSS

**Tools:** IntelliJ IDEA · Postman · Git · Grafana k6 (load testing)

---

## 🚀 Featured Projects

---

### 🎬 Cinestar — Distributed Cinema Booking System

> **Core challenge:** Eliminate double-booking under extreme concurrent load without pessimistic locks.

**[Backend Repo](https://github.com/cinema-Distributed-database/backend)**

A fault-tolerant cinema ticketing platform engineered around a distributed MongoDB architecture, designed to maintain 99.9% uptime and guaranteed seat integrity during blockbuster releases.

**Key Engineering Decisions:**
- **Atomic Concurrency Control** — Replaced the naive "Read-Check-Write" pattern with a single MongoDB atomic update command (`findAndModify` with status validation), eliminating race conditions at the database level without locking overhead
- **ACID Multi-Document Transactions** — Wrapped the full payment-to-seat-confirmation flow in a single Spring `@Transactional` scope: either the user is charged AND their seat is confirmed, or everything rolls back — no ghost bookings
- **4-Node MongoDB Replica Set** — 1 Primary + 3 Secondaries with automatic leader election; Primary failure is recovered in seconds with zero manual intervention
- **Read/Write Separation** — Routed 90% of read traffic (schedules, seat maps) to Secondary nodes via `secondaryPreferred`, keeping the Primary available for write-critical transactions
- **Soft-Lock Expiry Sweeper** — `@Scheduled` job releases `HOLDING` seats not paid within 5 minutes, maintaining high seat pool turnover
- **2dsphere Geospatial Index** — Efficient "Nearby Cinema" discovery powered by MongoDB's native geo-indexing
- **Embedded Document Pattern** — Full seat maps stored within each `Showtime` document for O(1) fetch of theater state in a single query

**Stack:** Java 21 · Spring Boot 3.3 · MongoDB Replica Set · VNPay · Docker

---

### 🛒 SmartVN — E-Commerce Microservices Platform

> **Core challenge:** Handle high product catalog traffic with near-zero latency under concurrent load.

**[Backend Repo](https://github.com/sangvirgo/microservice-smartVN)**

A production-grade cloud-native e-commerce backend, benchmarked under 100 concurrent virtual users with Grafana k6. Demonstrated **5.5× response time improvement** and **+26% throughput** gain from Redis caching.

**Performance Benchmark (Grafana k6, 100 VUs):**

| Metric | Without Cache | With Redis |
|---|---|---|
| Avg Response | 47.81 ms | 8.66 ms |
| p95 Response | 172.88 ms | 19.11 ms |
| Throughput | 196.8 req/s | 248.5 req/s |
| Failure Rate | 0.02% | **0.00%** |

**Key Engineering Decisions:**
- **Redis Cache-Aside Strategy** — Applied at the highest-traffic service (Product Service): `productDetail` TTL 10 min, `categories` TTL 1 hr, with automatic `@CacheEvict` on write
- **Cache bypass flag** — `getProductDetail(id, bypassCache)` allows admin/internal calls to skip cache for consistency-critical reads
- **Internal API Key auth** — Service-to-service calls (Admin → User/Product/Order) secured via `X-API-KEY` header, separated from user-facing JWT flows
- **OAuth2 integration** — Google & GitHub login via Spring Security OAuth2, with OTP email verification for standard registration
- **Resilience4j on Admin Service** — Circuit breaker + fallback on all aggregation Feign clients; admin dashboard degrades gracefully if a downstream service is slow
- **AI Recommendation Pipeline** — User interactions (VIEW = 1.0, ADD_TO_CART = 2.0, PURCHASE = 3.0) exported via internal endpoints for offline recommendation model training
- **Cloudinary media management** — Product image upload/management via Cloudinary SDK

**Stack:** Java 21 · Spring Boot 3.3 · Spring Cloud · MySQL 8 · Redis 7 · VNPay · Docker Compose

---

### 🍔 QuickFood — Full-Stack Food Delivery Platform

> **Core challenge:** Build a complete multi-role delivery ecosystem solo — from DB design to containerized deployment.

**[Backend Repo](https://github.com/sangvirgo/quickfood)**

An end-to-end food delivery platform mirroring UberEats/DoorDash core flows, developed entirely solo. Covers system architecture, backend microservices, real-time geospatial engine, and a multi-role frontend.

**Key Engineering Decisions:**
- **PostGIS Spatial Queries** — Real-time driver location tracking, distance calculation, and delivery radius validation powered by PostgreSQL + PostGIS extension
- **Pessimistic Locking for Order Acceptance** — When N drivers simultaneously accept the same `WAITING` order, exactly one succeeds; all others receive a safe rejection — guaranteed by transactional pessimistic lock at the DB level
- **Database-per-Service** — Core service owns `quickfood_core` (users, products, orders); Delivery service owns `quickfood_delivery` (shippers, shipments, PostGIS). No shared schema, no domain leakage
- **Dynamic Service Discovery** — Netflix Eureka registry with Spring Cloud Gateway as the single JWT-verified entry point for all API traffic
- **Multi-role Next.js Frontend** — Fully typed, responsive dashboards for Customers, Restaurant Staff, and Delivery Drivers
- **One-command infrastructure** — `docker compose up --build -d` spins up both PostgreSQL/PostGIS instances, Eureka, API Gateway, Core Service, and Delivery Service

**Stack:** Java 17 · Spring Boot 3 · Spring Cloud · PostgreSQL + PostGIS · Next.js · Docker Compose

---

## 📊 GitHub Stats




  
  







  




---




  Open to backend engineering roles — distributed systems, high-concurrency, Java/Spring ecosystem.

  tansang06092004@gmail.com



  
