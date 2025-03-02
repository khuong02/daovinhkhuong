## Frontend Layer (Web & Mobile)
* Technologies: React, Next.js, Flutter
* Cloud Services: AWS CloudFront + ALB (Application Load Balancer)
* Why?:
  - CloudFront provides low-latency content delivery globally.
  - Load Balancer distributes traffic to multiple API instances.
  - Next.js enables SSR (Server-Side Rendering) for SEO and performance.

## API Gateway & Microservices
* Technologies: API Gateway, Golang
* Cloud Services: AWS API Gateway + AWS EKS (Kubernetes) + Karpenter
* Why?:
  - API Gateway manages REST & WebSocket traffic.
  - Microservices ensure modular, scalable architecture.
  - EKS (Kubernetes) auto-scales critical services like order processing.
  - Karpenter is an open-source node lifecycle management project built for Kubernetes. Adding Karpenter to a Kubernetes cluster can dramatically improve the efficiency and cost of running workloads on that cluster

## Trading Engine (Core Matching System)
* Technologies: Golang
* Cloud Services: AWS EKS + Redis
* Why?:
  - High-performance, low-latency matching engine.
  - Redis caching to store open orders and transaction states.
  - Golang strong Concurrency with Goroutines

## Database Layer
* Relational Data (User & Orders): PostgreSQL
* Real-Time Caching: Redis
* Why?:
  - PostgreSQL for ACID-compliant transactions.
  - Redis for sub-millisecond query latency.

## Messaging & Events
* Technologies: Kafka
* Why?:
  - Kafka handles trade events asynchronously.

## Monitoring
* Technologies: Prometheus + Grafana, ELK
* Why?:
  - Monitor system metrics, logs, and alerts.

## Scaling Strategies
* API Scaling: AWS ALB + EKS + Karpenter.
* Database Scaling: PostgreSQL Master-Slave
* Event Processing Scaling: Kafka partitioning + Consumer Groups.
* Caching: Redis read replicas reduce DB load.