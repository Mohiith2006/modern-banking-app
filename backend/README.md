# Modern Banking App - Backend

Node.js and Express.js backend server for the Modern Banking App with TypeScript support, Firebase integration, and external API connections.

## 🚀 Quick Start

### Prerequisites

- **Node.js 18+** (LTS recommended)
- **npm** or **yarn** package manager
- **Firebase** project with Admin SDK configured
- **API Keys** for external services (Gemini, Stock APIs)

### Installation

```bash
# Navigate to backend directory
cd backend

# Install dependencies
npm install

# Copy environment variables
cp ../.env.example .env

# Configure your .env file with:
# - Firebase Admin SDK credentials
# - Gemini API key
# - Stock API credentials
# - JWT secrets

# Start development server
npm run dev
```

## 🛠️ Technology Stack

- **Runtime**: Node.js 18+
- **Framework**: Express.js
- **Language**: TypeScript
- **Authentication**: Firebase Admin SDK
- **Database**: Firebase Firestore
- **External APIs**: 
  - Gemini API (AI features)
  - Stock Market API (real-time data)
- **Validation**: Express Validator
- **Security**: Helmet, CORS, Rate Limiting

## 📁 Project Structure

```
backend/
├── src/
│   ├── controllers/     # Request handlers
│   │   ├── auth.ts     # Authentication controller
│   │   ├── users.ts    # User management controller
│   │   └── stocks.ts   # Stock data controller
│   ├── services/       # Business logic layer
│   │   ├── authService.ts    # Authentication service
│   │   ├── userService.ts    # User operations service
│   │   └── stockService.ts   # Stock data service
│   ├── middleware/     # Custom middleware
│   │   ├── auth.ts     # JWT authentication middleware
│   │   ├── validation.ts     # Request validation
│   │   └── errorHandler.ts   # Global error handling
│   ├── routes/         # API route definitions
│   │   ├── auth.ts     # Authentication routes
│   │   ├── users.ts    # User management routes
│   │   └── stocks.ts   # Stock API routes
│   ├── models/         # Data models and types
│   │   ├── User.ts     # User model
│   │   ├── Account.ts  # Account model
│   │   └── Stock.ts    # Stock model
│   ├── config/         # Configuration files
│   │   ├── firebase.ts # Firebase Admin setup
│   │   ├── database.ts # Database configuration
│   │   └── api.ts      # API clients setup
│   ├── utils/          # Utility functions
│   │   ├── logger.ts   # Logging utilities
│   │   ├── validators.ts # Data validation helpers
│   │   └── helpers.ts  # General helper functions
│   └── app.ts          # Express application setup
├── tests/              # Test files
├── package.json        # Dependencies and scripts
├── tsconfig.json       # TypeScript configuration
├── .env.example        # Environment variables template
└── README.md           # This file
```

## 📜 Available Scripts

```bash
# Development
npm run dev          # Start development server with nodemon
npm run dev:debug    # Start with debugging enabled

# Production
npm run build        # Compile TypeScript to JavaScript
npm run start        # Start production server
npm run start:prod   # Start with PM2 for production

# Testing
npm run test         # Run test suite
npm run test:watch   # Run tests in watch mode
npm run test:coverage # Generate test coverage report

# Code Quality
npm run lint         # Run ESLint
npm run lint:fix     # Fix linting issues
npm run format       # Format code with Prettier
npm run type-check   # TypeScript type checking

# Database
npm run db:seed      # Seed database with sample data
npm run db:reset     # Reset database (development only)
```

## 🔧 Environment Variables

Copy `.env.example` to `.env` and configure:

```env
# Server Configuration
PORT=5000
NODE_ENV=development
CORS_ORIGIN=http://localhost:3000

# Firebase Admin SDK
FIREBASE_PROJECT_ID=your-project-id
FIREBASE_PRIVATE_KEY_ID=your-private-key-id
FIREBASE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n"
FIREBASE_CLIENT_EMAIL=your-client-email
FIREBASE_CLIENT_ID=your-client-id
FIREBASE_AUTH_URI=https://accounts.google.com/o/oauth2/auth
FIREBASE_TOKEN_URI=https://oauth2.googleapis.com/token

# JWT Configuration
JWT_SECRET=your-super-secret-jwt-key
JWT_EXPIRE_TIME=24h
REFRESH_TOKEN_SECRET=your-refresh-token-secret

# External APIs
GEMINI_API_KEY=your-gemini-api-key
GEMINI_API_ENDPOINT=https://api.gemini.com
STOCK_API_KEY=your-stock-api-key
STOCK_API_ENDPOINT=https://api.stockmarket.com

# Security
RATE_LIMIT_MAX=100
RATE_LIMIT_WINDOW=15
BCRYPT_ROUNDS=12
```

## 🔐 Authentication & Authorization

### Firebase Admin SDK
- Server-side user authentication
- Custom JWT token generation
- Role-based access control
- Session management

### Security Features
- Password hashing with bcrypt
- JWT token-based authentication
- Rate limiting on API endpoints
- Input validation and sanitization
- CORS protection
- Helmet security headers

## 🏗️ Service Architecture

### Authentication Service (`src/services/authService.ts`)
```typescript
export class AuthService {
  // User registration
  async registerUser(userData: RegisterData): Promise<User>
  
  // User login
  async loginUser(credentials: LoginData): Promise<AuthResponse>
  
  // JWT token verification
  async verifyToken(token: string): Promise<DecodedToken>
  
  // Password reset
  async resetPassword(email: string): Promise<void>
}
```

### User Service (`src/services/userService.ts`)
```typescript
export class UserService {
  // Get user profile
  async getUserProfile(userId: string): Promise<UserProfile>
  
  // Update user information
  async updateUser(userId: string, data: UpdateUserData): Promise<User>
  
  // Account management
  async getAccounts(userId: string): Promise<Account[]>
  async createAccount(userId: string, accountData: CreateAccountData): Promise<Account>
}
```

### Stock Service (`src/services/stockService.ts`)
```typescript
export class StockService {
  // Get real-time stock data
  async getStockPrice(symbol: string): Promise<StockData>
  
  // Get historical data
  async getHistoricalData(symbol: string, range: string): Promise<HistoricalData[]>
  
  // Portfolio management
  async getPortfolio(userId: string): Promise<Portfolio>
  async executeTrade(userId: string, tradeData: TradeData): Promise<Trade>
}
```

## 📊 API Endpoints

### Authentication Routes
```
POST   /api/auth/register     # User registration
POST   /api/auth/login        # User login
POST   /api/auth/logout       # User logout
POST   /api/auth/refresh      # Refresh JWT token
POST   /api/auth/reset        # Password reset
GET    /api/auth/verify       # Verify token
```

### User Management Routes
```
GET    /api/users/profile     # Get user profile
PUT    /api/users/profile     # Update user profile
GET    /api/users/accounts    # Get user accounts
POST   /api/users/accounts    # Create new account
GET    /api/users/transactions # Get transaction history
```

### Stock Trading Routes
```
GET    /api/stocks/quote/:symbol      # Get stock quote
GET    /api/stocks/history/:symbol    # Get historical data
GET    /api/stocks/portfolio          # Get user portfolio
POST   /api/stocks/trade              # Execute trade
GET    /api/stocks/watchlist          # Get watchlist
POST   /api/stocks/watchlist          # Add to watchlist
```

## 🧪 Testing

### Test Structure
```
tests/
├── unit/           # Unit tests
│   ├── services/   # Service layer tests
│   ├── models/     # Model tests
│   └── utils/      # Utility function tests
├── integration/    # Integration tests
│   ├── auth.test.ts
│   ├── users.test.ts
│   └── stocks.test.ts
└── fixtures/       # Test data fixtures
```

### Running Tests
```bash
# Run all tests
npm test

# Run specific test file
npm test -- auth.test.ts

# Run tests with coverage
npm run test:coverage

# Run tests in watch mode
npm run test:watch
```

## 🚀 Deployment

### Development
```bash
npm run dev
```

### Production Build
```bash
# Build the application
npm run build

# Start production server
npm run start
```

### Docker Deployment
```bash
# From project root
docker-compose up backend
```

### Environment-Specific Configurations
- **Development**: Hot reload, detailed logging, debug mode
- **Staging**: Production build, limited logging, performance monitoring
- **Production**: Optimized build, error-only logging, full monitoring

## 📝 API Documentation

- **Swagger/OpenAPI**: Available at `/api-docs` when server is running
- **Postman Collection**: Import from `/docs/api-collection.json`
- **API Reference**: Detailed documentation in `/docs/API.md`

## 🔍 Logging & Monitoring

- **Winston Logger**: Structured logging with multiple transports
- **Request Logging**: All API requests logged with response times
- **Error Tracking**: Centralized error handling and logging
- **Performance Metrics**: API response times and system metrics

## 🛡️ Security Best Practices

- Input validation on all endpoints
- SQL injection prevention
- XSS protection
- Rate limiting
- CORS configuration
- Security headers (Helmet)
- Environment variable protection
- Firebase security rules

## 🤝 Contributing

1. Follow TypeScript strict mode guidelines
2. Write unit tests for new features
3. Update API documentation
4. Follow the established code style (ESLint + Prettier)
5. Ensure all tests pass before submitting PR

## 📞 Support

For backend-specific issues:
- Check server logs: `npm run logs`
- Run health check: `GET /api/health`
- Review API documentation
- Check Firebase console for authentication issues
