# Troubleshooting Guide — E-Commerce Platform

This Troubleshooting Guide helps users and developers quickly diagnose and resolve common issues they may encounter while using the E-Commerce Platform.

---

# 1. Login & Authentication Issues

## 1.1 Cannot Log In

**Possible Causes:**

* Incorrect email or password
* Account not verified
* Server temporarily unavailable

**Solutions:**

1. Check that your email and password are correct.
2. Reset your password if needed.
3. Ensure your account has been verified.
4. Try again after 2–3 minutes.

---

## 1.2 Token Expired

**Symptoms:** API requests returning `401 Unauthorized`.

**Solutions:**

1. Log in again to regenerate a new token.
2. Ensure the token is included in every API call:

```
Authorization: Bearer <API_KEY>
```

---

# 2. Product & Search Issues

## 2.1 Products Not Loading

**Possible Causes:**

* Slow network
* Filters too restrictive
* API timeout

**Solutions:**

1. Refresh the page.
2. Clear filters and try again.
3. Check your internet connection.
4. Retry after a few moments.

---

## 2.2 Search Not Showing Results

**Solutions:**

* Check for spelling mistakes.
* Try broader search terms.
* Remove filters.
* Ensure product exists in inventory.

---

# 3. Cart Issues

## 3.1 Item Not Added to Cart

**Possible Causes:**

* Out-of-stock product
* API error
* Session timeout

**Solutions:**

1. Refresh the product page.
2. Ensure the item is in stock.
3. Log in again and retry.

---

## 3.2 Cart Total Not Updating

**Solutions:**

1. Clear browser cache.
2. Re-open the cart.
3. Update item quantity again.
4. If using API, verify request format:

```json
{
  "product_id": "prd_101",
  "quantity": 2
}
```

---

# 4. Checkout & Payment Issues

## 4.1 Payment Failed

**Possible Causes:**

* Insufficient balance
* Incorrect payment details
* Payment gateway issue

**Solutions:**

1. Try a different payment method.
2. Re-enter card/UPI details.
3. Retry after 1–2 minutes.

---

## 4.2 Order Not Showing After Payment

**Solutions:**

1. Refresh the **My Orders** page.
2. Wait for 2–5 minutes for syncing.
3. Check email for order confirmation.
4. Contact support if still missing.

---

# 5. Order Tracking Issues

## 5.1 Tracking Not Updated

**Possible Causes:**

* Delivery partner delay
* API sync delay

**Solutions:**

1. Wait up to 24 hours for shipment updates.
2. Try again later.
3. Contact support if shipment is stuck.

---

# 6. API-Specific Troubleshooting (Developers)

## 6.1 400 Bad Request

**Causes:** Missing or invalid fields.

**Fix:** Check request structure.

## Example

```json
{
  "product_id": "prd_101",
  "quantity": 1
}
```

---

## 6.2 401 Unauthorized

**Fixes:**

* Token missing
* Token expired
* Incorrect Authorization header

Use:

```
Authorization: Bearer <API_KEY>
```

---

## 6.3 404 Not Found

**Causes:** Invalid product, cart, or order ID.

**Fix:** Verify the resource ID.

---

## 6.4 429 Rate Limit Exceeded

**Solutions:**

* Reduce frequency of API calls
* Use caching
* Wait for the reset time in headers

---

# 7. Contact Support

If issues persist, contact:

* **Live Chat** (recommended)
* **Help Center**
* **Email:** [support@ecommerce.com](mailto:support@ecommerce.com)
