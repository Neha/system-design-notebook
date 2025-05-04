# Week 2: Register API Refinement

continuing from week 1 discussion, we moved to the more in depth discussion.
The focus of this 1:1 session was - "How to handle the duplication of email ids? Is No-SQL would be good choice?"

These new questions lead us to revisit our tech decision of week 1. 

[Diagram week 2](./diagrams/week-2.png)

## 🔁 Updates from Week 1

- Moved logic of DB update after **3rd-party email service** response.
- Introduced **deduplication** check using cache and Request DB.
- Started defining **register types** and **service types**.

---

## 🔒 Security Enhancements

- Validate all input fields.
- Secure password storage using **salted hash**.
- Use **JWT** or **cookie-based** sessions.
- Store session tokens in a **session table** (with TTL).
- Protect APIs behind **API Gateway** and throttling.

---

## 🧠 Email Duplication Strategy

To prevent duplicate registrations with the same email:

- **Cache** used to detect recent registration attempts.
- **Request DB** stores registration attempts, possibly sharded:
  - **By email hash**
  - **Alphabetic bucket (A–Z)**
  - **Consistent hashing**

---

## 📬 Email Retry System

To handle failed or delayed email deliveries:

- Store undelivered requests in a retry table or queue.
- Retry sending confirmation only after confirmation of delivery failure.
- Event-driven architecture using:
  - **Email Service → Event Queue → Retry Job**

---

## 🔁 Token Expiry and Cleanup

- Tokens have a defined **expiry time**.
- Cleanup via **CRON job** that:
  - Expires unconfirmed users.
  - Deletes stale token entries.
- Ensures token expiration and email retry are in **sync**.

---

## ⚖️ Scaling Considerations

- Choose DB type (SQL vs NoSQL) based on:
  - Write-heavy behavior.
  - Query patterns for tokens and status updates.
- **Sharding** strategy for both:
  - User table (by email)
  - Request DB (for deduplication)
- Apply **event-driven** architecture for async tasks.

---

## 📊 Monitoring & Observability

- Add metrics for:
  - Email delivery rate
  - Confirmation success/failure
  - Retry attempts
- Enable **structured logging** for register API flows.

---

## 🛠️ Open Questions

- Optimal sharding function for request DB?
- How to guarantee email delivery acknowledgment?
- Where do we handle retries — job workers or event consumers?


