# Traveller-All-in-One-Network-Quality-Assessment

📖 **Introduction**

Traveller is a Client/Server (C/S) based distributed system designed for real-time network quality assessment and monitoring.
It provides multi-layer probes (ICMP, TCP, L7, MTR), intelligent task scheduling, data aggregation, and alerting.
The system helps upper-layer applications improve stability, availability, and user experience by guiding traffic through the best quality network paths.

🏗️ **Key Component**

Client (Agent)

- Pulls probe tasks from Manager via HTTP

- Executes probes (ICMP / TCP / L7 / MTR)

- Compresses and reports results to MQ

Manager (Server)

- Splits & assigns probe tasks

- Aggregates & analyzes results

- Stores metadata in MySQL

- Publishes probe results to MQ

Message Queue (MQ)

- Decouples data producers (clients) and consumers (storages, alerting)

- Buffers probe results, supports retry & backpressure

- Provides two data paths:

- 5s updates → ClickHouse → Grafana (real-time visualization)

- 10min updates → MySQL (metadata storage)

ClickHouse

- High-performance time-series storage for probe results

- Supports efficient query & analytics

Prometheus + Alertmanager

- Monitors probe metrics (loss rate, RTT, availability)

- Triggers alerts when thresholds are exceeded

Grafana

- Real-time dashboard for visualization

MySQL

- Stores task-related metadata (task definition, status, timestamps)
