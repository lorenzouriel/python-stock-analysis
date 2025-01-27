# Stock Management API Endpoints

This document lists the available endpoints for the Stock Management API.

## Base URL
- http://localhost:3000

## Endpoints

### 1. **`GET /stocks`**
- **Description**: Retrieves a list of all stocks.
- **Response**: Returns a JSON array of stocks.

#### Example:
```json
[ 
    {    
        "stock_id": 1,    
        "ticker": "AAPL",    
        "name": "Apple Inc.",    
        "sector": "Technology",    
        "industry": "Consumer Electronics",    
        "currency": "USD",    
        "created_at": "2024-01-01T00:00:00Z" 
}, ...]
```

### 2. `POST /stocks`
- **Description:** Creates a new stock record.
- **Body:**
Requires a JSON object with the following fields:
    - **ticker** (string): Asset code (e.g., AAPL, TSLA)
    - **name** (string): Full company name
    - **sector** (string): Company sector
    - **industry** (string): Company industry
    - **currency** (string): Trading currency

#### Response:
Returns the created stock record with its `stock_id`.

#### Example Request:
```json
{
  "ticker": "AAPL",
  "name": "Apple Inc.",
  "sector": "Technology",
  "industry": "Consumer Electronics",
  "currency": "USD"
}
```

#### Example Response:
```json
{
  "stock_id": 2,
  "ticker": "TSLA",
  "name": "Tesla Inc.",
  "sector": "Automotive",
  "industry": "Electric Vehicles",
  "currency": "USD",
  "created_at": "2024-01-02T00:00:00Z"
}
```

### 3. `GET /stocks/{id}`
- **Description:** Retrieves details of a specific stock by `stock_id`.
- **Parameters:**
    - **id** (integer): The unique `stock_id` of the stock.

#### Response:
Returns the stock details.

#### Example:
```json
{
  "stock_id": 1,
  "ticker": "AAPL",
  "name": "Apple Inc.",
  "sector": "Technology",
  "industry": "Consumer Electronics",
  "currency": "USD",
  "created_at": "2024-01-01T00:00:00Z"
}
```

### 4. `GET /stocks/{id}/data`
- **Description:** Retrieves all stock data for a specific stock (`stock_id`).
- **Parameters:**
    - **id** (integer): The unique `stock_id` of the stock.

#### Response:
Returns an array of stock data for the specified stock.

#### Example:
```json
[
  {
    "data_id": 1,
    "stock_id": 1,
    "date": "2024-01-01",
    "open_price": 150.25,
    "close_price": 155.30,
    "high_price": 157.00,
    "low_price": 148.80,
    "volume": 1200000,
    "created_at": "2024-01-01T00:00:00Z"
  },
  ...
]
```

### 5. `POST /stocks/{id}/data`
- **Description:** Adds new stock data for a specific stock (`stock_id`).
- **Parameters:**
    - **id** (integer): The unique `stock_id` of the stock.

- **Body:**  
Requires a JSON object with the following fields:
    - **date** (date): The quote date
    - **open_price** (decimal): Opening price
    - **close_price** (decimal): Closing price
    - **high_price** (decimal): Highest price
    - **low_price** (decimal): Lowest price
    - **volume** (bigint): Trading volume

#### Response:
Returns the created stock data record.

#### Example Request:
```json
{
  "date": "2024-01-02",
  "open_price": 156.20,
  "close_price": 160.00,
  "high_price": 162.00,
  "low_price": 155.10,
  "volume": 1500000
}
```

#### Example Response:
```json
{
  "data_id": 2,
  "stock_id": 1,
  "date": "2024-01-02",
  "open_price": 156.20,
  "close_price": 160.00,
  "high_price": 162.00,
  "low_price": 155.10,
  "volume": 1500000,
  "created_at": "2024-01-02T00:00:00Z"
}
```

### 6. `POST /users`
- **Description:** Creates a new user.

- **Body:**  
Requires a JSON object with the following fields:
    - **username** (string): Username
    - **email** (string): User email
    - **access_key** (string): Access key

#### Response:
Returns the created user record with its `user_id`.

#### Example Request:
```json
{
  "username": "Michael Burry",
  "email": "michael.burry@example.com",
  "access_key": "ef819ce1-2005-4e2d-b95e-8dd41bd215db"
}
```

#### Example Response:
```json
{
  "user_id": 1,
  "username": "Michael Burry",
  "email": "michael.burry@example.com",
  "access_key": "ef819ce1-2005-4e2d-b95e-8dd41bd215db",
  "created_at": "2024-01-01T00:00:00Z"
}
```

### 7. `GET /users/{id}`
- **Description:** Retrieves details of a specific user by `user_id`.
- **Parameters:**
    - **id** (integer): The unique `user_id` of the user.

#### Response:
Returns the user details.

#### Example:
```json
{
  "user_id": 1,
  "username": "Michael Burry",
  "email": "michael.burry@example.com",
  "access_key": "ef819ce1-2005-4e2d-b95e-8dd41bd215db",
  "created_at": "2024-01-01T00:00:00Z"
}
```

### 8. `POST /users/{id}/selections`
- **Description:** Allows a user to select a stock.

- **Parameters:**
    - **id** (integer): The unique `user_id` of the user.

- **Body:**  
Requires a JSON object with the following fields:
    - **stock_id** (integer): The `stock_id` of the selected stock.

#### Response:
Returns the created user selection record.

#### Example Request:
```json
{
  "stock_id": 1
}
```

#### Example Response:
```json
{
  "selection_id": 1,
  "user_id": 1,
  "stock_id": 1,
  "selected_at": "2024-01-01T00:00:00Z",
  "created_at": "2024-01-01T00:00:00Z"
}
```

### 9. `GET /user_selections`
- **Description:** Retrieves all selections made by users.

#### Response:
Returns an array of user selections.

#### Example:
```json
[
  {
    "selection_id": 1,
    "user_id": 1,
    "stock_id": 1,
    "selected_at": "2024-01-01T00:00:00Z",
    "created_at": "2024-01-01T00:00:00Z"
  },
  ...
]
```

## Authentication
Some endpoints may require authentication. Provide an `access_key` when making requests to the API.

This template includes the basic endpoints for the stock management system and its related functionality.