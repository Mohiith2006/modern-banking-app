# Modern Banking App - Frontend

This is the frontend application for the Modern Banking App, built with React 18, Vite, and TypeScript.

## 🚀 Quick Start

### Prerequisites
- Node.js 18 or higher
- npm or yarn

### Installation

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

## 🏗️ Project Structure

```
frontend/
├── public/                 # Static assets
│   ├── vite.svg           # Vite logo
│   └── favicon.ico        # App favicon
├── src/
│   ├── components/        # Reusable UI components
│   │   ├── common/        # Common components (Header, Footer, etc.)
│   │   ├── forms/         # Form components
│   │   └── ui/            # Basic UI elements (Button, Input, etc.)
│   ├── modules/           # Feature-specific modules
│   │   ├── personal/      # Personal banking module
│   │   ├── business/      # Business banking module
│   │   └── stocks/        # Stock simulator module
│   ├── hooks/             # Custom React hooks
│   ├── services/          # API service functions
│   ├── utils/             # Utility functions
│   ├── store/             # State management (Zustand/Redux)
│   ├── types/             # TypeScript type definitions
│   ├── styles/            # Global styles and themes
│   ├── assets/            # Images, icons, etc.
│   ├── App.tsx            # Main App component
│   ├── main.tsx           # Entry point
│   └── vite-env.d.ts      # Vite type definitions
├── index.html             # HTML template
├── package.json           # Dependencies and scripts
├── vite.config.ts         # Vite configuration
├── tsconfig.json          # TypeScript configuration
├── tailwind.config.js     # Tailwind CSS configuration
└── README.md              # This file
```

## 🛠️ Technology Stack

- **React 18** - UI library with concurrent features
- **Vite** - Fast build tool and dev server
- **TypeScript** - Type safety and better DX
- **Tailwind CSS** - Utility-first CSS framework
- **React Router** - Client-side routing
- **React Query** - Data fetching and caching
- **Zustand** - Lightweight state management
- **React Hook Form** - Form handling
- **Zod** - Schema validation
- **Firebase SDK** - Authentication and database

## 📱 Features

### Core Features
- ✅ Responsive design (mobile-first)
- ✅ Dark/light theme support
- ✅ Progressive Web App (PWA)
- ✅ TypeScript support
- ✅ Hot module replacement (HMR)
- ✅ Code splitting and lazy loading
- ✅ SEO optimization
- ✅ Accessibility (WCAG 2.1 AA)

### Banking Modules
- 💳 **Personal Banking** - Account management, transactions, budgeting
- 🏢 **Business Banking** - Corporate accounts, payroll, analytics
- 📈 **Stock Simulator** - Virtual trading, portfolio management

## 🚀 Available Scripts

```bash
# Development
npm run dev          # Start development server
npm run build        # Build for production
npm run preview      # Preview production build

# Testing
npm run test         # Run tests
npm run test:ui      # Run tests with UI
npm run test:coverage # Generate coverage report

# Code Quality
npm run lint         # Run ESLint
npm run lint:fix     # Fix ESLint issues
npm run format       # Format code with Prettier
npm run type-check   # Run TypeScript compiler check
```

## 🌐 Environment Variables

Create a `.env.local` file in the frontend directory:

```env
# API Configuration
VITE_API_URL=http://localhost:3001/api

# Firebase Configuration
VITE_FIREBASE_API_KEY=your_api_key
VITE_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
VITE_FIREBASE_APP_ID=your_app_id

# Feature Flags
VITE_ENABLE_STOCK_SIMULATOR=true
VITE_ENABLE_BUSINESS_BANKING=true
VITE_ENABLE_AI_INSIGHTS=true
```

## 🎨 Styling Guidelines

### Tailwind CSS
- Use Tailwind utility classes for styling
- Create custom components for reusable patterns
- Follow mobile-first responsive design principles

### Component Structure
```tsx
// Component example
export interface ComponentProps {
  // Define props with TypeScript
}

export const Component: React.FC<ComponentProps> = ({ ...props }) => {
  return (
    <div className="container mx-auto px-4">
      {/* Component content */}
    </div>
  )
}
```

## 🧪 Testing

- **Unit Tests** - Vitest + React Testing Library
- **Integration Tests** - Cypress
- **E2E Tests** - Playwright

## 🚀 Deployment

### Vercel (Recommended)
```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel
```

### Netlify
```bash
# Build command
npm run build

# Publish directory
dist
```

### Docker
```bash
# Build Docker image
docker build -t modern-banking-frontend .

# Run container
docker run -p 3000:3000 modern-banking-frontend
```

## 🤝 Contributing

1. Follow the established code style (ESLint + Prettier)
2. Write tests for new features
3. Update documentation as needed
4. Use conventional commits

## 📚 Resources

- [React Documentation](https://reactjs.org/)
- [Vite Documentation](https://vitejs.dev/)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [React Router Documentation](https://reactrouter.com/)
