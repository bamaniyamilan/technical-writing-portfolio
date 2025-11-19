# Quickstart Guide — E-Commerce Platform

Welcome to the E-Commerce Platform! This Quickstart Guide will help new developers and users get started quickly with core features such as authentication, browsing products, adding items to the cart, and placing an order.

---

# 1. Create an Account

To begin using the platform, create an account.

### Endpoint

```
POST /auth/register
```

### Example Request

```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "mypassword"
}
```

### Example Response

```json
{
  "message": "Account created successfully",
  "user_id": "usr_12345"
}
```

---

# 2. Log In & Get API Token

Once registered, log in to get your access token.

### Endpoint

```
POST /auth/login
```

### Example Request

```json
{
  "email": "john@example.com",
  "password": "mypassword"
}
```

### Example Response

```json
{
  "token": "eyJhbGci...",
  "expires_in": 3600
}
```

Use this token for all API calls.

---

# 3. Get All Products

Browse available products.

### Endpoint

```
GET /products
```

### Example Response

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

# 4. Add Product to Cart

Select a product and add it to your cart.

### Endpoint

```
POST /cart
```

### Example Request

```json
{
  "product_id": "prd_101",
  "quantity": 1
}
```

### Example Response

```json
{
  "cart_id": "crt_550",
  "message": "Item added to cart"
}
```

---

# 5. View Cart

Check your cart before placing the order.

### Endpoint

```
GET /cart
```

### Example Response

```json
{
  "items": [
    {
      "product_id": "prd_101",
      "name": "Running Shoes",
      "quantity": 1,
      "price": 1999
    }
  ],
  "total_amount": 1999
}
```

---

# 6. Place Your First Order

Place an order using your cart ID.

### Endpoint

```
POST /orders
```

### Example Request

```json
{
  "cart_id": "crt_550",
  "payment_method": "card"
}
```

### Example Response

```json
{
  "order_id": "ord_800",
  "status": "processing",
  "message": "Order placed successfully"
}
```

---

# 7. Track Your Order

Check the current status of your order.

### Endpoint

```
GET /orders/{id}
```

### Example Response

```json
{
  "order_id": "ord_800",
  "status": "shipped",
  "estimated_delivery": "2025-01-12"
}
```

---

# 8. You're Ready to Explore!

You have now:

* Created an account
* Logged in and obtained a token
* Viewed products
* Added items to cart
* Placed your first order
* Tracked your order

You're fully set up to continue integrating or using the E-Commerce Platform.
