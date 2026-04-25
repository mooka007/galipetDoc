# 📊 Gali'Pet Admin Dashboard

## 📋 Summary
Web-based admin control panel for managing users, professionals, bookings, orders, and marketplace. Real-time data visualization with charts, tables, and analytics.

---

## 🛠️ Tech Stack

| Technology | Version | Purpose |
|---|---|---|
| **React** | 18.x | UI library for dashboard components |
| **Vite** | 5.x | Fast build tool & dev server |
| **TypeScript** | 5.x | Type-safe code |
| **TanStack Query** | 5.x | Server state management & caching |
| **React Router** | 6.x | Navigation between dashboard pages |
| **Axios** | 1.x | HTTP client for API calls |
| **Tailwind CSS** | 3.x | Responsive styling |

---

## 🎯 Why These Dependencies?

- **React**: Component-based UI for complex dashboards
- **Vite**: Instant dev server, fast HMR for rapid development
- **TypeScript**: Prevent runtime errors in data handling
- **TanStack Query**: Automatic caching, refetching, and synchronization of server data
- **React Router**: Multi-page dashboard navigation
- **Axios**: Simplified HTTP requests with interceptors for auth tokens
- **Tailwind CSS**: Consistent, responsive design system

---

## 📱 How It Works (Step-by-Step)

1. **Admin logs in** → Credentials sent to backend API
2. **JWT token received** → Stored in localStorage/sessionStorage
3. **Dashboard loads** → TanStack Query fetches overview data
4. **Data displayed** → Charts, tables, and stat cards render
5. **Real-time updates** → Query auto-refetches every 30 seconds
6. **Admin clicks menu** → React Router navigates to new page
7. **Page data loads** → TanStack Query caches results for fast navigation
8. **Admin performs action** → API call sent with JWT token in header
9. **Response received** → Query cache invalidated, UI updates automatically

---

## 🎨 Dashboard Pages

| Page | Purpose |
|---|---|
| **Overview** | KPIs, recent bookings, revenue charts, booking status distribution |
| **Users** | User management, verification, account status |
| **Professionals** | Professional profiles, verification, ratings, availability |
| **Bookings** | Booking management, status tracking, cancellations |
| **Orders** | Marketplace orders, fulfillment tracking |
| **Products** | Inventory management, pricing, stock levels |

---

## 📊 Key Features

- ✅ Real-time data updates (auto-refetch)
- ✅ Interactive charts (pie, bar, line)
- ✅ Responsive tables with sorting/filtering
- ✅ JWT authentication with token refresh
- ✅ Role-based access control
- ✅ Dark/light theme support

---

## 📦 Installation & Running

```bash
cd dashboard
npm install
npm run dev      # Start dev server
npm run build    # Production build
npm run preview  # Preview production build
```

---

## 🔐 Authentication Flow

1. Admin enters email + password
2. Backend validates credentials
3. Backend returns `accessToken` (15min) + `refreshToken` (7d)
4. Tokens stored in browser
5. All API requests include `Authorization: Bearer {accessToken}`
6. If token expires, `refreshToken` automatically gets new `accessToken`

---
