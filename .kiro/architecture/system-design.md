# System Architecture

## 🏗️ High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        Frontend Layer                        │
│                    React.js + TypeScript                     │
│              Tailwind CSS + shadcn/ui Components             │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                     Authentication Layer                     │
│                      Firebase Auth                           │
│              (Role-based access control)                     │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                      Backend Services                        │
│                                                               │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   Supabase   │  │   Maps API   │  │  Firebase    │      │
│  │  (Database)  │  │  (Location)  │  │   (Auth)     │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└─────────────────────────────────────────────────────────────┘
```

## 📦 Component Architecture

### Frontend Structure
```
src/
├── components/          # Reusable UI components
│   ├── auth/           # Authentication components
│   ├── ui/             # shadcn/ui components
│   └── shared/         # Shared components
├── pages/              # Page components
│   ├── customer/       # Customer pages
│   ├── restaurant/     # Restaurant pages
│   ├── dabbawala/      # Dabbawala pages
│   └── admin/          # Admin pages
├── layouts/            # Layout components
├── context/            # React Context providers
├── hooks/              # Custom React hooks
├── utils/              # Utility functions
├── types/              # TypeScript types
└── integrations/       # External service integrations
```

## 🔄 Data Flow

### Order Placement Flow
```
Customer → Browse Menu → Add to Cart → Checkout
    ↓
Place Order → Supabase (Create Order)
    ↓
Notify Restaurant → Restaurant Accepts
    ↓
Assign Dabbawala → Dabbawala Picks Up
    ↓
Delivery in Progress → Customer Tracking
    ↓
Delivered → Order Complete
```

### Authentication Flow
```
User Login → Firebase Auth → Get User Role
    ↓
Role-based Redirect:
├── Customer → Home Page
├── Restaurant → Restaurant Dashboard
├── Dabbawala → Delivery Dashboard
└── Admin → Admin Dashboard
```

## 🗄️ Database Architecture

### Supabase Tables
- **users** - User profiles and roles
- **restaurants** - Restaurant/chef information
- **menu_items** - Food items and pricing
- **orders** - Order details and status
- **order_items** - Individual items in orders
- **deliveries** - Delivery assignments and tracking
- **reviews** - Customer reviews and ratings
- **addresses** - Customer delivery addresses

## 🔐 Security Architecture

### Authentication
- Firebase Authentication for user management
- JWT tokens for session management
- Role-based access control (RBAC)

### Authorization
- Protected routes based on user roles
- API-level permission checks
- Row-level security in Supabase

### Data Protection
- Environment variables for sensitive keys
- HTTPS for all communications
- Input validation and sanitization
- SQL injection prevention via Supabase

## 🚀 Deployment Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                         Vercel CDN                           │
│                    (Static Asset Hosting)                    │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                      React Application                       │
│                    (Client-Side Rendering)                   │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    External Services                         │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   Supabase   │  │   Firebase   │  │   Maps API   │      │
│  │   (Cloud)    │  │   (Cloud)    │  │   (Cloud)    │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└─────────────────────────────────────────────────────────────┘
```

## 📊 State Management

### Context Providers
- **AuthContext** - User authentication state
- **CartContext** - Shopping cart state
- **ThemeContext** - UI theme preferences

### React Query
- Server state management
- Caching and synchronization
- Optimistic updates
- Background refetching

## 🔌 API Integration

### Supabase Client
- Real-time subscriptions
- CRUD operations
- File storage
- Row-level security

### Firebase Services
- Authentication
- User management
- Password reset
- Email verification

### Maps API
- Geocoding
- Route calculation
- Distance matrix
- Place search
