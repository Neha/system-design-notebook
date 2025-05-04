# Week 1: Register API Design

## ✅ Functional Requirements

1. Users can register using **name**, **email**, and **password**.
2. A confirmation link will be sent to the user's email ID.
3. On clicking the confirmation link, the user is successfully registered.

## 🔒 Non-Functional Requirements

1. Prioritize **availability over consistency**.
2. Ensure **security** of the system.

---

## 🔁 Registration Flow

1. User submits name, email, and password.
2. System stores data with status as `pending`.
3. Sends email with confirmation link.
4. On clicking, status changes to `active`.

---

## 📦 API Design

**Endpoint**: `POST /facebook.com/api/v1/register`

**Request Body**:
```json
{
  "name": "string",
  "email": "string",
  "password": "string"
}
```

## responses

```json

Success (200):

{ "message": "", "description": "", "data": { "date": "", "other": "" } }

``` 

```json

Error (4xx):

{ "message": "", "description": "", "error_code": "" }
```

### 🛢️ Data Flow

[Diagram week 1](./diagrams/week-1.png)

- Client sends request.

- Server stores user (status = pending) in DB.

- Generates token + confirmation link.

- Sends email via email service.

- Confirmation changes status to active.

### 🛡️ Security Measures

- Data validation before DB insert.

- Password hashing using SALT.

- API Gateway to handle and throttle requests.

- Keep DB, email service, and confirm endpoint private.

⚖️ Scaling Considerations

- Use CloudFront for caching.

- Throttle /register with rate limits.

- Write-heavy workload; ensure appropriate DB design.

- Single-leader replication.

- NoSQL acceptable.

- CAP trade-off: Prefer availability.

- Horizontal scaling and partitioning.


### 🔁 Maintenance

- CRON job to clean up unconfirmed users.

- Token expiry logic.

- Retry logic for failed email deliveries.

### What Else?

- Prevent email duplication using cache or request DB.

- Support re-sending confirmation links.

- Handle syncing between token expiry and email delivery.

- CRON job should clean stale data (e.g. after 24 hrs).