---
inclusion: always
---

# Coding Standards for Bhoj-ki-Khoj

## 🎯 General Principles

- Write clean, readable, and maintainable code
- Follow DRY (Don't Repeat Yourself) principle
- Keep functions small and focused (single responsibility)
- Use meaningful variable and function names
- Comment complex logic, not obvious code
- Prioritize code readability over cleverness

## 📝 TypeScript Standards

### Type Safety
```typescript
// ✅ Good: Explicit types
interface User {
  id: string;
  name: string;
  email: string;
  role: 'customer' | 'restaurant' | 'dabbawala' | 'admin';
}

function getUser(id: string): Promise<User> {
  // implementation
}

// ❌ Bad: Using 'any'
function getUser(id: any): any {
  // implementation
}
```

### Interfaces vs Types
```typescript
// ✅ Use interfaces for objects
interface Restaurant {
  id: string;
  name: string;
}

// ✅ Use types for unions, primitives, tuples
type OrderStatus = 'pending' | 'confirmed' | 'delivered';
type Coordinates = [number, number];
```

### Null Safety
```typescript
// ✅ Good: Handle null/undefined
const userName = user?.name ?? 'Guest';

// ❌ Bad: Assuming value exists
const userName = user.name;
```

## ⚛️ React Standards

### Component Structure
```typescript
// ✅ Good: Functional components with TypeScript
interface ButtonProps {
  label: string;
  onClick: () => void;
  variant?: 'primary' | 'secondary';
  disabled?: boolean;
}

export const Button: React.FC<ButtonProps> = ({ 
  label, 
  onClick, 
  variant = 'primary',
  disabled = false 
}) => {
  return (
    <button 
      onClick={onClick} 
      disabled={disabled}
      className={`btn btn-${variant}`}
    >
      {label}
    </button>
  );
};
```

### Hooks Best Practices
```typescript
// ✅ Good: Proper dependency arrays
useEffect(() => {
  fetchData(userId);
}, [userId]);

// ❌ Bad: Missing dependencies
useEffect(() => {
  fetchData(userId);
}, []);

// ✅ Good: Custom hooks for reusable logic
function useAuth() {
  const [user, setUser] = useState<User | null>(null);
  const [loading, setLoading] = useState(true);
  
  useEffect(() => {
    // auth logic
  }, []);
  
  return { user, loading };
}
```

### State Management
```typescript
// ✅ Good: Separate concerns
const [isLoading, setIsLoading] = useState(false);
const [error, setError] = useState<string | null>(null);
const [data, setData] = useState<Data[]>([]);

// ❌ Bad: Complex state object
const [state, setState] = useState({ isLoading: false, error: null, data: [] });
```

## 🎨 Styling Standards

### Tailwind CSS
```typescript
// ✅ Good: Utility classes, responsive design
<div className="flex flex-col md:flex-row gap-4 p-4">
  <div className="w-full md:w-1/2">Content</div>
</div>

// ✅ Good: Use cn() for conditional classes
import { cn } from '@/lib/utils';

<button className={cn(
  "px-4 py-2 rounded",
  isActive && "bg-blue-500",
  isDisabled && "opacity-50 cursor-not-allowed"
)}>
  Click me
</button>

// ❌ Bad: Inline styles
<div style={{ display: 'flex', padding: '16px' }}>Content</div>
```

### Component Variants
```typescript
// ✅ Good: Use class-variance-authority
import { cva } from 'class-variance-authority';

const buttonVariants = cva(
  "rounded font-medium transition-colors",
  {
    variants: {
      variant: {
        primary: "bg-blue-500 text-white hover:bg-blue-600",
        secondary: "bg-gray-200 text-gray-900 hover:bg-gray-300",
      },
      size: {
        sm: "px-3 py-1 text-sm",
        md: "px-4 py-2 text-base",
        lg: "px-6 py-3 text-lg",
      },
    },
    defaultVariants: {
      variant: "primary",
      size: "md",
    },
  }
);
```

## 📁 File Organization

### Naming Conventions
```
Components:     PascalCase     (UserProfile.tsx)
Utilities:      camelCase      (formatDate.ts)
Hooks:          camelCase      (useAuth.ts)
Constants:      UPPER_SNAKE    (API_ENDPOINTS.ts)
Types:          PascalCase     (User.ts)
```

### Import Order
```typescript
// 1. React and external libraries
import React, { useState, useEffect } from 'react';
import { useNavigate } from 'react-router-dom';

// 2. Internal components
import { Button } from '@/components/ui/button';
import { Navbar } from '@/components/Navbar';

// 3. Hooks and utilities
import { useAuth } from '@/hooks/useAuth';
import { formatDate } from '@/utils/formatDate';

// 4. Types
import type { User } from '@/types/user';

// 5. Styles (if any)
import './styles.css';
```
