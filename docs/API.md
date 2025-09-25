# Modern Banking App - API Documentation

Comprehensive RESTful API documentation for the Modern Banking App backend services.

## Overview

This document outlines the API endpoints, request/response formats, authentication methods, and usage examples for the Modern Banking App. The API follows REST principles and returns JSON responses.

## Base URL

```
Development: http://localhost:5000/api
Staging: https://staging-api.modern-banking.com/api
Production: https://api.modern-banking.com/api
```

## Authentication

The API uses JWT (JSON Web Tokens) for authentication. Include the token in the Authorization header:

```
Authorization: Bearer <your-jwt-token>
```

## Response Format

All API responses follow this standard format:

```json
{
  "success": true,
  "message": "Request processed successfully",
  "data": {},
  "meta": {
    "timestamp": "2025-09-25T18:27:00Z",
    "requestId": "req_abc123"
  }
}
```

## Error Handling

Error responses include appropriate HTTP status codes and detailed error information:

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Email is required",
    "details": [
      {
        "field": "email",
        "message": "Email field is required"
      }
    ]
  },
  "meta": {
    "timestamp": "2025-09-25T18:27:00Z",
    "requestId": "req_abc123"
  }
}
```

## API Endpoints

### Authentication Endpoints

#### Register User
- **POST** `/auth/register`
- **Description**: Register a new user account
- **Request Body**:
```json
{
  "email": "user@example.com",
  "password": "SecurePass123!",
  "firstName": "John",
  "lastName": "Doe",
  "phone": "+1234567890",
  "dateOfBirth": "1990-01-15",
  "accountType": "personal" // "personal" or "business"
}
```
- **Response**: User object with JWT token

#### Login User
- **POST** `/auth/login`
- **Description**: Authenticate user and return JWT token
- **Request Body**:
```json
{
  "email": "user@example.com",
  "password": "SecurePass123!"
}
```
- **Response**: Authentication token and user profile

#### Logout User
- **POST** `/auth/logout`
- **Description**: Invalidate current session
- **Headers**: Authorization required
- **Response**: Success confirmation

#### Refresh Token
- **POST** `/auth/refresh`
- **Description**: Refresh expired JWT token
- **Request Body**:
```json
{
  "refreshToken": "refresh_token_here"
}
```
- **Response**: New JWT token

#### Reset Password
- **POST** `/auth/reset`
- **Description**: Send password reset email
- **Request Body**:
```json
{
  "email": "user@example.com"
}
```
- **Response**: Reset confirmation

#### Verify Token
- **GET** `/auth/verify`
- **Description**: Verify JWT token validity
- **Headers**: Authorization required
- **Response**: Token status and user info

### User Management Endpoints

#### Get User Profile
- **GET** `/users/profile`
- **Description**: Get current user's profile information
- **Headers**: Authorization required
- **Response**: Complete user profile

#### Update User Profile
- **PUT** `/users/profile`
- **Description**: Update user profile information
- **Headers**: Authorization required
- **Request Body**:
```json
{
  "firstName": "John",
  "lastName": "Doe",
  "phone": "+1234567890",
  "address": {
    "street": "123 Main St",
    "city": "New York",
    "state": "NY",
    "zipCode": "10001",
    "country": "USA"
  }
}
```
- **Response**: Updated user profile

#### Get User Accounts
- **GET** `/users/accounts`
- **Description**: Get all accounts associated with the user
- **Headers**: Authorization required
- **Query Parameters**:
  - `type` (optional): Filter by account type (checking, savings, business)
  - `status` (optional): Filter by account status (active, inactive, suspended)
- **Response**: Array of account objects

#### Create New Account
- **POST** `/users/accounts`
- **Description**: Create a new bank account
- **Headers**: Authorization required
- **Request Body**:
```json
{
  "accountType": "checking", // "checking", "savings", "business"
  "accountName": "My Checking Account",
  "initialDeposit": 100.00,
  "currency": "USD"
}
```
- **Response**: New account details

#### Get Transaction History
- **GET** `/users/transactions`
- **Description**: Get user's transaction history
- **Headers**: Authorization required
- **Query Parameters**:
  - `accountId` (optional): Filter by specific account
  - `startDate` (optional): Start date filter (YYYY-MM-DD)
  - `endDate` (optional): End date filter (YYYY-MM-DD)
  - `type` (optional): Transaction type (debit, credit, transfer)
  - `category` (optional): Transaction category
  - `limit` (optional): Number of results (default: 50)
  - `offset` (optional): Pagination offset (default: 0)
- **Response**: Array of transaction objects

### Stock Trading Endpoints

#### Get Stock Quote
- **GET** `/stocks/quote/:symbol`
- **Description**: Get current stock price and details
- **Headers**: Authorization required
- **Parameters**:
  - `symbol`: Stock symbol (e.g., AAPL, GOOGL)
- **Response**: Stock quote with current price and market data

#### Get Historical Data
- **GET** `/stocks/history/:symbol`
- **Description**: Get historical stock price data
- **Headers**: Authorization required
- **Parameters**:
  - `symbol`: Stock symbol
- **Query Parameters**:
  - `range`: Time range (1d, 5d, 1m, 3m, 6m, 1y, 2y, 5y, max)
  - `interval`: Data interval (1m, 2m, 5m, 15m, 30m, 60m, 90m, 1h, 1d, 5d, 1wk, 1mo, 3mo)
- **Response**: Array of historical price data

#### Get User Portfolio
- **GET** `/stocks/portfolio`
- **Description**: Get user's stock portfolio
- **Headers**: Authorization required
- **Response**: Portfolio summary with holdings and performance

#### Execute Trade
- **POST** `/stocks/trade`
- **Description**: Execute a stock trade (buy/sell)
- **Headers**: Authorization required
- **Request Body**:
```json
{
  "symbol": "AAPL",
  "action": "buy", // "buy" or "sell"
  "quantity": 10,
  "orderType": "market", // "market" or "limit"
  "limitPrice": 150.00, // Required for limit orders
  "accountId": "acc_123456"
}
```
- **Response**: Trade confirmation and updated portfolio

#### Get Watchlist
- **GET** `/stocks/watchlist`
- **Description**: Get user's stock watchlist
- **Headers**: Authorization required
- **Response**: Array of watched stocks with current prices

#### Add to Watchlist
- **POST** `/stocks/watchlist`
- **Description**: Add stock to watchlist
- **Headers**: Authorization required
- **Request Body**:
```json
{
  "symbol": "AAPL",
  "notes": "Watching for entry point"
}
```
- **Response**: Updated watchlist

#### Remove from Watchlist
- **DELETE** `/stocks/watchlist/:symbol`
- **Description**: Remove stock from watchlist
- **Headers**: Authorization required
- **Parameters**:
  - `symbol`: Stock symbol to remove
- **Response**: Success confirmation

### Business Banking Endpoints

#### Get Business Profile
- **GET** `/business/profile`
- **Description**: Get business account profile
- **Headers**: Authorization required
- **Response**: Business profile information

#### Update Business Profile
- **PUT** `/business/profile`
- **Description**: Update business profile
- **Headers**: Authorization required
- **Request Body**: Business profile data
- **Response**: Updated business profile

#### Get Employees
- **GET** `/business/employees`
- **Description**: Get list of business employees
- **Headers**: Authorization required
- **Query Parameters**:
  - `department` (optional): Filter by department
  - `status` (optional): Filter by employee status
- **Response**: Array of employee objects

#### Add Employee
- **POST** `/business/employees`
- **Description**: Add new employee
- **Headers**: Authorization required
- **Request Body**: Employee information
- **Response**: New employee details

#### Process Payroll
- **POST** `/business/payroll`
- **Description**: Process payroll for employees
- **Headers**: Authorization required
- **Request Body**: Payroll processing parameters
- **Response**: Payroll processing results

## Rate Limiting

API requests are rate-limited to prevent abuse:

- **General endpoints**: 100 requests per 15 minutes per IP
- **Authentication endpoints**: 5 requests per minute per IP
- **Trading endpoints**: 10 requests per minute per user

## SDKs and Libraries

- **JavaScript/Node.js**: `@modern-banking/api-client`
- **Python**: `modern-banking-python`
- **React**: `@modern-banking/react-hooks`
- **PHP**: `modern-banking/php-sdk`

## WebSocket Events

Real-time updates via WebSocket connection:

```javascript
const ws = new WebSocket('wss://api.modern-banking.com/ws');

// Subscribe to account updates
ws.send(JSON.stringify({
  type: 'subscribe',
  channel: 'account.updates',
  accountId: 'acc_123456'
}));
```

### Available Channels:
- `account.updates`: Account balance and transaction updates
- `stock.prices`: Real-time stock price updates
- `portfolio.changes`: Portfolio value changes
- `notifications`: System notifications

## Testing

### Postman Collection
Import our Postman collection for easy API testing:
```
https://api.modern-banking.com/postman-collection.json
```

### Test Environment
```
Base URL: https://api-test.modern-banking.com/api
Test User: testuser@example.com
Test Password: TestPass123!
```

## Support

For API support:
- **Documentation**: [https://docs.modern-banking.com](https://docs.modern-banking.com)
- **Status Page**: [https://status.modern-banking.com](https://status.modern-banking.com)
- **Developer Portal**: [https://developers.modern-banking.com](https://developers.modern-banking.com)
- **Support Email**: api-support@modern-banking.com
- **Discord Community**: [https://discord.gg/modern-banking](https://discord.gg/modern-banking)

## Changelog

### v1.2.0 (2025-09-25)
- Added business banking endpoints
- Enhanced stock trading with limit orders
- Improved error handling and validation
- WebSocket support for real-time updates

### v1.1.0 (2025-09-01)
- Added stock trading endpoints
- Portfolio management features
- Watchlist functionality
- Rate limiting improvements

### v1.0.0 (2025-08-01)
- Initial API release
- User authentication and management
- Basic banking operations
- Account management
