### Authorize Endpoint
**GET** `https://auth.company1.com/authorize`

#### Query Parameters:
| Parameter       | Type   | Description                                 |
|-----------------|--------|---------------------------------------------|
| `client_id`     | string | Your application's client ID.              |
| `response_type` | string | Must be `code`.                            |
| `redirect_url`  | string | The callback URL to handle responses.       |
| `code_challenge`| string | Base64-encoded PKCE code challenge.         |
| `state`         | string | *(Optional)* Protects against CSRF attacks.|

---

#### **2. Token Exchange Endpoint**
```markdown
### Token Exchange Endpoint
**POST** `https://auth.company1.com/token`

#### Body Parameters:
| Parameter       | Type   | Description                                 |
|-----------------|--------|---------------------------------------------|
| `grant_type`    | string | Must be `authorization_code`.              |
| `code`          | string | Authorization code from step 1.            |
| `redirect_url`  | string | Must match the value from step 1.           |
| `code_verifier` | string | Original PKCE code verifier.               |

- User
### User Entity
Represents a registered user on Company1.

#### Fields:
| Field       | Type   | Description                                    |
|-------------|--------|------------------------------------------------|
| `id`        | string | Unique Identifier for the user.               |
| `username`  | string | User's display name.                          |
| `email`     | string | User's email address.                         |
| `created_at`| string | ISO timestamp for account creation.           |
 
 - Item
### Item Entity
Represents a product listed for sale.

#### Fields:
| Field         | Type    | Description                                 |
|---------------|---------|---------------------------------------------|
| `id`          | string  | Unique identifier for the item.            |
| `title`       | string  | Name of the item.                          |
| `description` | string  | Item details provided by the seller.       |
| `price`       | number  | Price of the item in (specify currency).    |
| `status`      | string  | Status: `available`, `sold`.               |

- Transaction
### Transaction Entity
Represents a sale or purchase.

#### Fields:
| Field         | Type   | Description                                  |
|---------------|--------|----------------------------------------------|
| `id`          | string | Unique Identifier for the transaction.       |
| `item_id`     | string | Associated item ID.                         |
| `buyer_id`    | string | User ID of the buyer.                       |
| `seller_id`   | string | User ID of the seller.                      |
| `status`      | string | Status: `pending`, `completed`.             |
