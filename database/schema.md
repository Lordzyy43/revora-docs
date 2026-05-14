# Revora Database Schema

Dokumen ini menjelaskan rancangan database untuk Revora MVP. Schema ini digunakan sebagai acuan untuk migration Laravel, Eloquent relationship, API Resource, dan TypeScript type di frontend.

---

## 1. Database Design Principle

Revora menggunakan pendekatan **normalisasi secukupnya**.

Artinya:

- Data utama dipisah ke tabel yang sesuai.
- Relasi antar data dibuat jelas menggunakan foreign key.
- Data tidak disimpan berulang tanpa alasan.
- Struktur tetap sederhana agar MVP cepat selesai.
- Beberapa snapshot data boleh disimpan jika berguna untuk histori transaksi.

Target normalisasi untuk MVP:

```txt
1NF -> data atomic, tidak ada list campur dalam satu kolom
2NF -> data bergantung pada primary key tabelnya
3NF -> data non-key tidak saling bergantung secara berlebihan
```

Namun, Revora tidak perlu terlalu ekstrem sampai membuat terlalu banyak tabel kecil jika belum dibutuhkan.

Prinsip utama:

> Normalize the core data, but keep the MVP practical.

---

## 2. Why Normalization Matters

Normalisasi diperlukan agar:

1. Data tidak redundant.
2. Relasi antar data lebih jelas.
3. Update data tidak menyebabkan inkonsistensi.
4. Backend lebih mudah menjaga authorization.
5. API lebih mudah dikembangkan.
6. Query lebih aman dan predictable.

Contoh buruk jika tidak dinormalisasi:

```txt
bookings table menyimpan:
- customer_name
- customer_email
- vehicle_brand
- vehicle_model
- service_name
- service_price
```

Masalahnya:

- Kalau nama customer berubah, data lama bisa tidak sinkron.
- Kalau harga service berubah, booking lama bisa kacau.
- Kalau kendaraan diedit, riwayat booking jadi membingungkan.

Solusi normalisasi:

```txt
bookings menyimpan user_id, vehicle_id, service_id
```

Lalu data detail diambil dari tabel terkait.

Namun, untuk data transaksi tertentu, snapshot boleh digunakan.

Contoh snapshot yang masuk akal:

```txt
estimated_price
service_name_snapshot
vehicle_plate_snapshot
```

Snapshot digunakan supaya histori booking tetap akurat walaupun data service atau kendaraan berubah setelah booking dibuat.

---

## 3. MVP Tables

Tabel utama untuk Revora MVP:

```txt
users
vehicles
services
bookings
booking_status_logs
```

Tabel optional untuk fase lanjutan:

```txt
branches
mechanic_profiles
service_notes
payments
notifications
ai_diagnostics
```

Untuk MVP, role admin, customer, dan mechanic masih dapat disimpan langsung di tabel `users` melalui kolom `role`.

---

## 4. Entity Relationship Summary

Relasi utama:

```txt
users 1..n vehicles
users 1..n bookings
vehicles 1..n bookings
services 1..n bookings
bookings 1..n booking_status_logs
users 1..n booking_status_logs as changed_by
```

Penjelasan:

- Satu customer dapat memiliki banyak kendaraan.
- Satu customer dapat membuat banyak booking.
- Satu kendaraan dapat memiliki banyak riwayat booking.
- Satu service dapat dipakai di banyak booking.
- Satu booking dapat memiliki banyak log perubahan status.
- Setiap perubahan status dicatat oleh user tertentu, biasanya admin.

---

## 5. Table: users

Tabel `users` menyimpan data akun pengguna.

### Purpose

Menyimpan data akun customer, admin, dan mechanic.

### Columns

| Column            | Type            | Constraint                 | Description               |
| ----------------- | --------------- | -------------------------- | ------------------------- |
| id                | bigint unsigned | primary key                | Unique user ID            |
| name              | varchar(100)    | required                   | Full name                 |
| email             | varchar(150)    | required, unique           | Email for login           |
| password          | varchar(255)    | required                   | Hashed password           |
| phone             | varchar(30)     | nullable                   | User phone number         |
| role              | enum            | required, default customer | customer, admin, mechanic |
| email_verified_at | timestamp       | nullable                   | Email verification time   |
| remember_token    | varchar(100)    | nullable                   | Laravel remember token    |
| created_at        | timestamp       | auto                       | Created time              |
| updated_at        | timestamp       | auto                       | Updated time              |
| deleted_at        | timestamp       | nullable                   | Soft delete time          |

### Role Values

```txt
customer
admin
mechanic
```

### Index

```txt
unique(email)
index(role)
```

### Notes

- Password wajib di-hash menggunakan Laravel Hash.
- Admin user sebaiknya dibuat melalui seeder.
- Untuk MVP, role disimpan langsung di tabel `users` agar sederhana.
- Jika role makin kompleks, bisa dipisah ke tabel `roles` dan `user_roles` pada fase lanjutan.

---

## 6. Table: vehicles

Tabel `vehicles` menyimpan data kendaraan milik customer.

### Purpose

Menyimpan kendaraan yang akan digunakan dalam proses booking service.

### Columns

| Column            | Type              | Constraint  | Description                        |
| ----------------- | ----------------- | ----------- | ---------------------------------- |
| id                | bigint unsigned   | primary key | Unique vehicle ID                  |
| user_id           | bigint unsigned   | foreign key | Owner user ID                      |
| brand             | varchar(100)      | required    | Vehicle brand                      |
| model             | varchar(100)      | required    | Vehicle model                      |
| year              | unsigned smallint | required    | Vehicle production year            |
| plate_number      | varchar(30)       | required    | Vehicle plate number               |
| transmission_type | enum              | nullable    | manual, automatic                  |
| fuel_type         | enum              | nullable    | gasoline, diesel, electric, hybrid |
| last_odometer     | unsigned integer  | nullable    | Last known odometer                |
| color             | varchar(50)       | nullable    | Vehicle color                      |
| created_at        | timestamp         | auto        | Created time                       |
| updated_at        | timestamp         | auto        | Updated time                       |
| deleted_at        | timestamp         | nullable    | Soft delete time                   |

### Transmission Values

```txt
manual
automatic
```

### Fuel Values

```txt
gasoline
diesel
electric
hybrid
```

### Relationship

```txt
Vehicle belongs to User
Vehicle has many Bookings
```

### Index

```txt
index(user_id)
unique(user_id, plate_number)
```

### Notes

- `plate_number` dibuat unik per user agar satu user tidak membuat kendaraan duplikat.
- Pada kasus production nyata, plate number bisa dipertimbangkan unique global.
- Gunakan soft delete agar riwayat booking lama tidak rusak ketika kendaraan dihapus dari dashboard customer.

---

## 7. Table: services

Tabel `services` menyimpan layanan service kendaraan.

### Purpose

Menyimpan daftar layanan yang dapat dipilih customer saat booking.

### Columns

| Column             | Type             | Constraint             | Description                     |
| ------------------ | ---------------- | ---------------------- | ------------------------------- |
| id                 | bigint unsigned  | primary key            | Unique service ID               |
| name               | varchar(120)     | required               | Service name                    |
| slug               | varchar(150)     | required, unique       | URL-friendly service identifier |
| category           | varchar(100)     | nullable               | Service category                |
| description        | text             | nullable               | Service description             |
| estimated_duration | unsigned integer | nullable               | Estimated duration in minutes   |
| base_price         | decimal(12,2)    | required, default 0    | Base service price              |
| is_active          | boolean          | required, default true | Whether service can be booked   |
| created_at         | timestamp        | auto                   | Created time                    |
| updated_at         | timestamp        | auto                   | Updated time                    |
| deleted_at         | timestamp        | nullable               | Soft delete time                |

### Relationship

```txt
Service has many Bookings
```

### Index

```txt
unique(slug)
index(is_active)
index(category)
```

### Notes

- `is_active` digunakan untuk menonaktifkan service tanpa menghapus data.
- Service yang sudah pernah dipakai booking sebaiknya tidak hard delete.
- `base_price` digunakan sebagai estimasi awal, bukan final invoice.

---

## 8. Table: bookings

Tabel `bookings` menyimpan data booking service customer.

### Purpose

Menyimpan transaksi booking service kendaraan.

### Columns

| Column                 | Type            | Constraint                | Description                           |
| ---------------------- | --------------- | ------------------------- | ------------------------------------- |
| id                     | bigint unsigned | primary key               | Unique booking ID                     |
| booking_code           | varchar(30)     | required, unique          | Human-readable booking code           |
| user_id                | bigint unsigned | foreign key               | Customer who created booking          |
| vehicle_id             | bigint unsigned | foreign key               | Vehicle used for booking              |
| service_id             | bigint unsigned | foreign key               | Selected service                      |
| booking_date           | date            | required                  | Booking date                          |
| booking_time           | time            | required                  | Booking time                          |
| status                 | enum            | required, default pending | Current booking status                |
| complaint_note         | text            | nullable                  | Customer complaint or note            |
| admin_note             | text            | nullable                  | Admin internal note                   |
| estimated_price        | decimal(12,2)   | nullable                  | Estimated price at booking time       |
| final_price            | decimal(12,2)   | nullable                  | Final price after service completed   |
| service_name_snapshot  | varchar(120)    | nullable                  | Service name when booking was created |
| vehicle_plate_snapshot | varchar(30)     | nullable                  | Plate number when booking was created |
| completed_at           | timestamp       | nullable                  | Completion time                       |
| cancelled_at           | timestamp       | nullable                  | Cancellation time                     |
| created_at             | timestamp       | auto                      | Created time                          |
| updated_at             | timestamp       | auto                      | Updated time                          |
| deleted_at             | timestamp       | nullable                  | Soft delete time                      |

### Status Values

```txt
pending
confirmed
in_progress
completed
cancelled
```

### Relationship

```txt
Booking belongs to User
Booking belongs to Vehicle
Booking belongs to Service
Booking has many BookingStatusLogs
```

### Index

```txt
unique(booking_code)
index(user_id)
index(vehicle_id)
index(service_id)
index(status)
index(booking_date)
index(booking_date, booking_time)
```

### Notes

- `booking_code` digunakan agar booking mudah dibaca user, misalnya `REV-20260514-0001`.
- `estimated_price` menyimpan harga estimasi saat booking dibuat.
- `service_name_snapshot` dan `vehicle_plate_snapshot` bersifat denormalisasi terkontrol untuk menjaga histori.
- Status terkini disimpan di `bookings.status` agar query cepat.
- Riwayat perubahan status disimpan di `booking_status_logs`.

---

## 9. Table: booking_status_logs

Tabel `booking_status_logs` menyimpan riwayat perubahan status booking.

### Purpose

Mencatat timeline status booking agar customer dapat melihat progress service.

### Columns

| Column     | Type            | Constraint            | Description             |
| ---------- | --------------- | --------------------- | ----------------------- |
| id         | bigint unsigned | primary key           | Unique log ID           |
| booking_id | bigint unsigned | foreign key           | Related booking ID      |
| status     | enum            | required              | Status at this log      |
| note       | text            | nullable              | Status update note      |
| changed_by | bigint unsigned | nullable, foreign key | User who changed status |
| created_at | timestamp       | auto                  | Status change time      |
| updated_at | timestamp       | auto                  | Updated time            |

### Status Values

```txt
pending
confirmed
in_progress
completed
cancelled
```

### Relationship

```txt
BookingStatusLog belongs to Booking
BookingStatusLog belongs to User as changedBy
```

### Index

```txt
index(booking_id)
index(status)
index(changed_by)
index(created_at)
```

### Notes

- Log pertama dibuat otomatis saat booking dibuat dengan status `pending`.
- Setiap admin mengubah status, log baru harus dibuat.
- `changed_by` nullable agar sistem bisa membuat log otomatis jika diperlukan.

---

## 10. Optional Tables for Phase 2+

Tabel berikut belum wajib untuk MVP, tetapi disiapkan untuk pengembangan berikutnya.

---

## 10.1 Table: branches

Digunakan jika Revora mendukung banyak cabang bengkel.

```txt
id
name
address
city
phone
opening_time
closing_time
is_active
created_at
updated_at
deleted_at
```

Nanti `bookings` dapat memiliki `branch_id`.

---

## 10.2 Table: mechanic_profiles

Digunakan jika role mechanic ingin dibuat lebih detail.

```txt
id
user_id
specialization
experience_years
is_available
created_at
updated_at
```

Nanti `bookings` dapat memiliki `mechanic_id`.

---

## 10.3 Table: service_notes

Digunakan untuk catatan teknis dari mechanic.

```txt
id
booking_id
mechanic_id
note
diagnosis
recommended_action
created_at
updated_at
```

---

## 10.4 Table: payments

Digunakan untuk pembayaran.

```txt
id
booking_id
amount
method
status
paid_at
created_at
updated_at
```

---

## 10.5 Table: notifications

Digunakan untuk notifikasi app, email, atau WhatsApp.

```txt
id
user_id
title
message
type
is_read
read_at
created_at
updated_at
```

---

## 10.6 Table: ai_diagnostics

Digunakan untuk fitur AI diagnostic.

```txt
id
user_id
vehicle_id
symptom_text
possible_causes
recommendation
estimated_cost_min
estimated_cost_max
created_at
updated_at
```

---

## 11. Status Transition Rule

Status booking tidak boleh berubah sembarangan.

Allowed transitions:

```txt
pending -> confirmed
pending -> cancelled
confirmed -> in_progress
confirmed -> cancelled
in_progress -> completed
```

Not allowed:

```txt
completed -> pending
completed -> in_progress
cancelled -> confirmed
cancelled -> in_progress
```

Catatan:

- Status `completed` dan `cancelled` dianggap final state.
- Jika ada kebutuhan koreksi status, sebaiknya hanya admin tertentu yang boleh melakukan override pada fase lanjutan.

---

## 12. Data Ownership Rule

Aturan ownership sangat penting untuk keamanan API.

### Customer

Customer hanya boleh mengakses:

```txt
vehicles.user_id = authenticated_user.id
bookings.user_id = authenticated_user.id
```

Customer tidak boleh:

```txt
melihat kendaraan user lain
melihat booking user lain
mengubah status booking
mengakses endpoint admin
```

### Admin

Admin boleh mengakses:

```txt
semua vehicles
semua bookings
semua services
semua customers
```

Admin boleh mengubah:

```txt
booking status
service data
```

---

## 13. Soft Delete Strategy

Soft delete disarankan untuk tabel:

```txt
users
vehicles
services
bookings
```

Alasan:

- Data histori booking tetap aman.
- Data yang terhubung tidak langsung rusak.
- Lebih mendekati praktik production.

Tabel log seperti `booking_status_logs` tidak perlu soft delete pada MVP.

---

## 14. Seeder Data

Seeder dibutuhkan agar development lebih cepat.

### Admin Seeder

```txt
name: Admin Revora
email: admin@revora.test
password: password
role: admin
```

### Customer Seeder

```txt
name: Customer Demo
email: customer@revora.test
password: password
role: customer
```

### Service Seeder

Contoh layanan:

```txt
Oil Change
Brake Inspection
Tire Rotation
Engine Tune Up
AC Service
Battery Check
General Inspection
```

### Vehicle Seeder

Contoh kendaraan:

```txt
Toyota Avanza 2020
Honda Brio 2021
Daihatsu Xenia 2019
```

---

## 15. Laravel Migration Order

Urutan migration yang disarankan:

```txt
1. users
2. vehicles
3. services
4. bookings
5. booking_status_logs
```

Alasan:

- `vehicles` membutuhkan `users`.
- `bookings` membutuhkan `users`, `vehicles`, dan `services`.
- `booking_status_logs` membutuhkan `bookings` dan `users`.

---

## 16. Eloquent Relationship Draft

### User Model

```php
public function vehicles()
{
    return $this->hasMany(Vehicle::class);
}

public function bookings()
{
    return $this->hasMany(Booking::class);
}
```

### Vehicle Model

```php
public function user()
{
    return $this->belongsTo(User::class);
}

public function bookings()
{
    return $this->hasMany(Booking::class);
}
```

### Service Model

```php
public function bookings()
{
    return $this->hasMany(Booking::class);
}
```

### Booking Model

```php
public function user()
{
    return $this->belongsTo(User::class);
}

public function vehicle()
{
    return $this->belongsTo(Vehicle::class);
}

public function service()
{
    return $this->belongsTo(Service::class);
}

public function statusLogs()
{
    return $this->hasMany(BookingStatusLog::class);
}
```

### BookingStatusLog Model

```php
public function booking()
{
    return $this->belongsTo(Booking::class);
}

public function changedBy()
{
    return $this->belongsTo(User::class, 'changed_by');
}
```

---

## 17. Frontend Type Reference

Frontend TypeScript type bisa mengikuti response API.

### User

```ts
export type UserRole = "customer" | "admin" | "mechanic";

export interface User {
  id: number;
  name: string;
  email: string;
  phone?: string | null;
  role: UserRole;
}
```

### Vehicle

```ts
export type TransmissionType = "manual" | "automatic";
export type FuelType = "gasoline" | "diesel" | "electric" | "hybrid";

export interface Vehicle {
  id: number;
  user_id: number;
  brand: string;
  model: string;
  year: number;
  plate_number: string;
  transmission_type?: TransmissionType | null;
  fuel_type?: FuelType | null;
  last_odometer?: number | null;
  color?: string | null;
}
```

### Service

```ts
export interface Service {
  id: number;
  name: string;
  slug: string;
  category?: string | null;
  description?: string | null;
  estimated_duration?: number | null;
  base_price: number;
  is_active: boolean;
}
```

### Booking

```ts
export type BookingStatus =
  | "pending"
  | "confirmed"
  | "in_progress"
  | "completed"
  | "cancelled";

export interface Booking {
  id: number;
  booking_code: string;
  user_id: number;
  vehicle_id: number;
  service_id: number;
  booking_date: string;
  booking_time: string;
  status: BookingStatus;
  complaint_note?: string | null;
  admin_note?: string | null;
  estimated_price?: number | null;
  final_price?: number | null;
  service_name_snapshot?: string | null;
  vehicle_plate_snapshot?: string | null;
  completed_at?: string | null;
  cancelled_at?: string | null;
}
```

---

## 18. Schema Notes for MVP

Keputusan schema MVP:

1. Role disimpan langsung di tabel `users`.
2. Branch belum dibuat di MVP.
3. Mechanic profile belum dibuat di MVP.
4. Booking hanya memilih satu service utama.
5. Multi-service booking belum masuk MVP.
6. Payment belum masuk MVP.
7. AI diagnostic belum masuk MVP.
8. Snapshot ringan digunakan pada booking untuk menjaga histori.
9. Soft delete digunakan pada tabel utama.
10. Status log digunakan untuk tracking progress.

---

## 19. Future Improvement

Pengembangan schema berikutnya:

1. Menambah `branches` untuk multi-cabang.
2. Menambah `mechanic_profiles` untuk dashboard mekanik.
3. Menambah `booking_services` jika satu booking bisa memiliki banyak service.
4. Menambah `payments` untuk pembayaran.
5. Menambah `service_notes` untuk catatan mekanik.
6. Menambah `notifications` untuk reminder.
7. Menambah `ai_diagnostics` untuk fitur AI diagnostic.
8. Menambah `roles` dan `permissions` jika authorization makin kompleks.

---

## 20. Final Recommendation

Untuk MVP Revora, gunakan schema sederhana dan normalized:

```txt
users
vehicles
services
bookings
booking_status_logs
```

Schema ini sudah cukup untuk membangun fitur utama:

```txt
Customer auth
Vehicle management
Service list
Booking service
Booking tracking
Admin booking management
Admin service management
```

Dengan desain ini, Revora tetap sederhana untuk dikerjakan, tetapi cukup profesional untuk portfolio fullstack berbasis React dan Laravel.
