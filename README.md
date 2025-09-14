# 🛒 E-Commerce Frontend ↔ Backend Routes Documentation

This document maps **frontend routes** in the React app to the **backend APIs** required.  
It also explains **purpose, authentication needs, and expected backend behavior**.

---

## 🚀 1. Public Routes (No Authentication Required)

| Frontend Route | Purpose | Backend API | Explanation |
|----------------|---------|-------------|-------------|
| `/` | Homepage | `GET /api/home` | Featured products, categories, banners. |
| `/login` | Login page | `POST /api/auth/login` | Accepts email/password → returns JWT. |
| `/signup` | User registration | `POST /api/auth/register` | Creates new user. |
| `/forgot-password` | Reset password | `POST /api/auth/forgot-password` | Sends OTP or reset link. |
| `/2fa` | 2FA verification | `POST /api/auth/verify-2fa` | Confirms OTP. |
| `/verifyemail` | Email verification | `POST /api/auth/verify-email` | Verifies email token. |
| `/authgoogle` | Google OAuth login | `POST /api/auth/google` | OAuth login flow. |
| `/products` | Product listing | `GET /api/products` | Supports filters, search, pagination. |
| `/product/:id` | Single product page | `GET /api/products/:id` | Detailed product info. |
| `/cart` | Shopping cart | `GET /api/cart`, `POST /api/cart`, `DELETE /api/cart/:id` | Add/remove/view cart items. |
| `/checkout` | Checkout | `POST /api/orders` | Place order from cart. |
| `/order-tracking` | Track order | `GET /api/orders/track/:id` | Track status by order ID. |
| `/order` | User orders | `GET /api/orders/user` | Fetch logged-in user’s orders. |

---

## 🔐 2. Protected Routes (Require Authentication)

### 🛠️ Admin Portal (`/admin/...`)

| Frontend Route | Backend API | Explanation |
|----------------|-------------|-------------|
| `/admin` | `GET /api/admin/summary` | Dashboard stats. |
| `/admin/users` | `GET /api/admin/users` | Manage users. |
| `/admin/sellers` | `GET /api/admin/sellers` | Manage sellers. |
| `/admin/analytics` | `GET /api/admin/analytics` | Analytics data. |
| `/admin/requests` | `GET /api/admin/requests`, `POST /api/admin/requests/:id/approve`, `POST /api/admin/requests/:id/deny` | Seller approvals. |
| `/admin/settings` | `PATCH /api/admin/settings` | Admin settings update. |

---

### 🛒 Buyer Portal

| Frontend Route | Backend API | Explanation |
|----------------|-------------|-------------|
| `/buyer` | `GET /api/buyer/profile`, `GET /api/orders/user` | Buyer dashboard: profile + orders. |

---

### 🏪 Vendor Portal

| Frontend Route | Backend API | Explanation |
|----------------|-------------|-------------|
| `/vendor` | `GET /api/seller/profile`, `GET /api/seller/products`, `POST /api/seller/products`, `PATCH /api/seller/products/:id` | Seller dashboard: product management. |

---

### 💬 Chat System

| Frontend Route | Backend API | Explanation |
|----------------|-------------|-------------|
| `/chat` | `GET /api/chat/:conversationId`, `POST /api/chat/message` | Messaging between users, sellers, and admin. |

---

## 🔑 3. Authentication Notes

- Use **JWT tokens** (Access + Refresh).
- Protect `/admin`, `/buyer`, `/vendor`, `/chat` with **auth middleware**.
- Google OAuth (`/authgoogle`) should map to internal user + return JWT.

---

## ⚙️ 4. Backend Guidelines

- Response format:  
  ```json
  { "success": true, "data": {}, "message": "OK" }
