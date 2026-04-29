# 🍽️ Tempat-in

> **Platform reservasi kafe & restoran berbasis web** — pesan meja, pre-order menu, dan bayar dalam satu sistem digital terpadu.

<p align="center">
  <img src="https://img.shields.io/badge/Laravel-12.x-FF2D20?style=for-the-badge&logo=laravel&logoColor=white"/>
  <img src="https://img.shields.io/badge/PHP-8.2+-777BB4?style=for-the-badge&logo=php&logoColor=white"/>
  <img src="https://img.shields.io/badge/TailwindCSS-3.x-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white"/>
  <img src="https://img.shields.io/badge/Midtrans-Payment-003D6A?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Status-MVP%20Beta-yellow?style=for-the-badge"/>
</p>

---

## 📋 Daftar Isi

- [Tentang Proyek](#-tentang-proyek)
- [Tim Pengembang](#-tim-pengembang)
- [SQA Documentation](#-sqa-documentation)
- [Testing Tools](#-testing-tools). 
- [Fitur Utama](#-fitur-utama)
- [Teknologi](#-teknologi)
- [Arsitektur Sistem](#-arsitektur-sistem)
- [Skema Database](#-skema-database)
- [Peran Pengguna](#-peran-pengguna)
- [Instalasi](#-instalasi)


---

## 📖 Tentang Proyek

**Tempat-in** hadir untuk menjawab kebutuhan digitalisasi industri F&B lokal. Sistem ini mengintegrasikan tiga proses utama — *pemesanan meja*, *pre-order makanan*, dan *pembayaran digital* — dalam satu platform yang efisien dan responsif.

Proyek ini dikembangkan sebagai bagian dari mata kuliah **Software Quality Assurance (SQA)**, dengan fokus pada penerapan standar kualitas perangkat lunak dari tahap perencanaan hingga pengujian.

---
---

## 👨‍💻 Tim Pengembang

| Nama | NIM | Role |
|---|---|---|
| **Tryas** | 20231310075 | Project Manager & System Analyst |
| **Salma** | 20231310085 | UI/UX Designer & Technical Writer |
| **Fauzan** | 202310109 | Software Engineer & Quality Assurance |

---
## 📁 SQA Documentation

Seluruh dokumentasi Software Quality Assurance tersedia di direktori [`SQA_Development/`](./SQA_Development):

## 📂 Repository Structure

```
SQA_Project/
│
├── 📁 Software Design Documentation/    # Arsitektur & Desain Sistem
│   ├── 📁 Deskripsi Umum/
│   ├── 📁 Pendahuluan/
│   └── 📁 Software Design/              # ERD, UML, UI/UX, Flowchart
│
├── 📁 Software Requirements Specification/  # Spesifikasi Kebutuhan
│   ├── Use Case Diagram & Narasi
│   ├── Functional & Non-Functional Requirements
│   └── Business Rules & Constraints
│
├── 📁 Software Testing Documentation/      # Panduan Pengguna Akhir
│   ├── 📁 Blackbox
│   ├── 📁 Whitebox
│   └── 📁 Greybox
│
├── 📁 Software User Documentation/      # Panduan Pengguna Akhir
│   └── User Manual (fitur per modul)
│
├── 📁 Test Plan/                        # Inti Aktivitas SQA
│   ├── 📄 Test Scenarios
│   ├── 📄 Test Cases
│   ├── 📄 Defect / Bug Report
│   └── 📄 Test Execution Result
└── 📄 README.md                         # Dokumen ini
```
## 🛠️ Testing Tools 
### Backend & API Testing

| Tool | Kegunaan |
|---|---|
| **Postman / Insomnia** | Pengujian endpoint API (REST), validasi response, dan autentikasi token |
| **PHPUnit** | Unit testing & feature testing pada layer backend Laravel |

### Manajemen & Pelaporan

| Tool | Kegunaan |
|---|---|
| **Git** | Pengecekan versi, maaintain local, pull repo |
| **GitHub** | Repository online, update documentation |
| **GitHub Issues** | Pelacakan bug dan defect secara terpusat |
| **Markdown Reports** | Dokumentasi hasil test di dalam repositori ini |


---


## ✨ Fitur Utama

| Fitur | Deskripsi | Status |
|---|---|:---:|
| 🔐 **Autentikasi** | Register, login, verifikasi email | ✅ |
| 📅 **Reservasi Meja** | Pilih restoran, meja, tanggal & waktu | ✅ |
| 🍜 **Pre-order Menu** | Pesan makanan sebelum datang | ✅ |
| 📦 **Paket Booking** | Pilih paket khusus (VIP, Standar, dll.) | ✅ |
| 💳 **Pembayaran Digital** | Integrasi Midtrans Snap (down payment 50%) | ✅ |
| 🔁 **Reschedule** | Pengajuan perubahan jadwal reservasi (H-1) | ✅ |
| 📜 **Riwayat Reservasi** | Pantau status semua reservasi | ✅ |
| 🏠 **Dashboard Admin** | Kelola menu, meja, reservasi, & paket | ✅ |
| 👑 **Dashboard Superadmin** | Kelola semua restoran & user | ✅ |

---

## 🛠️ Teknologi

```
Frontend   : Laravel Blade + Tailwind CSS
Backend    : Laravel 12 (PHP 8.2+)
Database   : MySQL (SQLite untuk testing)
Payment    : Midtrans Snap API
Build Tool : Vite + npm
Testing    : PHPUnit 11
```

---

## 🏗️ Arsitektur Sistem

```
Tempat-in/
├── app/
│   ├── Http/
│   │   ├── Controllers/
│   │   │   ├── Admin/          # BookingPackage, MenuItem, Reservation, Restaurant, Table
│   │   │   ├── Auth/           # PartnerRegistration
│   │   │   ├── SuperAdmin/     # Dashboard, Restaurant, User
│   │   │   ├── AuthController.php
│   │   │   ├── ReservationController.php
│   │   │   └── MidtransWebhookController.php
│   │   └── Middleware/
│   │       └── RoleMiddleware.php   # Guard: user | admin | superadmin
│   ├── Models/                  # User, Reservation, Restaurant, dll.
│   └── Providers/
├── database/
│   ├── migrations/              # 13 migration files
│   ├── seeders/
│   └── factories/
├── resources/views/             # Blade templates per role
├── routes/web.php               # Route terpisah per role
├── tests/
│   ├── Feature/
│   └── Unit/
└── SQA_Development/             # Dokumentasi SQA lengkap
```

---

## 🗄️ Skema Database

```
users ──────────────┬──── restaurants ──┬──── menu_items
                    │                   ├──── booking_packages
                    │                   └──── tables
                    │
                    └──── reservations ─┬──── menu_item_reservation (pivot)
                                        ├──── booking_packages (FK)
                                        └──── tables (FK)
```

Tabel utama: `users`, `restaurants`, `reservations`, `menu_items`, `booking_packages`, `tables`, `menu_item_reservation`

---

## 👥 Peran Pengguna

| Role | Akses |
|---|---|
| 👤 **User** | Lihat restoran, buat reservasi, pre-order, bayar, reschedule, riwayat |
| 🏪 **Admin** | Kelola restoran milik sendiri, menu, meja, paket, & konfirmasi reservasi |
| 🛡️ **Superadmin** | Kelola semua restoran, semua user, monitoring platform |

---

## 🚀 Instalasi

### Prasyarat

- PHP >= 8.2
- Composer
- Node.js & npm
- MySQL

### Langkah Instalasi

```bash
# 1. Clone repository
git clone https://github.com/Lputaa/SQA_test.git
cd SQA_test
git checkout Beta

# 2. Install dependencies
composer install
npm install

# 3. Konfigurasi environment
cp .env.example .env
php artisan key:generate

# 4. Isi konfigurasi database & Midtrans di .env
# DB_DATABASE, DB_USERNAME, DB_PASSWORD
# MIDTRANS_SERVER_KEY, MIDTRANS_CLIENT_KEY

# 5. Migrasi & seeder database
php artisan migrate --seed

# 6. Jalankan aplikasi
composer run dev
```

Aplikasi akan berjalan di `http://localhost:8000`

### Menjalankan Tests

```bash
php artisan test
```

---
