# Multi-Level User Management System

A highly secure, full-stack **MEAN (MongoDB, Express.js, Angular, Node.js)** application designed to demonstrate robust authentication, a multi-tenant role-based user hierarchy, and a real-time financial transaction system.

This project was built to satisfy all mandatory and bonus requirements for a comprehensive machine test.

---

## 🌟 Key Features

### 1. Advanced Security & Authentication
*   **JWT in HTTP-Only Cookies:** Tokens are securely stored in HTTP-Only, SameSite cookies to prevent XSS attacks.
*   **Session-Based CAPTCHA:** Custom SVG CAPTCHA required for login. Expires securely after 5 minutes.
*   **Multi-Tenant Architecture:** Public registration is restricted to creating independent root `Admin` accounts. Standard `User` accounts must be created internally by their upline.
*   **Global Auth Interceptor:** Frontend automatically catches `401 Unauthorized` responses and logs the user out globally.
*   **Encrypted Passwords:** Passwords securely hashed via `bcrypt.js`.

### 2. Deep User Hierarchy (Role-Based Access)
*   **Admin Overrides:** 'Admin' users act as the root of their tree. They can view their entire global hierarchy and create next-level users.
*   **Strict Downline Scoping:** Standard Users can only view and manage their personal downline (users created directly or indirectly by them).
*   **Password Management:** Users and Admins can securely reset the passwords for any user within their downline hierarchy.
*   **Quick Actions:** The interactive Hierarchy tree features quick-action buttons to instantly transfer funds or reset passwords for specific users.

### 3. Financial & Balance Management
*   **Self-Recharging:** Admins have the privilege to securely mint/recharge their own balance.
*   **Deep Downline Transfers:** Standard Users can transfer funds to anyone in their deep downline. The amount is securely deducted from the sender.
*   **Admin Transfers:** If an Admin transfers funds deep into the hierarchy, the amount is automatically deducted from the recipient's immediate parent to maintain balance integrity.
*   **Detailed Statements:** View complete Transaction Statements (Date, Sender, Receiver, Amount, Commission) localized in Indian Rupees (₹).

### 4. Bonus Features Implemented
*   **Commission System:** Automated percentage commission distribution on transfers.
*   **Real-Time Data:** WebSockets (`Socket.io`) instantly push balance updates to the frontend dashboard without refreshing.
*   **Premium UI/UX:** Built with Angular Material, Tailwind CSS, custom "Glassmorphism", and highly optimized micro-animations for a snappy feel.
*   **Local Proxy Configuration:** Angular development server configured with a local proxy to securely support Incognito mode testing with First-Party cookies.
*   **Interactive Swagger Docs:** Auto-generated Swagger documentation for testing all backend REST APIs.

---

## 🛠️ Technology Stack
*   **Frontend:** Angular 20, Tailwind CSS, Angular Material, RxJS, Signals.
*   **Backend:** Node.js, Express.js, Socket.io, Swagger-JSDoc.
*   **Database:** MongoDB & Mongoose.

---

## 🚀 Getting Started (Local Development)

### Prerequisites
*   Node.js (v18+ recommended)
*   MongoDB installed locally or a MongoDB Atlas URI

### 1. Setup Backend
```bash
cd backend
npm install
```

Create a `.env` file in the `backend/` directory:
```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/user_management
JWT_SECRET=your_super_secret_key
JWT_EXPIRE=1d
JWT_REFRESH_SECRET=your_refresh_secret_key
JWT_REFRESH_EXPIRE=7d
COOKIE_EXPIRE=1
NODE_ENV=development
```

Start the backend:
```bash
npm run dev
```
*(The backend will run on `http://localhost:5000`. You can view the API documentation at `http://localhost:5000/api-docs`)*

### 2. Setup Frontend
```bash
cd frontend
npm install
```

Start the frontend:
```bash
npm start
```
> **Important:** Always use `npm start` (or `ng serve`) so the local Angular Proxy starts up. This proxy is required for the authentication cookies to work locally (especially in Incognito mode).

*(The frontend will run on `http://localhost:4200`)*

---

## 🧪 Testing the Application

1. **Register an Admin:** Go to the register page and create an account. This public registration automatically creates an independent **Admin** account.
2. **Login & CAPTCHA:** You will be redirected to the login page to verify your CAPTCHA.
3. **Recharge Wallet:** Log in as the Admin and use the "Self Recharge" button on the dashboard to add funds.
4. **Create Downline:** Create a standard "User" using the Create User form. You can log out, then log in as that new user to see their scoped permissions.
5. **Test Transfers:** Notice how balances update instantly (thanks to Socket.io) when transferring funds down the tree. Try using the quick action buttons in the Hierarchy tab!

---

## 📄 API Documentation
The backend includes a fully interactive Swagger UI. Once the server is running, navigate to:
`http://localhost:5000/api-docs`

This interface allows you to view schemas, exact request bodies, and test endpoints directly from the browser.
