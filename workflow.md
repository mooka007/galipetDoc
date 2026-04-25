# 🔧 Gali'Pet Backend API

## 📋 Summary
Node.js REST API + WebSocket server powering the entire Gali'Pet ecosystem. Handles authentication, bookings, payments, real-time chat, notifications, and marketplace operations.

---

## 🛠️ Tech Stack

| Technology | Version | Purpose |
|---|---|---|
| **Node.js** | 20 LTS | JavaScript runtime |
| **Express.js** | 5.x | HTTP framework & routing |
| **TypeScript** | 5.x | Type-safe backend code |
| **PostgreSQL** | 15 | Primary relational database |
| **Prisma ORM** | 5.x | Database abstraction & migrations |
| **Redis** | 7.x | Session cache, rate limiting, OTP storage |
| **Socket.IO** | 4.x | Real-time bidirectional communication |
| **JWT** | Latest | Stateless authentication tokens |
| **bcryptjs** | Latest | Password hashing |
| **Stripe** | Latest | Payment processing |
| **Firebase Admin SDK** | Latest | Push notifications (FCM) |
| **Twilio** | Latest | SMS OTP verification |
| **Cloudinary** | Latest | Image storage & CDN |
| **Nodemailer** | Latest | Transactional emails |
| **node-cron** | Latest | Scheduled jobs (reminders) |
| **Helmet** | Latest | HTTP security headers |
| **express-rate-limit** | Latest | API rate limiting |
| **Zod** | Latest | Runtime request validation |

---

## 🎯 Why These Dependencies?

| Dependency | Why Used |
|---|---|
| **Express.js** | Lightweight, flexible HTTP framework |
| **Prisma** | Type-safe DB queries, auto-migrations, excellent DX |
| **PostgreSQL** | Reliable relational database, ACID compliance |
| **Redis** | Fast in-memory cache, session storage, rate limiting |
| **Socket.IO** | Real-time chat, typing indicators, online status |
| **JWT** | Stateless auth, no server session storage needed |
| **bcryptjs** | Secure password hashing with salt |
| **Stripe** | Industry-standard payment processing |
| **Firebase** | Push notifications for iOS & Android |
| **Twilio** | SMS OTP for phone verification |
| **Cloudinary** | Image hosting, CDN, automatic optimization |
| **Nodemailer** | Send transactional emails (confirmations, resets) |
| **node-cron** | Schedule appointment reminders (24h, 1h before) |
| **Helmet** | Prevent common security vulnerabilities |
| **express-rate-limit** | Prevent brute-force attacks, API abuse |
| **Zod** | Validate request data at runtime |

---

## 📊 Database Models

| Model | Purpose |
|---|---|
| **User** | Pet owners, professionals, admins |
| **Professional** | Service provider profiles |
| **Service** | Services offered by professionals |
| **Availability** | Weekly schedule per professional |
| **Pet** | Pet profiles owned by users |
| **Booking** | Appointments between owner & professional |
| **Review** | Star ratings & comments |
| **Conversation** | Chat threads between users |
| **Message** | Individual chat messages |
| **Notification** | In-app notifications with FCM metadata |
| **Payment** | Stripe payment records |
| **Product** | Marketplace items |
| **Order** | Purchase orders |
| **OrderItem** | Line items within orders |

---

## 🔄 How It Works (Step-by-Step)

### **Authentication Flow:**
1. User sends email + password to `/api/v1/auth/login`
2. Backend validates credentials with bcryptjs
3. Backend generates JWT tokens:
   - `accessToken` (15min) - for API requests
   - `refreshToken` (7d) - for getting new accessToken
4. Tokens returned to client
5. Client includes `Authorization: Bearer {accessToken}` in all requests
6. Backend verifies JWT signature & expiration
7. If accessToken expired, client uses refreshToken to get new one

### **Booking Flow:**
1. User selects professional, service, date, time
2. Backend checks availability (no conflicts)
3. Stripe payment intent created
4. Client processes payment
5. Backend receives Stripe webhook confirmation
6. Booking created in database
7. Firebase push notification sent to professional
8. Socket.IO emits real-time update to both users
9. Scheduled cron job sends reminders (24h, 1h before)

### **Real-Time Chat Flow:**
1. User connects to Socket.IO server with JWT token
2. Socket.IO middleware verifies JWT
3. User joins conversation room
4. Message sent → Socket.IO broadcasts to other user
5. Message saved to database
6. Firebase push notification sent if recipient offline
7. Typing indicator sent in real-time

### **Payment Flow:**
1. User initiates booking payment
2. Backend creates Stripe payment intent
3. Client opens Stripe payment sheet
4. User enters card details (handled by Stripe, not backend)
5. Stripe processes payment
6. Stripe sends webhook to backend
7. Backend verifies webhook signature
8. Backend updates booking status to CONFIRMED
9. Notifications sent to both parties

### **Marketplace Flow:**
1. User browses products
2. Backend returns paginated product list
3. User adds items to cart (client-side)
4. User checks out
5. Backend creates order with atomic stock decrement
6. Payment processed via Stripe
7. Order confirmation sent via email & push notification
8. Admin notified of new order

---

## 🔐 Security Features

- ✅ JWT authentication with refresh tokens
- ✅ Password hashing with bcryptjs (salt rounds: 12)
- ✅ Rate limiting (prevent brute-force attacks)
- ✅ Helmet security headers
- ✅ Zod input validation (prevent injection attacks)
- ✅ CORS configuration
- ✅ Stripe webhook signature verification
- ✅ Socket.IO JWT authentication

---

## 📦 Installation & Running

```bash
cd Server
npm install
npx prisma migrate dev    # Run migrations
npx prisma db seed        # Seed admin user
npm run dev               # Start dev server
npm run build             # Production build
npm start                 # Run production
```

---

## 🚀 API Endpoints Summary

```
POST   /api/v1/auth/register
POST   /api/v1/auth/login
POST   /api/v1/auth/refresh
POST   /api/v1/auth/logout
POST   /api/v1/auth/verify-otp

GET    /api/v1/professionals
POST   /api/v1/professionals
PUT    /api/v1/professionals/:id

GET    /api/v1/bookings
POST   /api/v1/bookings
PUT    /api/v1/bookings/:id/confirm
PUT    /api/v1/bookings/:id/cancel

POST   /api/v1/payments/create-intent
POST   /api/v1/payments/webhook

GET    /api/v1/pets
POST   /api/v1/pets
PUT    /api/v1/pets/:id

POST   /api/v1/reviews
GET    /api/v1/reviews/professional/:id

GET    /api/v1/chat/conversations
POST   /api/v1/chat/conversations/:userId
GET    /api/v1/chat/conversations/:id/messages

GET    /api/v1/marketplace/products
POST   /api/v1/marketplace/orders
GET    /api/v1/marketplace/orders

GET    /health
```

---

## 🔌 WebSocket Events

```
socket.on('message:send')        → Send chat message
socket.on('typing:start')        → User typing indicator
socket.on('typing:stop')         → Stop typing
socket.on('notification:new')    → New notification
socket.on('booking:updated')     → Booking status changed
```

---

_Built with Node.js + Express for scalable, real-time API_ ⚡
