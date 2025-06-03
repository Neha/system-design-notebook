# Week 3: Register API Refinement - Scaling Discussions

We focused on Scaling related discussions from week 2 for Register API.
The focus of this 1:1 session was - Decision on SQL Database for ACID compliance and Sharding Design for User Database.

Scaling considerations required us to revisit our tech decisions of week 1 and week 2.

[Diagram week 3](./diagrams/week-3.png)

## 🔁 Updates from Week 2

- Selected an SQL database to ensure ACID compliance, prioritizing consistency over availability.
- Updated **deduplication** check using **Last write** Cache.
- Sharding Options and considerations for Register API.

---

## Database Type Selection

- Despite being **write-heavy**, this is a system where correctness and consistency outweigh raw scalability and performance
- **Consistency** over **Availability** to ensure deduplication of Email Addresses.
- **ACID Compliance** database is preferred hence decided to use SQL. 


---

## Scaling Considerations

To improve performance of overall system:

- Decided to go for a **Standy Main Replica** for main database
- **Standby Main Replica** will be kept in SYNC to ensure Consistency
- **Standby Main Replica** is used to check deduplication reads

---

## Sharding

- Explored following **Sharding** strategies:
  - **Alphabetic bucket (A–Z)**
  - **Geographical sharding**
  - **By email hash**

Decided to go ahead with **Alphabetic bucket (A-Z)** based Sharding for Email Address given it's simple yet effective for evenly distributing user data and enables fast, deterministic shard selection during registration.


---

## Cache Strategy

- Decided to use **Last Write** Cache strategy to:
  - Reduces DB Load on Retries
  - Fast Feedback to User
  - Short TTL to keep the memory in check

---

## Event Driven System

- Email Delivery through Batch Processing
  - Decided to go for a 3rd party solution for Email Delivery
  - Emails with "Failed" delivery can be kept in a separate database for retries
  - Retries can be configured through batch processing every 24 hours

---

## Next Session

- Extend system to support Login functionality
- Discuss what prior decisions needs to be reconsidered/changed due to extend system to support Login

