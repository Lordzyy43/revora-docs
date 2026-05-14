# Revora Documentation

Revora adalah web application untuk booking, tracking, dan management service kendaraan. Repository ini digunakan sebagai pusat dokumentasi resmi untuk menjaga kesesuaian antara frontend dan backend.

Repository dokumentasi ini menjadi **single source of truth** untuk:

- Product Requirement Document
- Database schema
- API contract
- Authentication flow
- Role permission
- Frontend routes
- Backend endpoint behavior
- Technical decision log
- Development workflow

---

## 1. Repository Overview

Revora dikembangkan menggunakan tiga repository terpisah:

```txt
revora-client   -> React frontend
revora-api      -> Laravel backend
revora-docs     -> Project documentation and API contract
```

Tujuan pemisahan repository:

1. Frontend dan backend dapat dikembangkan secara mandiri.
2. Dokumentasi menjadi acuan bersama sebelum implementasi fitur.
3. API contract dapat disepakati lebih awal.
4. Risiko mismatch antara frontend dan backend dapat dikurangi.
5. Project lebih mudah dipresentasikan sebagai portfolio fullstack profesional.

---

## 2. Project Vision

Revora bukan hanya website bengkel biasa. Revora diarahkan sebagai **Smart Automotive Service Platform** yang membantu customer melakukan booking service kendaraan, memantau progress service, dan mengelola riwayat kendaraan.

Core value Revora:

```txt
Book, track, and manage your car service in one place.
```

Fokus MVP:

- Customer dapat mengelola kendaraan.
- Customer dapat melakukan booking service.
- Customer dapat memantau status service.
- Admin dapat mengelola booking.
- Admin dapat mengelola layanan service.
- Sistem memiliki role-based access.

---

## 3. Documentation Structure

Struktur folder dokumentasi:

```txt
revora-docs/
├── README.md
├── prd/
│   └── revora-prd.md
├── api/
│   ├── auth.md
│   ├── vehicles.md
│   ├── services.md
│   ├── bookings.md
│   └── admin.md
├── database/
│   ├── erd.md
│   └── schema.md
├── frontend/
│   ├── routes.md
│   ├── pages.md
│   └── components.md
├── backend/
│   ├── setup.md
│   ├── endpoints.md
│   └── auth-flow.md
└── decisions/
    └── technical-decisions.md
```

---

## 4. Documentation Rules

Dokumentasi harus diperbarui ketika:

1. Ada fitur baru.
2. Ada perubahan endpoint API.
3. Ada perubahan request body.
4. Ada perubahan response API.
5. Ada perubahan database schema.
6. Ada perubahan role permission.
7. Ada perubahan frontend route.
8. Ada keputusan teknis baru.

Prinsip utama:

> If it affects frontend, backend, database, or user flow, document it here first.

---

## 5. Tech Stack

### Frontend

```txt
React
Vite
TypeScript
Tailwind CSS
React Router
Axios
TanStack Query
Zustand / Context API
Framer Motion
```

### Backend

```txt
Laravel
Laravel Sanctum
Eloquent ORM
REST API
Form Request Validation
API Resource
Middleware / Policy
MySQL / PostgreSQL
```

### Deployment Target

```txt
Frontend : Vercel / Netlify
Backend  : Railway / Render / VPS
Database : Supabase / Railway / Neon / MySQL hosting
```

---

## 6. Development Environment

Revora menggunakan beberapa environment:

```txt
local       -> development di laptop
staging     -> testing sebelum production
production  -> aplikasi live
```

File `.env` tidak boleh di-commit.

Yang boleh di-commit:

```txt
.env.example
```

Contoh frontend environment:

```txt
VITE_API_BASE_URL=http://localhost:8000/api
```

Contoh backend environment:

```txt
APP_NAME=Revora
APP_ENV=local
APP_URL=http://localhost:8000
FRONTEND_URL=http://localhost:5173
DB_DATABASE=revora
```

---

## 7. Branching Convention

Branch utama:

```txt
main       -> stable branch
develop    -> integration branch
feature/*  -> new feature development
fix/*      -> bug fixing
chore/*    -> config, docs, dependency, or maintenance
```

Contoh branch:

```txt
feature/auth-api
feature/customer-vehicles
feature/booking-flow
feature/admin-booking-management
fix/login-validation
chore/update-docs-structure
```

---

## 8. Commit Convention

Gunakan commit message yang jelas dan konsisten.

Format umum:

```txt
type: short description
```

Tipe commit:

```txt
feat     -> fitur baru
fix      -> perbaikan bug
docs     -> perubahan dokumentasi
style    -> perubahan style tanpa mengubah logic
refactor -> perubahan struktur kode tanpa mengubah behavior
chore    -> konfigurasi, dependency, maintenance
test     -> testing
```

Contoh:

```txt
feat: add vehicle API contract
feat: add customer booking flow documentation
fix: update booking response status field
docs: add authentication flow
chore: update documentation folder structure
```

---

## 9. API Contract Standard

Semua API contract harus memiliki format berikut:

```txt
Feature Name
Description
Role Access
Endpoint
Method
Headers
Request Body
Success Response
Error Response
Validation Rules
Frontend Notes
Backend Notes
```

Contoh singkat:

```txt
Feature      : Create Vehicle
Role         : Customer
Method       : POST
Endpoint     : /api/vehicles
Auth         : Required
Description  : Customer creates a new vehicle data.
```

Request body:

```json
{
  "brand": "Toyota",
  "model": "Avanza",
  "year": 2020,
  "plate_number": "AD 1234 XX",
  "transmission_type": "automatic",
  "fuel_type": "gasoline",
  "last_odometer": 45000
}
```

Success response:

```json
{
  "success": true,
  "message": "Vehicle created successfully",
  "data": {
    "id": 1,
    "brand": "Toyota",
    "model": "Avanza",
    "year": 2020,
    "plate_number": "AD 1234 XX",
    "transmission_type": "automatic",
    "fuel_type": "gasoline",
    "last_odometer": 45000
  }
}
```

Error response:

```json
{
  "success": false,
  "message": "Validation failed",
  "errors": {
    "plate_number": ["The plate number field is required."]
  }
}
```

---

## 10. API Response Convention

Backend harus mengirim response dengan pola konsisten.

### Success Response

```json
{
  "success": true,
  "message": "Request successful",
  "data": {}
}
```

### Success Response with List Data

```json
{
  "success": true,
  "message": "Data retrieved successfully",
  "data": [],
  "meta": {
    "current_page": 1,
    "per_page": 10,
    "total": 100
  }
}
```

### Error Response

```json
{
  "success": false,
  "message": "Something went wrong",
  "errors": null
}
```

### Validation Error Response

```json
{
  "success": false,
  "message": "Validation failed",
  "errors": {
    "field_name": ["Error message"]
  }
}
```

---

## 11. Naming Convention

### Database

Gunakan `snake_case`.

Contoh:

```txt
plate_number
booking_date
booking_time
created_at
updated_at
```

### API Response

Untuk MVP, API response mengikuti Laravel convention yaitu `snake_case`.

Contoh:

```json
{
  "plate_number": "AD 1234 XX",
  "booking_date": "2026-05-14"
}
```

### Frontend

Frontend boleh menggunakan `camelCase` di dalam komponen dan logic internal.

Contoh:

```ts
const plateNumber = vehicle.plate_number;
const bookingDate = booking.booking_date;
```

Catatan:

Jika diperlukan, mapping dari `snake_case` ke `camelCase` dilakukan di service layer atau mapper, bukan di setiap component.

---

## 12. Role Access Summary

### Customer

Customer dapat:

- Mengelola kendaraan miliknya sendiri.
- Membuat booking service.
- Melihat booking miliknya sendiri.
- Melihat tracking status service miliknya sendiri.

Customer tidak dapat:

- Mengakses dashboard admin.
- Melihat data customer lain.
- Mengubah status booking.
- Mengelola layanan service.

### Admin

Admin dapat:

- Melihat semua booking.
- Melihat detail booking.
- Mengubah status booking.
- Mengelola layanan service.
- Melihat data customer.
- Melihat statistik dashboard.

### Mechanic

Mechanic belum menjadi prioritas MVP. Role ini disiapkan untuk fase lanjutan.

---

## 13. MVP Feature List

Fitur MVP:

```txt
Landing Page
Register Customer
Login Customer
Login Admin
Customer Dashboard
Vehicle Management
Service List
Booking Service
Booking History
Booking Detail Tracking
Admin Dashboard
Admin Booking Management
Admin Service Management
Role-Based Access
```

Fitur yang belum masuk MVP:

```txt
AI Diagnostic
Payment Gateway
Marketplace Sparepart
WhatsApp Notification
Email Notification
Invoice PDF
Multi-branch Workshop
Full Mechanic Dashboard
Advanced Analytics
Real-time Tracking
```

---

## 14. Development Flow

Alur kerja setiap fitur:

```txt
1. Define feature requirement in docs
2. Define database impact
3. Define API contract
4. Implement backend endpoint
5. Test backend endpoint
6. Implement frontend UI
7. Connect frontend to backend
8. Handle loading, empty, and error state
9. Manual test full flow
10. Update documentation
```

Prinsip:

> Documentation first, implementation second.

---

## 15. Definition of Done

Sebuah fitur dianggap selesai jika:

1. Requirement sudah tertulis.
2. API contract sudah tersedia.
3. Database impact sudah jelas.
4. Backend endpoint sudah dibuat.
5. Backend validation sudah dibuat.
6. Authorization sudah aman.
7. Frontend UI sudah dibuat.
8. Frontend sudah terhubung ke API.
9. Loading state tersedia.
10. Empty state tersedia jika dibutuhkan.
11. Error state tersedia.
12. Manual test sudah dilakukan.
13. Dokumentasi sudah diperbarui.

---

## 16. Technical Decision Log

Setiap keputusan teknis penting harus dicatat di:

```txt
decisions/technical-decisions.md
```

Format keputusan:

```txt
# Decision Title

Date:
Status: Proposed / Accepted / Rejected / Changed

## Context
Penjelasan masalah atau kebutuhan.

## Decision
Keputusan yang diambil.

## Reason
Alasan keputusan.

## Consequence
Dampak dari keputusan.
```

Contoh keputusan yang perlu dicatat:

- Menggunakan Laravel sebagai backend.
- Menggunakan React Vite TypeScript sebagai frontend.
- Menggunakan Laravel Sanctum untuk auth.
- Menggunakan `snake_case` untuk API response.
- Memisahkan repository frontend, backend, dan documentation.

---

## 17. Production Mindset

Revora dikembangkan dengan mindset production-ready.

Artinya, target project bukan hanya:

```txt
fitur jalan
```

Tetapi juga:

```txt
fitur jelas
kode rapi
API konsisten
database terstruktur
auth aman
role tidak bocor
error handling jelas
dokumentasi sinkron
mudah dideploy
mudah dilanjutkan
```

Prinsip utama:

> Build small, document clearly, integrate carefully, and polish consistently.

---

## 18. Next Documentation Tasks

Dokumentasi berikutnya yang perlu dibuat:

1. `prd/revora-prd.md`
2. `database/schema.md`
3. `database/erd.md`
4. `api/auth.md`
5. `api/vehicles.md`
6. `api/services.md`
7. `api/bookings.md`
8. `api/admin.md`
9. `frontend/routes.md`
10. `backend/auth-flow.md`

Prioritas pertama setelah README:

```txt
database/schema.md
```

Alasannya, database schema akan menjadi dasar untuk migration Laravel, model, relationship, API resource, dan frontend type.
