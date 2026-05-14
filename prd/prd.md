# Product Requirement Document (PRD)

## Revora — Automotive Service Management Platform

### 1. Informasi Dokumen

| Item            | Keterangan                                                 |
| --------------- | ---------------------------------------------------------- |
| Nama Produk     | Revora                                                     |
| Jenis Produk    | Website / Web App Booking dan Management Service Kendaraan |
| Platform        | Web                                                        |
| Target Pengguna | Customer, Admin, Mechanic                                  |
| Frontend        | React + Vite + TypeScript                                  |
| Backend         | Laravel REST API                                           |
| Database        | MySQL / PostgreSQL                                         |
| Auth            | Laravel Sanctum                                            |
| Arsitektur Repo | Separate Repository: Frontend, Backend, dan Documentation  |
| Status Dokumen  | Draft v0.1                                                 |

---

## 2. Latar Belakang

Banyak proses service kendaraan masih dilakukan secara manual, mulai dari pelanggan datang langsung ke bengkel, bertanya jadwal kosong, menunggu konfirmasi, hingga tidak adanya informasi yang jelas mengenai progress pengerjaan kendaraan.

Revora dirancang sebagai platform digital untuk membantu customer melakukan booking service kendaraan, memantau status pengerjaan, dan mengelola riwayat service. Di sisi bengkel, admin dapat mengelola layanan, booking masuk, status pengerjaan, dan data customer secara lebih terstruktur.

Project ini juga ditujukan sebagai portfolio fullstack yang menunjukkan kemampuan dalam membangun sistem web modern berbasis REST API, role-based access, dashboard, database relational, dan UI yang profesional.

---

## 3. Tujuan Produk

Tujuan utama Revora adalah menyediakan platform yang memudahkan proses booking dan tracking service kendaraan secara digital.

Secara khusus, Revora bertujuan untuk:

1. Memudahkan customer melakukan booking service kendaraan.
2. Memudahkan customer mengelola data kendaraan pribadi.
3. Memungkinkan customer melihat status progress service.
4. Membantu admin mengelola booking service yang masuk.
5. Membantu admin mengelola daftar layanan service.
6. Menyediakan sistem dashboard yang rapi, responsif, dan mudah digunakan.
7. Menjadi portfolio fullstack dengan struktur frontend dan backend terpisah.

---

## 4. Konsep Utama Produk

Revora bukan hanya website profil bengkel. Revora diarahkan sebagai automotive service management platform dengan fitur utama:

- Booking service kendaraan
- Vehicle dashboard
- Tracking progress service
- Admin booking management
- Service management
- Role-based dashboard

Konsep sederhana:

> Customer dapat mendaftarkan kendaraannya, memilih layanan service, melakukan booking jadwal, lalu memantau status pengerjaan melalui dashboard.

---

## 5. Target Pengguna

### 5.1 Customer

Customer adalah pengguna yang ingin melakukan booking service kendaraan secara online.

Kebutuhan customer:

- Membuat akun
- Login ke dashboard
- Menambahkan data kendaraan
- Melihat layanan service
- Membuat booking service
- Melihat status booking
- Melihat riwayat service

### 5.2 Admin

Admin adalah pengguna internal bengkel yang mengelola sistem.

Kebutuhan admin:

- Login ke dashboard admin
- Melihat daftar booking masuk
- Mengubah status booking
- Mengelola data layanan service
- Melihat data customer
- Melihat ringkasan statistik dashboard

### 5.3 Mechanic

Mechanic adalah pengguna internal yang bertugas menangani kendaraan customer.

Untuk MVP awal, role mechanic belum wajib diimplementasikan penuh. Role ini dapat masuk pada fase lanjutan.

Kebutuhan mechanic pada fase lanjutan:

- Melihat daftar tugas service
- Update progress pengerjaan
- Menambahkan catatan perbaikan
- Melaporkan estimasi atau hasil pengecekan

---

## 6. Scope MVP

MVP adalah versi awal yang harus selesai terlebih dahulu sebelum menambahkan fitur lanjutan.

### 6.1 Fitur yang Masuk MVP

1. Landing page
2. Register dan login customer
3. Login admin
4. Customer dashboard
5. Vehicle management
6. Service list
7. Booking service
8. Booking history
9. Tracking status booking
10. Admin dashboard
11. Admin booking management
12. Admin service management
13. Role-based access
14. Responsive layout
15. Loading, empty, dan error state dasar

### 6.2 Fitur yang Tidak Masuk MVP

Fitur berikut belum masuk MVP dan akan dikerjakan pada fase berikutnya:

1. AI diagnostic
2. Payment gateway
3. Marketplace sparepart
4. WhatsApp notification
5. Email notification
6. Invoice PDF
7. Multi-branch workshop
8. Full mechanic dashboard
9. Advanced analytics
10. Real-time tracking

---

## 7. Problem Statement

Customer sering mengalami kesulitan dalam melakukan service kendaraan karena harus datang langsung atau menghubungi bengkel terlebih dahulu untuk mengetahui jadwal, layanan, dan status pengerjaan.

Di sisi bengkel, pengelolaan booking, data kendaraan, dan status service yang masih manual dapat menyebabkan miskomunikasi, kehilangan data, dan proses pelayanan yang kurang efisien.

Revora hadir untuk menyelesaikan masalah tersebut dengan sistem booking dan tracking service kendaraan yang terpusat.

---

## 8. Solusi yang Ditawarkan

Revora menyediakan sistem berbasis web yang memungkinkan customer melakukan booking service secara online dan melihat status pengerjaan kendaraan. Admin dapat mengelola booking, layanan, dan status service melalui dashboard.

Dengan sistem ini, customer mendapatkan kejelasan informasi, sedangkan admin mendapatkan alat bantu untuk mengelola operasional service secara lebih rapi.

---

## 9. User Flow Utama

### 9.1 Customer Flow

1. Customer membuka landing page.
2. Customer melakukan register atau login.
3. Customer masuk ke dashboard.
4. Customer menambahkan data kendaraan.
5. Customer memilih layanan service.
6. Customer memilih kendaraan, tanggal, dan jam booking.
7. Customer mengirim booking.
8. Booking masuk dengan status pending.
9. Admin mengonfirmasi booking.
10. Customer melihat status booking di dashboard.
11. Admin memperbarui status menjadi in progress atau completed.
12. Customer melihat riwayat service setelah selesai.

### 9.2 Admin Flow

1. Admin login ke dashboard admin.
2. Admin melihat ringkasan data booking.
3. Admin membuka daftar booking masuk.
4. Admin melihat detail booking.
5. Admin mengubah status booking.
6. Admin mengelola layanan service.
7. Admin melihat data customer dan kendaraan.

---

## 10. Role dan Permission

### 10.1 Customer

Customer dapat:

- Register
- Login
- Logout
- Melihat dashboard customer
- Mengelola kendaraan miliknya sendiri
- Membuat booking service
- Melihat booking miliknya sendiri
- Melihat status service miliknya sendiri

Customer tidak dapat:

- Mengakses dashboard admin
- Melihat booking customer lain
- Mengubah status booking
- Mengelola data layanan service

### 10.2 Admin

Admin dapat:

- Login
- Logout
- Mengakses dashboard admin
- Melihat semua booking
- Melihat semua customer
- Melihat semua kendaraan customer
- Mengubah status booking
- Mengelola layanan service
- Melihat statistik dashboard

Admin tidak difokuskan untuk membuat booking pribadi pada MVP.

### 10.3 Mechanic

Mechanic belum wajib untuk MVP. Role ini akan disiapkan sebagai pengembangan fase berikutnya.

---

## 11. Fitur Detail MVP

## 11.1 Landing Page

Landing page adalah halaman pertama yang dilihat user.

### Tujuan

Menjelaskan value utama Revora dan mengarahkan user untuk booking service.

### Section

- Navbar
- Hero section
- Service highlight
- How it works
- Why choose us
- Promo atau featured service
- Testimonial
- CTA booking
- Footer

### CTA Utama

- Book Service
- Get Started
- Login

### Style Visual

- Dark automotive theme
- Premium look
- Modern card UI
- Glassmorphism ringan
- Accent color biru, cyan, atau neon amber
- Responsive untuk desktop dan mobile

---

## 11.2 Authentication

### Fitur

- Register customer
- Login customer
- Login admin
- Logout
- Get current authenticated user
- Protect route berdasarkan role

### Data Register Customer

- Name
- Email
- Password
- Password confirmation
- Phone number

### Data Login

- Email
- Password

### Catatan Teknis

Backend menggunakan Laravel Sanctum. Frontend menyimpan status user secara aman melalui request API dan route guard.

---

## 11.3 Customer Dashboard

Customer dashboard menampilkan ringkasan data milik customer.

### Informasi yang Ditampilkan

- Nama customer
- Jumlah kendaraan
- Booking aktif
- Booking terakhir
- Riwayat service singkat
- Shortcut untuk booking baru

### Komponen UI

- Stats card
- Vehicle card
- Recent booking card
- Status badge
- CTA card

---

## 11.4 Vehicle Management

Customer dapat mengelola kendaraan pribadi.

### Fitur

- Tambah kendaraan
- Lihat daftar kendaraan
- Edit kendaraan
- Hapus kendaraan

### Data Kendaraan

- Brand
- Model
- Year
- Plate number
- Transmission type
- Fuel type
- Last odometer

### Validasi

- Plate number wajib unik per user
- Brand wajib diisi
- Model wajib diisi
- Year harus valid

---

## 11.5 Service List

Customer dapat melihat daftar layanan service yang tersedia.

### Data Layanan

- Service name
- Description
- Estimated duration
- Base price
- Category
- Is active

### Contoh Layanan

- Oil Change
- Brake Inspection
- Tire Rotation
- Engine Tune Up
- AC Service
- Battery Check
- General Inspection

---

## 11.6 Booking Service

Customer dapat membuat booking service.

### Form Booking

- Pilih kendaraan
- Pilih layanan
- Pilih tanggal
- Pilih jam
- Keluhan atau catatan customer

### Status Awal

Setiap booking baru akan memiliki status:

```txt
pending
```

### Validasi

- Customer harus login
- Customer harus memiliki minimal satu kendaraan
- Service harus aktif
- Tanggal booking tidak boleh tanggal masa lalu
- Jam booking wajib dipilih

---

## 11.7 Booking History

Customer dapat melihat daftar booking yang pernah dibuat.

### Informasi yang Ditampilkan

- Nomor booking
- Kendaraan
- Layanan
- Tanggal booking
- Status
- Estimasi harga

### Filter Dasar

- All
- Pending
- Confirmed
- In Progress
- Completed
- Cancelled

---

## 11.8 Tracking Status Booking

Customer dapat melihat progress booking.

### Status Booking

```txt
pending
confirmed
in_progress
completed
cancelled
```

### Tampilan Tracking

- Timeline status
- Tanggal update status
- Catatan admin jika ada

### Contoh Timeline

1. Booking Created
2. Booking Confirmed
3. Vehicle In Progress
4. Service Completed

---

## 11.9 Admin Dashboard

Admin dashboard menampilkan ringkasan data operasional.

### Informasi yang Ditampilkan

- Total booking
- Booking pending
- Booking in progress
- Booking completed
- Total customer
- Total service aktif
- Revenue estimation sederhana

### Komponen UI

- Stats card
- Booking table preview
- Recent activity
- Chart sederhana pada fase lanjutan

---

## 11.10 Admin Booking Management

Admin dapat mengelola semua booking.

### Fitur

- Lihat semua booking
- Lihat detail booking
- Update status booking
- Tambahkan catatan admin
- Filter berdasarkan status

### Status yang Dapat Diubah Admin

- pending → confirmed
- confirmed → in_progress
- in_progress → completed
- pending / confirmed → cancelled

### Catatan

Setiap perubahan status akan dicatat ke tabel booking_status_logs.

---

## 11.11 Admin Service Management

Admin dapat mengelola daftar layanan service.

### Fitur

- Tambah layanan
- Lihat daftar layanan
- Edit layanan
- Nonaktifkan layanan
- Hapus layanan jika belum pernah dipakai booking

### Data Layanan

- Name
- Category
- Description
- Estimated duration
- Base price
- Is active

---

## 12. Halaman Frontend

## 12.1 Public Pages

```txt
/
/login
/register
```

## 12.2 Customer Pages

```txt
/dashboard
/dashboard/vehicles
/dashboard/vehicles/create
/dashboard/vehicles/:id/edit
/dashboard/services
/dashboard/bookings
/dashboard/bookings/create
/dashboard/bookings/:id
/profile
```

## 12.3 Admin Pages

```txt
/admin
/admin/bookings
/admin/bookings/:id
/admin/services
/admin/services/create
/admin/services/:id/edit
/admin/customers
```

---

## 13. Backend API Endpoint Draft

## 13.1 Auth

```txt
POST   /api/register
POST   /api/login
POST   /api/logout
GET    /api/user
```

## 13.2 Customer Vehicles

```txt
GET    /api/vehicles
POST   /api/vehicles
GET    /api/vehicles/{id}
PUT    /api/vehicles/{id}
DELETE /api/vehicles/{id}
```

## 13.3 Services

```txt
GET    /api/services
GET    /api/services/{id}
```

## 13.4 Bookings

```txt
GET    /api/bookings
POST   /api/bookings
GET    /api/bookings/{id}
DELETE /api/bookings/{id}
```

## 13.5 Admin Bookings

```txt
GET    /api/admin/bookings
GET    /api/admin/bookings/{id}
PATCH  /api/admin/bookings/{id}/status
```

## 13.6 Admin Services

```txt
GET    /api/admin/services
POST   /api/admin/services
GET    /api/admin/services/{id}
PUT    /api/admin/services/{id}
DELETE /api/admin/services/{id}
```

## 13.7 Admin Customers

```txt
GET    /api/admin/customers
GET    /api/admin/customers/{id}
```

---

## 14. Database Draft

## 14.1 users

| Field      | Type      | Keterangan                |
| ---------- | --------- | ------------------------- |
| id         | bigint    | Primary key               |
| name       | varchar   | Nama user                 |
| email      | varchar   | Email user, unique        |
| password   | varchar   | Password hash             |
| phone      | varchar   | Nomor telepon             |
| role       | enum      | customer, admin, mechanic |
| created_at | timestamp | Tanggal dibuat            |
| updated_at | timestamp | Tanggal update            |

## 14.2 vehicles

| Field             | Type      | Keterangan                            |
| ----------------- | --------- | ------------------------------------- |
| id                | bigint    | Primary key                           |
| user_id           | bigint    | Relasi ke users                       |
| brand             | varchar   | Merek kendaraan                       |
| model             | varchar   | Model kendaraan                       |
| year              | integer   | Tahun kendaraan                       |
| plate_number      | varchar   | Nomor plat                            |
| transmission_type | varchar   | Manual / Automatic                    |
| fuel_type         | varchar   | Gasoline / Diesel / Electric / Hybrid |
| last_odometer     | integer   | Kilometer terakhir                    |
| created_at        | timestamp | Tanggal dibuat                        |
| updated_at        | timestamp | Tanggal update                        |

## 14.3 services

| Field              | Type      | Keterangan                  |
| ------------------ | --------- | --------------------------- |
| id                 | bigint    | Primary key                 |
| name               | varchar   | Nama layanan                |
| category           | varchar   | Kategori layanan            |
| description        | text      | Deskripsi layanan           |
| estimated_duration | integer   | Durasi estimasi dalam menit |
| base_price         | decimal   | Harga dasar                 |
| is_active          | boolean   | Status aktif layanan        |
| created_at         | timestamp | Tanggal dibuat              |
| updated_at         | timestamp | Tanggal update              |

## 14.4 bookings

| Field           | Type      | Keterangan                                            |
| --------------- | --------- | ----------------------------------------------------- |
| id              | bigint    | Primary key                                           |
| booking_code    | varchar   | Kode booking unik                                     |
| user_id         | bigint    | Relasi ke users                                       |
| vehicle_id      | bigint    | Relasi ke vehicles                                    |
| service_id      | bigint    | Relasi ke services                                    |
| booking_date    | date      | Tanggal booking                                       |
| booking_time    | time      | Jam booking                                           |
| status          | enum      | pending, confirmed, in_progress, completed, cancelled |
| complaint_note  | text      | Keluhan customer                                      |
| admin_note      | text      | Catatan admin                                         |
| estimated_price | decimal   | Estimasi harga                                        |
| created_at      | timestamp | Tanggal dibuat                                        |
| updated_at      | timestamp | Tanggal update                                        |

## 14.5 booking_status_logs

| Field      | Type      | Keterangan                |
| ---------- | --------- | ------------------------- |
| id         | bigint    | Primary key               |
| booking_id | bigint    | Relasi ke bookings        |
| status     | varchar   | Status booking            |
| note       | text      | Catatan perubahan status  |
| changed_by | bigint    | User yang mengubah status |
| created_at | timestamp | Tanggal dibuat            |
| updated_at | timestamp | Tanggal update            |

---

## 15. Struktur Repository

Project akan dibuat dalam tiga repository terpisah agar frontend, backend, dan dokumentasi API dapat dikembangkan secara rapi tanpa terjadi mismatch antara implementasi FE dan BE.

## 15.1 Frontend Repository

Nama repo yang disarankan:

```txt
revora-client
```

Stack:

- React
- Vite
- TypeScript
- Tailwind CSS
- React Router
- Axios
- TanStack Query
- Zustand atau Context API
- Framer Motion

Contoh struktur folder:

```txt
revora-client/
├── src/
│   ├── app/
│   ├── assets/
│   ├── components/
│   ├── features/
│   │   ├── auth/
│   │   ├── vehicles/
│   │   ├── services/
│   │   ├── bookings/
│   │   └── admin/
│   ├── hooks/
│   ├── layouts/
│   ├── lib/
│   ├── pages/
│   ├── routes/
│   ├── types/
│   └── main.tsx
├── .env.example
├── package.json
└── README.md
```

## 15.2 Backend Repository

Nama repo yang disarankan:

```txt
revora-api
```

Stack:

- Laravel
- Laravel Sanctum
- Eloquent ORM
- MySQL / PostgreSQL
- Form Request Validation
- API Resource
- Policy / Middleware

Contoh struktur penting:

```txt
revora-api/
├── app/
│   ├── Http/
│   │   ├── Controllers/
│   │   │   ├── Api/
│   │   │   └── Admin/
│   │   ├── Requests/
│   │   ├── Resources/
│   │   └── Middleware/
│   ├── Models/
│   ├── Policies/
│   └── Services/
├── database/
│   ├── migrations/
│   └── seeders/
├── routes/
│   └── api.php
├── .env.example
└── README.md
```

---

## 15.3 Documentation Repository

Nama repo:

```txt
revora-docs
```

Fungsi utama repository ini adalah menjadi pusat dokumentasi project Revora, terutama untuk menjaga kesesuaian antara frontend dan backend.

Isi dokumentasi yang disarankan:

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

Dokumentasi penting yang wajib ada:

1. PRD final
2. ERD dan database schema
3. API contract
4. Auth flow
5. Role permission
6. Frontend routes
7. Backend endpoints
8. Response format standar
9. Error response standar
10. Technical decision log

Tujuan `revora-docs`:

- Menjadi sumber kebenaran bersama antara FE dan BE.
- Menghindari perbedaan nama field antara frontend dan backend.
- Menentukan endpoint sebelum coding frontend.
- Menentukan response API sebelum implementasi backend.
- Menyimpan perubahan keputusan teknis selama development.
- Membantu project terlihat lebih profesional untuk portfolio.

## 16. UI/UX Direction

### 16.1 Visual Identity

Revora menggunakan visual premium dengan nuansa otomotif modern.

Karakter desain:

- Clean
- Dark premium
- Modern
- Fast
- Trustworthy
- Tech-oriented

### 16.2 Warna Awal

Rekomendasi warna:

```txt
Background dark : #0B0F17
Surface dark    : #111827
Primary blue    : #2563EB
Cyan accent     : #06B6D4
Amber accent    : #F59E0B
Text primary    : #F9FAFB
Text secondary  : #9CA3AF
```

### 16.3 Komponen Utama

- Button
- Input
- Select
- Textarea
- Card
- Modal
- Badge
- Table
- Sidebar
- Navbar
- Stats card
- Timeline
- Empty state
- Loading skeleton
- Alert

---

## 17. Non-Functional Requirement

### 17.1 Performance

- Halaman utama harus ringan dan cepat dimuat.
- Data dashboard menggunakan loading state.
- API response konsisten dan tidak mengirim data berlebihan.

### 17.2 Security

- Password harus di-hash.
- Endpoint admin harus dilindungi role middleware.
- Customer hanya boleh mengakses data miliknya sendiri.
- Validasi dilakukan di backend.
- Frontend tidak boleh menjadi satu-satunya pengaman role.

### 17.3 Responsiveness

- Landing page responsif di mobile, tablet, dan desktop.
- Dashboard minimal nyaman digunakan di laptop dan tablet.
- Table admin perlu mendukung responsive layout.

### 17.4 Maintainability

- Struktur folder harus modular.
- Komponen frontend harus reusable.
- Backend menggunakan controller, request validation, resource, dan service layer jika diperlukan.
- README harus menjelaskan cara menjalankan project.

---

## 18. Success Criteria MVP

MVP dianggap selesai jika:

1. Customer bisa register dan login.
2. Customer bisa menambahkan kendaraan.
3. Customer bisa melihat layanan service.
4. Customer bisa membuat booking.
5. Customer bisa melihat riwayat dan status booking.
6. Admin bisa login.
7. Admin bisa melihat semua booking.
8. Admin bisa update status booking.
9. Admin bisa mengelola layanan service.
10. Route customer dan admin sudah diproteksi sesuai role.
11. Frontend responsif dan memiliki UI yang konsisten.
12. Backend API memiliki response dan validation error yang rapi.
13. Project FE dan BE memiliki README masing-masing.

---

## 19. Development Phase

## Phase 0 — Planning

- Finalisasi PRD
- Finalisasi tech stack
- Finalisasi database schema
- Finalisasi API endpoint
- Menentukan UI direction

## Phase 1 — Backend Foundation

- Setup Laravel project
- Setup database
- Setup Sanctum
- Setup auth API
- Setup role middleware
- Setup migration awal
- Setup seeder admin dan services

## Phase 2 — Frontend Foundation

- Setup React Vite TypeScript
- Setup Tailwind CSS
- Setup routing
- Setup layout public, customer, admin
- Setup API client
- Setup auth store
- Setup protected route

## Phase 3 — Customer Features

- Customer dashboard
- Vehicle CRUD
- Service list
- Booking form
- Booking history
- Booking detail tracking

## Phase 4 — Admin Features

- Admin dashboard
- Booking management
- Booking status update
- Service management
- Customer list

## Phase 5 — Polish

- Responsive improvements
- Loading state
- Empty state
- Error handling
- Toast notification
- UI consistency
- README documentation

## Phase 6 — Advanced Features

- Mechanic role
- AI diagnostic
- Reminder service
- Invoice PDF
- Notification
- Payment gateway

---

## 20. Risiko dan Batasan

### Risiko

1. Scope terlalu besar jika semua fitur dikerjakan sekaligus.
2. Integrasi auth Laravel Sanctum dan React bisa membingungkan jika konfigurasi CORS/CSRF tidak rapi.
3. Role system bisa menjadi kompleks jika mechanic langsung dimasukkan di awal.
4. Dashboard admin bisa melebar jika analytics terlalu banyak.

### Batasan MVP

1. MVP hanya fokus pada booking dan tracking service.
2. Payment belum tersedia.
3. AI diagnostic belum tersedia.
4. Mechanic dashboard belum wajib.
5. Notifikasi WhatsApp/email belum tersedia.

---

## 21. Catatan Pengembangan

Prioritas utama adalah membuat sistem yang selesai, rapi, dan bisa dipresentasikan sebagai portfolio. Fitur boleh sederhana, tetapi alur harus jelas dan konsisten.

Urutan pengerjaan yang disarankan:

1. Backend auth dan database
2. Backend API vehicles, services, bookings
3. Frontend auth dan route protection
4. Customer dashboard
5. Booking flow
6. Admin dashboard
7. Status tracking
8. Polish UI dan dokumentasi

---

## 22. Ringkasan MVP

Revora MVP adalah web app fullstack dengan Laravel sebagai backend REST API dan React sebagai frontend SPA. Fitur utamanya adalah customer dapat mengelola kendaraan, melakukan booking service, dan memantau status service, sementara admin dapat mengelola booking dan layanan service.

Dengan scope ini, Revora sudah cukup kuat sebagai portfolio karena mencakup auth, role-based access, CRUD relasional, dashboard, tracking status, API design, dan UI modern.

---

## 23. Production Learning Goals

Selain menjadi portfolio, Revora juga digunakan sebagai media belajar bagaimana web app dibuat dengan pendekatan production atau industry-level.

Tujuan pembelajaran production:

1. Memahami cara memisahkan frontend, backend, dan dokumentasi.
2. Memahami API contract agar frontend dan backend tidak mismatch.
3. Memahami environment development, staging, dan production.
4. Memahami authentication flow yang aman.
5. Memahami role-based access control.
6. Memahami database migration, seeder, dan relational design.
7. Memahami error handling yang konsisten.
8. Memahami validasi data di backend dan frontend.
9. Memahami struktur folder yang maintainable.
10. Memahami deployment workflow.
11. Memahami dokumentasi teknis yang rapi.
12. Memahami testing dasar sebelum fitur dianggap selesai.

---

## 24. Industry-Level Development Standard

Revora akan dikembangkan dengan standar yang mendekati cara kerja project profesional.

### 24.1 Repository Separation

Revora menggunakan tiga repository:

```txt
revora-client   -> React frontend
revora-api      -> Laravel backend
revora-docs     -> Documentation and API contract
```

Tujuan pemisahan repository:

- Frontend dan backend dapat dikembangkan secara mandiri.
- Dokumentasi menjadi sumber kebenaran bersama.
- API contract dapat ditentukan sebelum implementasi.
- Struktur project terlihat lebih profesional.

### 24.2 Documentation First

Sebelum fitur dibuat, dokumentasi minimal harus menjelaskan:

- Tujuan fitur
- Role yang boleh mengakses
- Endpoint API
- Request body
- Response success
- Response error
- Status code
- Validasi data
- Catatan frontend
- Catatan backend

Prinsip:

> Jangan coding fitur besar sebelum flow, data, dan API contract jelas.

### 24.3 Environment Management

Project harus membedakan environment:

```txt
local       -> berjalan di laptop developer
staging     -> tempat testing sebelum production
production  -> aplikasi live untuk user asli
```

File `.env` tidak boleh di-commit ke repository. Yang boleh di-commit adalah `.env.example`.

Contoh environment frontend:

```txt
VITE_API_BASE_URL=http://localhost:8000/api
```

Contoh environment backend:

```txt
APP_ENV=local
APP_URL=http://localhost:8000
DB_DATABASE=revora
FRONTEND_URL=http://localhost:5173
```

### 24.4 Branching Workflow

Branch dasar yang disarankan:

```txt
main       -> kode stabil
develop    -> integrasi fitur sebelum masuk main
feature/*  -> pengembangan fitur tertentu
fix/*      -> perbaikan bug
```

Contoh branch:

```txt
feature/auth-api
feature/customer-vehicles
feature/booking-flow
fix/login-validation
```

### 24.5 Commit Convention

Gunakan commit message yang jelas.

Contoh:

```txt
feat: add customer vehicle CRUD API
fix: handle invalid login response
chore: update env example
refactor: improve booking service layer
```

Tujuannya agar history project mudah dibaca.

### 24.6 API Response Standard

Backend harus mengirim response yang konsisten.

Success response:

```json
{
  "success": true,
  "message": "Vehicle created successfully",
  "data": {
    "id": 1,
    "brand": "Toyota",
    "model": "Avanza",
    "plate_number": "AD 1234 XX"
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

### 24.7 Frontend Data Handling

Frontend tidak langsung menaruh logic API di komponen halaman.

Struktur yang disarankan:

```txt
pages       -> tampilan halaman
features    -> logic per fitur
services    -> komunikasi API
components  -> reusable UI
hooks       -> reusable stateful logic
types       -> TypeScript type/interface
```

Prinsip:

> Component fokus ke UI, service fokus ke API, hook fokus ke logic.

### 24.8 Backend Structure Standard

Backend Laravel harus menjaga pemisahan tanggung jawab.

Struktur yang disarankan:

```txt
Controller       -> menerima request dan mengembalikan response
Form Request     -> validasi input
Model            -> representasi tabel database
Policy/Middleware-> authorization dan role access
Resource         -> format response API
Service Class    -> business logic jika mulai kompleks
Seeder           -> data awal untuk testing
Migration        -> struktur database
```

Prinsip:

> Controller jangan terlalu gemuk. Logic kompleks dipindahkan ke service class.

### 24.9 Security Minimum Standard

Hal penting yang harus diterapkan:

1. Password harus di-hash.
2. Endpoint admin wajib dilindungi middleware role.
3. Customer hanya boleh mengakses data miliknya sendiri.
4. Validasi tetap wajib di backend walaupun frontend sudah validasi.
5. `.env` tidak boleh masuk GitHub.
6. Error production tidak boleh menampilkan detail sensitif.
7. API harus membatasi akses berdasarkan user login.
8. Delete data penting sebaiknya dipertimbangkan soft delete.

### 24.10 Testing Minimum Standard

Minimal testing yang disarankan:

Backend:

- Auth register
- Auth login
- Vehicle CRUD
- Booking creation
- Admin update booking status
- Role access protection

Frontend:

- Form validation manual
- Route protection manual
- Loading state
- Empty state
- Error state
- Responsive check

### 24.11 Definition of Done

Sebuah fitur dianggap selesai jika:

1. Requirement fitur sudah jelas.
2. API contract sudah ditulis di revora-docs.
3. Backend endpoint sudah dibuat.
4. Backend validation sudah dibuat.
5. Backend authorization sudah aman.
6. Frontend UI sudah dibuat.
7. Frontend terhubung dengan API.
8. Loading, empty, dan error state tersedia.
9. Fitur sudah dites secara manual.
10. Dokumentasi diperbarui.

### 24.12 Production Mindset

Dalam project production, targetnya bukan hanya “fitur jalan”. Targetnya adalah:

- Aman
- Stabil
- Mudah dikembangkan
- Mudah dipahami developer lain
- Mudah didebug
- Mudah dideploy
- Konsisten antara frontend, backend, dan dokumentasi

Prinsip utama Revora:

> Build small, document clearly, integrate carefully, and polish consistently.
