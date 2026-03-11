# AWS SNS (Amazon Simple Notification Service)

## 1. What is SNS

Amazon Simple Notification Service (SNS) is a fully managed publish/subscribe messaging service used to send notifications to multiple subscribers simultaneously.

It works like a broadcast system.

Example flow:

Application → SNS Topic → Multiple Subscribers

Subscribers may include:

* Email
* SMS
* HTTP / HTTPS endpoints
* AWS Lambda
* SQS queues
* Mobile push notifications

---

## 2. Core Concepts

### Topic

A Topic is the communication channel where messages are published.

Examples:

```
user-signup-topic
payment-success-topic
system-alert-topic
```

Publisher sends message → Topic → Topic delivers to all subscribers.

---

### Publisher

The service or application sending the message.

Examples:

* Backend API
* Background worker
* Microservice
* Scheduled job

Example workflow:

```
User signs up → publish message → send welcome email
```

---

### Subscriber

A subscriber is any endpoint that receives messages from a topic.

Examples:

* Email address
* SQS queue
* Lambda function
* Webhook (HTTP/HTTPS)

---

## 3. Basic Architecture

Typical architecture:

```
Backend App
     |
     v
   SNS Topic
  /    |     \
Email  SQS   Lambda
```

This enables fan-out messaging where one message is delivered to multiple systems.

---

## 4. Common Use Cases

System Alerts:

```
Server error → SNS → Email / Slack webhook
```

User Notifications:

```
User purchase → SNS → Email confirmation
```

Microservices Communication:

```
Service A publishes → SNS → Service B, C, D receive
```

Fan-out Architecture:

```
SNS distributes messages to multiple SQS queues
```

---

## 5. SNS vs SQS

| Feature             | SNS     | SQS          |
| ------------------- | ------- | ------------ |
| Type                | Pub/Sub | Queue        |
| Delivery            | Push    | Pull         |
| Multiple consumers  | Yes     | Not directly |
| Message persistence | No      | Yes          |

Common pattern:

```
SNS → SQS → Worker
```

SNS broadcasts the message, SQS stores it for processing.

---

## 6. Message Types

### Standard Topic

* At-least-once delivery
* Best-effort ordering
* Very high throughput

### FIFO Topic

* Exactly-once processing
* Ordered messages
* Topic name must end with `.fifo`

Example:

```
order-events.fifo
```

---

## 7. AWS CLI Examples

Create topic:

```
aws sns create-topic --name user-signup-topic
```

Publish message:

```
aws sns publish \
  --topic-arn TOPIC_ARN \
  --message "New user registered"
```

---

## 8. Security

SNS supports:

* IAM permissions
* Topic access policies
* Encryption with AWS KMS
* HTTPS endpoints for secure delivery

---

## 9. Best Practices

Use SNS + SQS fanout architecture for reliability.

Example:

```
SNS Topic
   |
   +----> SQS Queue → Worker A
   |
   +----> SQS Queue → Worker B
```

Advantages:

* Reliable message storage
* Retry mechanisms
* Independent service scaling
* Failure isolation

---

## 10. Limits

Common limits:

* Maximum message size: 256 KB
* Very high publish throughput (millions of messages per second for standard topics)

---

## 11. Cost Overview

Pricing mainly depends on:

* Publish requests
* Notification deliveries

Typical costs:

* ~$0.50 per 1 million publish requests
* SMS notifications cost extra
