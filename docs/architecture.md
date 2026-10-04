# System Architecture

## Goal

CDC platform demonstrating reliable movement of database changes from PostgreSQL through Debezium and Kafka into downstream processing/storage, with Rust for event consumption and processing.

## Flow

~~~text
PostgreSQL
(transactional DB)
      |
      | WAL
      v
Debezium CDC Connector
      |
      | change events
      v
Apache Kafka
      |
      v
Rust Consumer
      |
      +----------------+
      |                |
      v                v
Offsets / Replay   Data Lake /
                   Analytics
~~~

## Core concerns

- WAL-based change capture
- Kafka offsets and replay
- Ordering and partitioning
- At-least-once delivery
- Duplicate handling and idempotency
- Schema evolution
- Consumer recovery
- Deterministic replay

## Local architecture

The target local stack is PostgreSQL + Debezium + Kafka + Rust consumer, allowing failures and recovery to be demonstrated without cloud dependencies.
