# Test-API Documentation

Welcome to the Test-API Documentation! This repository provides a comprehensive guide to integrating with the Test-API, enabling seamless interaction with key entities like users, items, and transactions.

## 📖 Overview
The Test-API allows developers to:
- Manage users and items.
- Handle transactions and disputes.
- Subscribe to webhook events for real-time updates.

This documentation includes:
- API reference (OpenAPI Specification in YAML format).
- Detailed workflows and Mermaid diagrams.
- Guidance for beta environment testing and migration.

### Base URL
All API endpoints are relative to the base URL:  
`https://api.company1.com/v1`

---

## Authentication

Test-API uses **OAuth 2.0 with PKCE (Proof Key for Code Exchange)** for secure authentication.

### OAuth 2.0 + PKCE Workflow

1. **Authorize Endpoint:**

   **GET** `https://auth.company1.com/authorize`  
   Query Parameters:  

   | Parameter        | Type   | Description                              |
   |------------------|--------|------------------------------------------|
   | `client_id`      | string | Your application's client ID.           |
   | `response_type`  | string | Must be `code`.                         |
   | `redirect_url`   | string | The callback URL to handle responses.   |
   | `code_challenge` | string | Base64-encoded PKCE code challenge.     |
   | `state`          | string | (Optional) Protects against CSRF.       |

2. **Token Exchange Endpoint:**

   **POST** `https://auth.company1.com/token`  
   Body Parameters:  

   | Parameter        | Type   | Description                              |
   |------------------|--------|------------------------------------------|
   | `grant_type`     | string | Must be `authorization_code`.           |
   | `code`           | string | Authorization code from step 1.         |
   | `redirect_url`   | string | Must match the value from step 1.       |
   | `code_verifier`  | string | Original PKCE code verifier.            |

---

## Company1 Key Entities

### 1. User
Represents a registered user on Company1.  

| Field         | Type   | Description                           |
|---------------|--------|---------------------------------------|
| `id`          | string | Unique Identifier for the user.      |
| `username`    | string | User's display name.                 |
| `email`       | string | User's email address.                |
| `created_at`  | string | ISO timestamp for account creation.  |

---

### 2. Item
Represents a product listed for sale.  

| Field         | Type    | Description                           |
|---------------|---------|---------------------------------------|
| `id`          | string  | Unique identifier for the item.      |
| `title`       | string  | Name of the item.                    |
| `description` | string  | Item details provided by the seller. |
| `price`       | number  | Price of the item (specify currency).|
| `status`      | string  | Status: `available`, `sold`.         |

---

### 3. Transaction
Represents a sale or purchase.  

| Field         | Type   | Description                           |
|---------------|--------|---------------------------------------|
| `id`          | string | Unique Identifier for the transaction.|
| `item_id`     | string | Associated item ID.                  |
| `buyer_id`    | string | User ID of the buyer.                |
| `seller_id`   | string | User ID of the seller.               |
| `status`      | string | Status: `pending`, `completed`.      |

---
