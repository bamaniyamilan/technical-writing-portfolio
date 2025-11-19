# API Documentation — E-Commerce Platform

## Overview

The E-Commerce API enables developers to integrate product browsing, cart management, user authentication, and order processing into external applications. All endpoints follow REST principles and use JSON for request and response bodies.

Base URL:

```
https://api.ecommerce.com/v1
```

Authentication:

```
Authorization: Bearer <API_KEY>
```

---

# 1. Authentication API

## POST /auth/login

Authenticate a user using email and password.

### Request Body

```json
{
  "email": "user@example.com",
  "password": "mypassword"
}
```

### Response

```json
{
  "token": "eyJhbGci...",
  "expires_in": 3600
}
```

---

# 2. Product API

## GET /products

Retrieve a list of all available products.

### Query Parameters

| Name     | Type   | Description                 |
| -------- | ------ | --------------------------- |
| category | string | Filter products by category |
| limit    | number | Limit the number of results |

### Response

```json
[
  {
    "id": "prd_101",
    "name": "Running Shoes",
    "price": 1999,
    "in_stock": true
  }
]
```

---

## GET /products/{id}

Retrieve details of a specific product.

### Response

```json
{
  "id": "prd_101",
  "name": "Running Shoes",
  "description": "Comfortable sports shoes",
  "price": 1999,
  "stock": 42
}
```

---

# 3. Cart API

## POST /cart

Add an item to the user's cart.

### Request Body

```json
{
  "product_id": "prd_101",
  "quantity": 2
}
```

### Response

```json
{
  "cart_id": "crt_554",
  "message": "Item added to cart"
}
```

---

## GET /cart

Retrieve the current user's cart.

### Response

```json
{
  "items": [
    {
      "product_id": "prd_101",
      "name": "Running Shoes",
      "quantity": 2,
      "price": 1999
    }
  ],
  "total_amount": 3998
}
```

---

# 4. Order API

## POST /orders

Place a new order.

### Request Body

```json
{
  "cart_id": "crt_554",
  "payment_method": "card"
}
```

### Response

```json
{
  "order_id": "ord_789",
  "status": "processing",
  "message": "Order placed successfully"
}
```

---

## GET /orders/{id}

Retrieve order details.

### Response

```json
{
  "order_id": "ord_789",
  "status": "shipped",
  "items": [
    {
      "product_id": "prd_101",
      "quantity": 2
    }
  ],
  "total_amount": 3998
}
```

---

# 5. Error Responses

Standard error format:

```json
{
  "error": "invalid_request",
  "message": "The provided product ID is invalid.",
  "status": 400
}
```
