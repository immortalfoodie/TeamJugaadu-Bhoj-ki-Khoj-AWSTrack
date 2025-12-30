# Data Models

## 📊 Database Schema

### Users Table
```typescript
interface User {
  id: string;                    // UUID (Primary Key)
  email: string;                 // Unique
  name: string;
  phone: string;
  role: 'customer' | 'restaurant' | 'dabbawala' | 'admin';
  avatar_url?: string;
  created_at: timestamp;
  updated_at: timestamp;
  is_active: boolean;
  firebase_uid: string;          // Firebase Auth UID
}
```

### Restaurants Table
```typescript
interface Restaurant {
  id: string;                    // UUID (Primary Key)
  user_id: string;               // Foreign Key → users.id
  name: string;
  description: string;
  cuisine_type: string[];
  address: string;
  latitude: number;
  longitude: number;
  phone: string;
  image_url?: string;
  rating: number;                // Average rating
  is_verified: boolean;
  is_active: boolean;
  opening_time: time;
  closing_time: time;
  delivery_radius: number;       // in kilometers
  commission_rate: number;       // percentage
  created_at: timestamp;
  updated_at: timestamp;
}
```

### Menu Items Table
```typescript
interface MenuItem {
  id: string;                    // UUID (Primary Key)
  restaurant_id: string;         // Foreign Key → restaurants.id
  name: string;
  description: string;
  price: number;
  category: string;              // e.g., 'Main Course', 'Dessert'
  image_url?: string;
  is_vegetarian: boolean;
  is_vegan: boolean;
  is_gluten_free: boolean;
  is_available: boolean;
  preparation_time: number;      // in minutes
  calories?: number;
  allergens?: string[];
  created_at: timestamp;
  updated_at: timestamp;
}
```

### Orders Table
```typescript
interface Order {
  id: string;                    // UUID (Primary Key)
  customer_id: string;           // Foreign Key → users.id
  restaurant_id: string;         // Foreign Key → restaurants.id
  dabbawala_id?: string;         // Foreign Key → users.id
  order_number: string;          // Unique order number
  status: OrderStatus;
  total_amount: number;
  delivery_fee: number;
  tax_amount: number;
  discount_amount: number;
  final_amount: number;
  payment_method: 'cash' | 'online' | 'wallet';
  payment_status: 'pending' | 'completed' | 'failed' | 'refunded';
  delivery_address: string;
  delivery_latitude: number;
  delivery_longitude: number;
  delivery_instructions?: string;
  estimated_delivery_time: timestamp;
  actual_delivery_time?: timestamp;
  created_at: timestamp;
  updated_at: timestamp;
}

type OrderStatus = 
  | 'pending'           // Order placed, awaiting restaurant confirmation
  | 'confirmed'         // Restaurant confirmed
  | 'preparing'         // Food being prepared
  | 'ready'             // Ready for pickup
  | 'assigned'          // Dabbawala assigned
  | 'picked_up'         // Dabbawala picked up
  | 'in_transit'        // On the way to customer
  | 'delivered'         // Successfully delivered
  | 'cancelled'         // Order cancelled
  | 'rejected';         // Restaurant rejected
```

### Order Items Table
```typescript
interface OrderItem {
  id: string;                    // UUID (Primary Key)
  order_id: string;              // Foreign Key → orders.id
  menu_item_id: string;          // Foreign Key → menu_items.id
  quantity: number;
  unit_price: number;
  total_price: number;
  special_instructions?: string;
  created_at: timestamp;
}
```

### Addresses Table
```typescript
interface Address {
  id: string;                    // UUID (Primary Key)
  user_id: string;               // Foreign Key → users.id
  label: string;                 // e.g., 'Home', 'Office'
  address_line1: string;
  address_line2?: string;
  city: string;
  state: string;
  postal_code: string;
  latitude: number;
  longitude: number;
  is_default: boolean;
  created_at: timestamp;
  updated_at: timestamp;
}
```

### Deliveries Table
```typescript
interface Delivery {
  id: string;                    // UUID (Primary Key)
  order_id: string;              // Foreign Key → orders.id
  dabbawala_id: string;          // Foreign Key → users.id
  pickup_address: string;
  pickup_latitude: number;
  pickup_longitude: number;
  delivery_address: string;
  delivery_latitude: number;
  delivery_longitude: number;
  status: DeliveryStatus;
  distance: number;              // in kilometers
  estimated_time: number;        // in minutes
  actual_time?: number;
  pickup_time?: timestamp;
  delivery_time?: timestamp;
  delivery_proof_url?: string;   // Photo proof
  created_at: timestamp;
  updated_at: timestamp;
}

type DeliveryStatus = 
  | 'assigned'
  | 'heading_to_pickup'
  | 'at_pickup'
  | 'picked_up'
  | 'in_transit'
  | 'at_delivery'
  | 'delivered'
  | 'failed';
```

### Reviews Table
```typescript
interface Review {
  id: string;                    // UUID (Primary Key)
  order_id: string;              // Foreign Key → orders.id
  customer_id: string;           // Foreign Key → users.id
  restaurant_id: string;         // Foreign Key → restaurants.id
  rating: number;                // 1-5
  food_rating: number;
  delivery_rating: number;
  comment?: string;
  images?: string[];
  is_verified: boolean;
  created_at: timestamp;
  updated_at: timestamp;
}
```

### Feedback Table
```typescript
interface Feedback {
  id: string;                    // UUID (Primary Key)
  user_id: string;               // Foreign Key → users.id
  type: 'bug' | 'feature' | 'complaint' | 'suggestion';
  subject: string;
  message: string;
  status: 'open' | 'in_progress' | 'resolved' | 'closed';
  priority: 'low' | 'medium' | 'high';
  admin_response?: string;
  created_at: timestamp;
  updated_at: timestamp;
}
```

## 🔗 Relationships

```
users (1) ──────────── (many) restaurants
users (1) ──────────── (many) orders (as customer)
users (1) ──────────── (many) orders (as dabbawala)
users (1) ──────────── (many) addresses
users (1) ──────────── (many) reviews

restaurants (1) ────── (many) menu_items
restaurants (1) ────── (many) orders
restaurants (1) ────── (many) reviews

orders (1) ──────────── (many) order_items
orders (1) ──────────── (1) delivery
orders (1) ──────────── (1) review

menu_items (1) ────── (many) order_items
```

## 📈 Indexes

### Performance Optimization
```sql
-- Users
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_role ON users(role);
CREATE INDEX idx_users_firebase_uid ON users(firebase_uid);

-- Restaurants
CREATE INDEX idx_restaurants_user_id ON restaurants(user_id);
CREATE INDEX idx_restaurants_location ON restaurants USING GIST(
  ll_to_earth(latitude, longitude)
);

-- Menu Items
CREATE INDEX idx_menu_items_restaurant_id ON menu_items(restaurant_id);
CREATE INDEX idx_menu_items_category ON menu_items(category);

-- Orders
CREATE INDEX idx_orders_customer_id ON orders(customer_id);
CREATE INDEX idx_orders_restaurant_id ON orders(restaurant_id);
CREATE INDEX idx_orders_dabbawala_id ON orders(dabbawala_id);
CREATE INDEX idx_orders_status ON orders(status);
CREATE INDEX idx_orders_created_at ON orders(created_at DESC);

-- Order Items
CREATE INDEX idx_order_items_order_id ON order_items(order_id);
CREATE INDEX idx_order_items_menu_item_id ON order_items(menu_item_id);

-- Deliveries
CREATE INDEX idx_deliveries_order_id ON deliveries(order_id);
CREATE INDEX idx_deliveries_dabbawala_id ON deliveries(dabbawala_id);
CREATE INDEX idx_deliveries_status ON deliveries(status);
```

## 🔒 Row Level Security (RLS)

### Supabase RLS Policies

```sql
-- Users can only read their own data
CREATE POLICY "Users can view own profile"
  ON users FOR SELECT
  USING (auth.uid() = firebase_uid);

-- Restaurants can manage their own menu
CREATE POLICY "Restaurants can manage own menu"
  ON menu_items FOR ALL
  USING (restaurant_id IN (
    SELECT id FROM restaurants WHERE user_id = auth.uid()
  ));

-- Customers can view their own orders
CREATE POLICY "Customers can view own orders"
  ON orders FOR SELECT
  USING (customer_id = auth.uid());

-- Dabbawalas can view assigned orders
CREATE POLICY "Dabbawalas can view assigned orders"
  ON orders FOR SELECT
  USING (dabbawala_id = auth.uid());

-- Admins can view all data
CREATE POLICY "Admins have full access"
  ON ALL TABLES FOR ALL
  USING (
    EXISTS (
      SELECT 1 FROM users 
      WHERE firebase_uid = auth.uid() 
      AND role = 'admin'
    )
  );
```
