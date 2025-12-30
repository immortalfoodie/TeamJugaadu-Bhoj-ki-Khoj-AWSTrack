# User Flows

## 🧑 Customer User Flow

### 1. Registration & Login
```
Start
  ↓
Landing Page
  ↓
Click "Sign Up"
  ↓
Enter Details (Name, Email, Phone, Password)
  ↓
Verify Email
  ↓
Complete Profile
  ↓
Add Delivery Address
  ↓
Home Page
```

### 2. Browse & Order Flow
```
Home Page
  ↓
Browse Restaurants
  ├─→ Search by Name/Cuisine
  ├─→ Filter (Veg/Non-veg, Rating, Distance)
  └─→ Sort (Rating, Distance, Price)
  ↓
Select Restaurant
  ↓
View Menu
  ↓
Select Items
  ├─→ View Item Details
  ├─→ Add Special Instructions
  └─→ Add to Cart
  ↓
Review Cart
  ├─→ Modify Quantities
  ├─→ Remove Items
  └─→ Apply Coupon (future)
  ↓
Proceed to Checkout
  ↓
Select/Add Delivery Address
  ↓
Choose Payment Method
  ↓
Place Order
  ↓
Order Confirmation
  ↓
Track Order
  ├─→ View Status Updates
  ├─→ View Dabbawala Location (future)
  └─→ Contact Support
  ↓
Order Delivered
  ↓
Rate & Review (optional)
```

### 3. Order Tracking Flow
```
Order Placed
  ↓
Restaurant Confirmed
  ↓
Preparing Food
  ↓
Ready for Pickup
  ↓
Dabbawala Assigned
  ↓
Picked Up
  ↓
In Transit
  ├─→ View Map
  ├─→ View ETA
  └─→ Contact Dabbawala
  ↓
Delivered
  ↓
Complete
```

---

## 🍳 Restaurant User Flow

### 1. Registration & Onboarding
```
Start
  ↓
Sign Up as Restaurant
  ↓
Enter Business Details
  ├─→ Restaurant Name
  ├─→ Cuisine Type
  ├─→ Address & Location
  ├─→ Contact Details
  └─→ Business Documents
  ↓
Admin Verification (pending)
  ↓
Approved
  ↓
Complete Profile
  ├─→ Upload Photos
  ├─→ Set Operating Hours
  └─→ Set Delivery Radius
  ↓
Restaurant Dashboard
```

### 2. Menu Management Flow
```
Dashboard
  ↓
Menu Management
  ↓
Add New Item
  ├─→ Item Name
  ├─→ Description
  ├─→ Price
  ├─→ Category
  ├─→ Upload Photo
  ├─→ Dietary Info (Veg/Non-veg/Vegan)
  └─→ Preparation Time
  ↓
Save Item
  ↓
Manage Existing Items
  ├─→ Edit Item
  ├─→ Mark Available/Unavailable
  └─→ Delete Item
```

### 3. Order Management Flow
```
New Order Notification
  ↓
View Order Details
  ├─→ Customer Info
  ├─→ Items Ordered
  ├─→ Delivery Address
  └─→ Special Instructions
  ↓
Accept/Reject Order
  ↓
If Accepted:
  ↓
Update Status: Preparing
  ↓
Update Status: Ready for Pickup
  ↓
Dabbawala Assigned (automatic)
  ↓
Dabbawala Picks Up
  ↓
Order Delivered
  ↓
View Feedback (if any)
```

---

## 🚲 Dabbawala User Flow

### 1. Registration & Onboarding
```
Start
  ↓
Sign Up as Dabbawala
  ↓
Enter Personal Details
  ├─→ Name
  ├─→ Phone
  ├─→ Email
  ├─→ Vehicle Type
  └─→ Service Area
  ↓
Upload Documents
  ├─→ ID Proof
  ├─→ Vehicle Registration
  └─→ Driving License
  ↓
Admin Verification
  ↓
Approved
  ↓
Dabbawala Dashboard
```

### 2. Delivery Assignment Flow
```
Dashboard
  ↓
View Available Orders
  ↓
Order Auto-Assigned (based on location)
  ↓
Accept Assignment
  ↓
View Order Details
  ├─→ Pickup Location
  ├─→ Delivery Location
  ├─→ Customer Contact
  └─→ Order Items
  ↓
View Route Map
  ├─→ Pickup Point
  ├─→ Delivery Point
  └─→ Optimized Route
  ↓
Start Navigation
```

### 3. Delivery Execution Flow
```
Heading to Pickup
  ↓
Update Status: At Pickup Location
  ↓
Collect Order from Restaurant
  ↓
Verify Items
  ↓
Update Status: Picked Up
  ↓
Start Delivery
  ↓
Update Status: In Transit
  ↓
Navigate to Customer
  ↓
Update Status: At Delivery Location
  ↓
Hand Over to Customer
  ↓
Update Status: Delivered
  ↓
Upload Delivery Proof (optional)
  ↓
Complete Delivery
  ↓
View Earnings
```

---

## 🛠️ Admin User Flow

### 1. Dashboard Overview
```
Admin Login
  ↓
Dashboard
  ├─→ Total Users
  ├─→ Total Restaurants
  ├─→ Total Dabbawalas
  ├─→ Total Orders
  ├─→ Revenue
  └─→ Active Orders
```

### 2. User Management Flow
```
Users Section
  ↓
View All Users
  ├─→ Filter by Role
  ├─→ Search by Name/Email
  └─→ Sort by Date
  ↓
Select User
  ↓
View User Details
  ├─→ Profile Info
  ├─→ Order History
  └─→ Activity Log
  ↓
Actions
  ├─→ Edit User
  ├─→ Suspend User
  ├─→ Delete User
  └─→ Reset Password
```

### 3. Restaurant Approval Flow
```
Restaurant Management
  ↓
View Pending Approvals
  ↓
Select Restaurant
  ↓
Review Details
  ├─→ Business Info
  ├─→ Documents
  └─→ Location
  ↓
Verify Information
  ↓
Approve/Reject
  ├─→ If Approved: Send Notification
  └─→ If Rejected: Provide Reason
```

### 4. Order Monitoring Flow
```
Order Management
  ↓
View All Orders
  ├─→ Filter by Status
  ├─→ Filter by Date
  └─→ Search by Order ID
  ↓
Select Order
  ↓
View Order Details
  ├─→ Customer Info
  ├─→ Restaurant Info
  ├─→ Dabbawala Info
  ├─→ Items
  ├─→ Timeline
  └─→ Payment Status
  ↓
Actions
  ├─→ Cancel Order
  ├─→ Reassign Dabbawala
  ├─→ Issue Refund
  └─→ Contact Parties
```

### 5. Analytics Flow
```
Analytics Section
  ↓
Select Report Type
  ├─→ Revenue Report
  ├─→ User Growth
  ├─→ Order Trends
  ├─→ Restaurant Performance
  └─→ Dabbawala Efficiency
  ↓
Select Date Range
  ↓
View Charts & Graphs
  ↓
Export Report (CSV/PDF)
```

---

## 🔄 Common Flows

### Password Reset Flow
```
Login Page
  ↓
Click "Forgot Password"
  ↓
Enter Email
  ↓
Receive Reset Link
  ↓
Click Link
  ↓
Enter New Password
  ↓
Confirm Password
  ↓
Password Updated
  ↓
Login with New Password
```

### Profile Update Flow
```
Dashboard
  ↓
Click Profile
  ↓
Edit Profile
  ├─→ Update Name
  ├─→ Update Phone
  ├─→ Update Photo
  └─→ Update Address
  ↓
Save Changes
  ↓
Confirmation
```

### Notification Flow
```
Event Occurs
  ├─→ New Order
  ├─→ Status Update
  ├─→ Delivery Assigned
  └─→ Order Delivered
  ↓
Generate Notification
  ↓
Send to User
  ├─→ In-App Notification
  ├─→ Email (future)
  └─→ SMS (future)
  ↓
User Views Notification
  ↓
Navigate to Relevant Page
```

---

## 📱 Mobile-Specific Flows (Future)

### Quick Reorder Flow
```
Order History
  ↓
Select Previous Order
  ↓
Click "Reorder"
  ↓
Review Cart
  ↓
Modify if Needed
  ↓
Place Order
```

### Voice Order Flow (Future)
```
Home Page
  ↓
Click Voice Icon
  ↓
Speak Order
  ↓
AI Processes Request
  ↓
Confirm Items
  ↓
Place Order
```

### Scan QR Code Flow (Future)
```
At Restaurant
  ↓
Scan QR Code
  ↓
View Menu
  ↓
Order for Dine-in/Takeaway
  ↓
Pay & Collect
```
