# 🎭 Behaviour Testing (BDD)

> **Model Black Box Testing #7** — *Logic-Based Testing*  
> **Project:** Tempat.in — Restaurant Reservation Platform  
> **Metode:** Black Box Behaviour Testing

---

# 📖 1. Definisi

**Behaviour Testing** (juga dikenal sebagai **Behavior-Driven Development / BDD**) adalah pendekatan pengujian perangkat lunak yang berfokus pada perilaku yang diharapkan dari suatu program dari sudut pandang pengguna.

Metode ini digunakan untuk:
- menguji alur sistem secara end-to-end,
- memastikan interaksi antar modul berjalan sesuai spesifikasi,
- memvalidasi perilaku sistem berdasarkan aksi pengguna.

Pada project **Tempat.in**, Behaviour Testing digunakan untuk menguji keseluruhan flow utama aplikasi reservasi restoran mulai dari registrasi hingga pembayaran reservasi.

---

# 🎯 2. Tujuan Pengujian

| No | Tujuan |
|---|---|
| 1 | Memvalidasi user journey utama aplikasi |
| 2 | Menguji interaksi antar modul sistem |
| 3 | Memastikan state reservation berjalan normal |
| 4 | Menguji validasi autentikasi dan otorisasi |
| 5 | Menguji respons sistem terhadap kondisi gagal |
| 6 | Memastikan proses pembayaran berjalan sesuai flow |

---

# 💻 3. Modul yang Diuji

## User Journey

```text
Register → Verifikasi Email → Login → Cari Restoran → Reservasi → Pembayaran → Riwayat Reservasi
```

---

## Modul Sistem

| Modul | Fungsi |
|---|---|
| Authentication | Login, Register, Logout |
| Email Verification | Aktivasi akun |
| Restaurant Listing | Menampilkan daftar restoran |
| Restaurant Detail | Menampilkan detail restoran |
| Reservation | Membuat reservasi |
| Payment | Pembayaran reservasi |
| Reservation History | Riwayat reservasi user |

---

# 👤 4. Aktor Pengguna

| Aktor | Deskripsi |
|---|---|
| Guest | Pengunjung belum login |
| User | Pengguna terdaftar |
| Verified User | User yang sudah verifikasi email |
| Admin Restaurant | Pengelola restoran |
| Super Admin | Pengelola platform |

---

# 🔷 5. Sequence Diagram

## 5.1 Flow Login User

```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant Backend
    participant Database

    User->>Frontend: Buka halaman login
    Frontend-->>User: Tampilkan form login

    User->>Frontend: Input email & password
    Frontend->>Backend: POST /login
    Backend->>Database: Validasi user

    alt Login berhasil
        Database-->>Backend: User valid
        Backend-->>Frontend: Session/token
        Frontend-->>User: Redirect dashboard
    else Login gagal
        Database-->>Backend: User invalid
        Backend-->>Frontend: Error login
        Frontend-->>User: Tampilkan pesan error
    end
```

---

## 5.2 Flow Reservasi Restoran

```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant Backend
    participant Database
    participant PaymentGateway

    User->>Frontend: Pilih restoran
    Frontend->>Backend: GET restaurant detail
    Backend->>Database: Fetch data restoran
    Database-->>Backend: Return data
    Backend-->>Frontend: Return detail restoran

    User->>Frontend: Isi form reservasi
    Frontend->>Backend: POST reservation
    Backend->>Backend: Validasi data

    alt Data valid
        Backend->>Database: Simpan reservasi
        Database-->>Backend: Reservation created
        Backend->>PaymentGateway: Generate payment token
        PaymentGateway-->>Backend: Payment token
        Backend-->>Frontend: Redirect payment
    else Data invalid
        Backend-->>Frontend: Validation error
    end
```

---

# 🔶 6. Activity Diagram

## 6.1 Activity Diagram — Registrasi User

```mermaid
flowchart TD
    START([Mulai]) --> A[Buka halaman register]
    A --> B[Isi form register]
    B --> C{Validasi input}

    C -->|Invalid| D[Tampilkan error]
    D --> B

    C -->|Valid| E{Email sudah digunakan?}

    E -->|Ya| F[Tampilkan email sudah digunakan]
    F --> B

    E -->|Tidak| G[Simpan user]
    G --> H[Kirim email verifikasi]
    H --> I[Redirect login]

    I --> END([Selesai])
```

---

## 6.2 Activity Diagram — Reservasi

```mermaid
flowchart TD
    START([Mulai]) --> AUTH{User login?}

    AUTH -->|Tidak| LOGIN[Redirect login]
    LOGIN --> END1([End])

    AUTH -->|Ya| A[Pilih restoran]
    A --> B[Pilih tanggal reservasi]
    B --> C[Isi jumlah tamu]
    C --> D[Submit reservasi]

    D --> E{Validasi data}

    E -->|Invalid| F[Tampilkan error]
    F --> C

    E -->|Valid| G[Simpan reservasi]
    G --> H[Generate payment]
    H --> I[Redirect pembayaran]

    I --> END([Selesai])
```

---

# 🔵 7. Statechart Diagram

## 7.1 User State

```mermaid
stateDiagram-v2
    [*] --> Guest

    Guest --> Registered : Register berhasil
    Registered --> Verified : Email verification
    Verified --> LoggedIn : Login berhasil

    LoggedIn --> LoggedOut : Logout
    LoggedOut --> LoggedIn : Login ulang

    LoggedIn --> Suspended : Akun diblokir
    Suspended --> LoggedIn : Akun dipulihkan
```

---

## 7.2 Reservation State

```mermaid
stateDiagram-v2
    [*] --> Draft

    Draft --> PendingPayment : Reservasi dibuat
    PendingPayment --> Confirmed : Pembayaran berhasil
    PendingPayment --> Cancelled : Dibatalkan user
    PendingPayment --> Expired : Payment timeout

    Confirmed --> Completed : Reservasi selesai
```

---

# 🟣 8. Collaboration Diagram

```mermaid
graph TB

    USER[👤 User]
    FRONTEND[🌐 Frontend]
    CTRL[Reservation Controller]
    VALIDATOR[Validator]
    SERVICE[Reservation Service]
    DB[(Database)]
    PAYMENT[💳 Payment Gateway]

    USER -->|1. Input reservasi| FRONTEND
    FRONTEND -->|2. POST reservation| CTRL
    CTRL -->|3. Validate request| VALIDATOR
    VALIDATOR -->|4. Validation result| CTRL
    CTRL -->|5. Store reservation| SERVICE
    SERVICE -->|6. Insert reservation| DB
    SERVICE -->|7. Generate payment| PAYMENT
    PAYMENT -->|8. Payment token| SERVICE
    SERVICE -->|9. Return response| CTRL
    CTRL -->|10. Success response| FRONTEND
    FRONTEND -->|11. Tampilkan pembayaran| USER
```

---

# 🧪 9. BDD Scenario (Gherkin)

```gherkin
Feature: Reservation System
  Sebagai pengguna Tempat.in
  Saya ingin melakukan reservasi restoran
  Agar saya dapat memesan tempat secara online

  Background:
    Given saya memiliki akun yang sudah terverifikasi

  Scenario: Login berhasil
    When saya membuka halaman login
    And saya mengisi email dan password yang valid
    And saya menekan tombol Login
    Then saya diarahkan ke dashboard

  Scenario: Reservasi berhasil
    Given saya sudah login
    When saya memilih restoran
    And saya memilih tanggal reservasi
    And saya memasukkan jumlah tamu
    And saya submit reservasi
    Then reservasi berhasil dibuat
    And saya diarahkan ke halaman pembayaran
```

---

# 📊 10. Hasil Eksekusi

| Scenario | Expected Result | Status |
|---|---|---|
| Login berhasil | Redirect dashboard | ⏳ Pending |
| Reservasi berhasil | Reservation created | ⏳ Pending |
| Pembayaran berhasil | Status confirmed | ⏳ Pending |

---

# 🐛 11. Prediksi Temuan Bug

| ID | Severity | Deskripsi |
|---|---|---|
| BHV-001 | High | User dapat bypass email verification |
| BHV-002 | Medium | Reservation tetap tersimpan saat payment gagal |
| BHV-003 | Medium | Tidak ada validasi double booking |
| BHV-004 | Low | Redirect login tidak konsisten |

---

# 📚 Referensi

1. Suprihadi, D. (2025). Software Quality — Black Box Testing.
2. Myers, G. J. The Art of Software Testing.
3. Laravel Documentation.
4. Mermaid Documentation.
