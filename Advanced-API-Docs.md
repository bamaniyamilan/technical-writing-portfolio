# Advanced API Documentation — E-Commerce Platform

This document provides developer-focused details for advanced API operations including pagination, filtering, sorting, authentication flows, rate limiting, and webhook handling.

Base URL:

```
https://api.ecommerce.com/v1
```

Authentication:

```
Authorization: Bearer <API_KEY>
```

---

# 1. Pagination

Most list endpoints support cursor-based pagination.

## Example Endpoint

```
GET /products?limit=20&cursor=eyJpZCI6IjEwMCJ9
```

### Query Parameters

| Name   | Type   | Description                                    |
| ------ | ------ | ---------------------------------------------- |
| limit  | number | Number of items per page (default 20, max 100) |
| cursor | string | Token indicating the next page of results      |

### Response

```json
{
  "data": [
    { "id": "prd_101", "name": "Running Shoes" }
  ],
  "next_cursor": "eyJpZCI6IjEwMSJ9"
}
```

---

# 2. Filtering & Sorting

List endpoints allow filtering by fields and sorting results.

## Example Endpoint

```
GET /products?category=shoes&min_price=500&sort=price&order=asc
```

### Supported Filters

| Filter    | Description                |
| --------- | -------------------------- |
| category  | Filter by product category |
| min_price | Minimum price              |
| max_price | Maximum price              |
| in_stock  | true/false                 |

### Sorting

| Query | Description                            |
| ----- | -------------------------------------- |
| sort  | Field to sort by (price, name, rating) |
| order | asc / desc                             |

---

# 3. Authentication Flow

The API uses Bearer Token authentication.

## 3.1 Obtain Token

```
POST /auth/login
```

Response:

```json
{
  "token": "eyJhbGci...",
  "expires_in": 3600
}
```

## 3.2 Token Expiry

If token expires, the API returns:

```json
{
  "error": "token_expired",
  "message": "Authentication token has expired.",
  "status": 401
}
```

---

# 4. Rate Limiting

To protect system performance, rate limits apply.

### Headers in Response

| Header                | Description                |
| --------------------- | -------------------------- |
| X-RateLimit-Limit     | Total allowed requests     |
| X-RateLimit-Remaining | Requests left              |
| X-RateLimit-Reset     | Time until reset (seconds) |

### Rate Limit Exceeded Response

```json
{
  "error": "rate_limit_exceeded",
  "message": "Too many requests. Try again later.",
  "status": 429
}
```

---

# 5. Webhook Events

Webhooks are triggered when key events occur (e.g., order creation, payment success).

## Webhook Notification Format

```json
{
  "event": "payment.success",
  "timestamp": 1738392021,
  "data": {
    "order_id": "ord_789",
    "amount": 3998,
    "status": "paid"
  }
}
```

## Required Headers

```
X-Signature: <HMAC_SHA256_SIGNATURE>
Content-Type: application/json
```

## Example Webhook Handler

```javascript
app.post('/webhooks/payment', (req, res) => {
  const signature = req.headers['x-signature'];
  // Validate signature
  // Process payment event
  res.status(200).send({ received: true });
});
```

---

# 6. Error Handling

Standardized error format across the API.

```json
{
  "error": "invalid_parameter",
  "message": "The value of 'price' must be a number.",
  "status": 400
}
```

Common Errors:

* **400 Bad Request** – Missing or invalid fields
* **401 Unauthorized** – Token missing or expired
* **404 Not Found** – Resource does not exist
* **409 Conflict** – Duplicate entries
* **429 Too Many Requests** – Rate limit exceeded

---

# 7. Webhook Security

Verify webhooks using HMAC SHA-256.

### Verification Example

```javascript
const crypto = require('crypto');

const verify = (payload, signature, secret) => {
  const hash = crypto.createHmac('sha256', secret).update(payload).digest('hex');
  return hash === signature;
};
```
