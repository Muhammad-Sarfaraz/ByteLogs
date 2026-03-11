# AWS SQS (Simple Queue Service) 

## Overview
Amazon Simple Queue Service (SQS) is a fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications. SQS allows you to send, store, and receive messages between software components at any volume, without losing messages.

---

## Key Concepts

### 1. Queue Types
- **Standard Queue**
  - Best-effort ordering (messages might be delivered out of order)
  - At-least-once delivery (messages can be delivered multiple times)
  - High throughput

- **FIFO Queue** (First-In-First-Out)
  - Exactly-once processing
  - Strict message ordering
  - Limited throughput compared to standard queues

### 2. Message
- Contains data sent between components.
- Max size: 256 KB
- Can include attributes (metadata) for filtering and processing.

### 3. Visibility Timeout
- Time a message is hidden after being received by a consumer.
- Prevents multiple consumers from processing the same message simultaneously.
- Default: 30 seconds (configurable 0–12 hours)

### 4. Dead Letter Queue (DLQ)
- Used to store messages that could not be processed successfully.
- Helps in debugging and preventing message loss.

### 5. Message Retention
- Time SQS retains a message if not deleted.
- Range: 1 minute – 14 days (default: 4 days)

---

## Common Operations

### 1. Create a Queue
- **AWS Console**: Navigate to SQS → Create queue → Select Standard/FIFO → Configure
- **AWS CLI Example**:
```bash
aws sqs create-queue --queue-name MyQueue
