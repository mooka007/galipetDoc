# 📱 Gali'Pet Mobile App

## 📋 Summary
Cross-platform mobile application (iOS & Android) for pet owners and professionals to book services, manage pets, chat in real-time, and access marketplace. Built with React Native for code reuse across platforms.

---


## 🧪 Testing the Mobile App

### **Test Accounts:**

#### Pet Owner Account:
```
Email:    owner@galipet.com
Password: Owner1234!
```

#### Professional Account:
```
Email:    professional@galipet.com
Password: Professional1234!
```

### **Owner Quick Start:**
1. Open app and select "Login"
2. Enter owner email & password
3. Allow location permissions
4. Browse nearby professionals on map
5. Click professional to view profile & services
6. Select service, date, and time
7. Complete payment with test card: `4242 4242 4242 4242`
8. View booking confirmation
9. Chat with professional in real-time
10. Leave review after service completion

### **Professional Quick Start:**
1. Open app and select "Login"
2. Enter professional email & password
3. View pending booking requests on dashboard
4. Confirm or decline bookings
5. Chat with pet owners
6. Set availability schedule
7. View earnings and completed bookings
8. Receive push notifications for new requests

### **Test Features:**
- Real-time chat with Socket.IO
- Location-based professional search
- Secure payment processing (Stripe test mode)
- Push notifications (Firebase)
- Booking lifecycle management
- Professional ratings & reviews
- Pet profile management
- Marketplace browsing & ordering

### **Test Payment Card (Stripe):**
```
Card Number: 4242 4242 4242 4242
Expiry:      Any future date (e.g., 12/25)
CVC:         Any 3 digits (e.g., 123)
```

---

## 🛠️ Tech Stack

| Technology | Version | Purpose |
|---|---|---|
| **React Native** | 0.73.x | Cross-platform mobile framework |
| **Expo** | 52.x | Managed React Native platform |
| **Expo Router** | 3.x | File-based routing (like Next.js) |
| **TypeScript** | 5.x | Type-safe code |
| **Zustand** | 4.x | Lightweight state management |
| **TanStack Query** | 5.x | Server state & caching |
| **Socket.IO** | 4.x | Real-time chat & notifications |
| **NativeWind** | 4.x | Tailwind CSS for React Native |
| **Stripe RN SDK** | Latest | Payment processing |
| **Firebase Admin SDK** | Latest | Push notifications (FCM) |
| **Expo Location** | Latest | GPS & geolocation |
| **React Native Maps** | Latest | Map display & location search |

---

## 🎯 Why These Dependencies?

- **React Native**: Write once, deploy to iOS & Android (code reuse)
- **Expo**: Managed platform eliminates native build complexity
- **Expo Router**: File-based routing simplifies navigation structure
- **TypeScript**: Catch errors before runtime
- **Zustand**: Minimal boilerplate for global state (auth, UI)
- **TanStack Query**: Automatic caching & background refetching
- **Socket.IO**: Real-time bidirectional communication for chat
- **NativeWind**: Consistent styling with Tailwind utilities
- **Stripe RN SDK**: Secure payment processing
- **Firebase**: Push notifications for bookings & messages
- **Expo Location & Maps**: Location-based service discovery

---

## 📱 How It Works (Step-by-Step)

### **Pet Owner Flow:**
1. **User opens app** → Expo loads JavaScript bundle
2. **User logs in** → Credentials sent to backend
3. **JWT token received** → Stored in secure storage (Zustand + MMKV)
4. **Home screen loads** → TanStack Query fetches nearby professionals
5. **User searches** → Map displays professionals with filters
6. **User selects professional** → Views profile, services, availability
7. **User books service** → Stripe payment intent created
8. **Payment processed** → Booking confirmed, notification sent
9. **Real-time chat** → Socket.IO connects to chat server
10. **Service day arrives** → Firebase push notification reminder (24h, 1h before)
11. **Service completed** → User leaves review & rating

### **Professional Flow:**
1. **Professional logs in** → Dashboard shows pending bookings
2. **Booking request arrives** → Real-time notification via Socket.IO
3. **Professional confirms** → Booking status updated, owner notified
4. **Chat with owner** → Socket.IO real-time messaging
5. **Service completed** → Mark as complete, receive payment
6. **View earnings** → Dashboard shows monthly revenue

---

## 🎨 App Screens

| Screen | Purpose |
|---|---|
| **Auth** | Login, register, OTP verification |
| **Home (Owner)** | Nearby professionals, search, filters |
| **Professional Detail** | Profile, services, availability, reviews |
| **Booking** | Calendar, time slots, payment |
| **Chat** | Real-time messaging with professionals |
| **Pets** | Pet profile management |
| **Marketplace** | Product browsing, cart, checkout |
| **Orders** | Order history, tracking |
| **Dashboard (Pro)** | Pending bookings, earnings, schedule |
| **Notifications** | In-app notification center |

---

## 🔄 Real-Time Features

- **Chat**: Socket.IO bidirectional messaging
- **Notifications**: Firebase FCM push notifications
- **Typing Indicators**: Real-time "user is typing" status
- **Online Status**: See if professional is available
- **Live Updates**: Booking status changes in real-time

---

## 💳 Payment Flow

1. User selects service & date
2. Stripe payment intent created on backend
3. Stripe RN SDK opens payment sheet
4. User enters card details (secure)
5. Payment processed
6. Backend webhook confirms payment
7. Booking created & notifications sent

---

## 📦 Installation & Running

```bash
cd galipet-mobile
npm install
npx expo start          # Start dev server
npx expo start --ios    # Run on iOS simulator
npx expo start --android # Run on Android emulator
npm run build           # Production build
```

---

## 🚀 Key Features

- ✅ Cross-platform (iOS & Android)
- ✅ Real-time chat with Socket.IO
- ✅ Location-based professional search
- ✅ Secure payment processing (Stripe)
- ✅ Push notifications (Firebase)
- ✅ Offline support (cached data)
- ✅ Native performance with Expo

---

_Built with React Native + Expo for iOS & Android_ 🚀
