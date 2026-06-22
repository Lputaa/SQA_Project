# 🧪 White Box Testing Documentation — Tempat-in

## 📌 Deskripsi Project

**Tempat-in** merupakan aplikasi reservasi restoran berbasis web yang dikembangkan menggunakan framework **Laravel 12**. Sistem ini dirancang untuk membantu pengguna melakukan:

- reservasi meja restoran
- pemesanan menu makanan
- pengelolaan pembayaran
- manajemen reservasi pengguna
- monitoring reservasi oleh admin restoran

Project ini mengimplementasikan berbagai proses transactional seperti:
- booking reservation
- availability checking
- payment processing
- reservation status management
- data validation

Karena sistem memiliki kompleksitas logika dan transaksi yang cukup tinggi, maka dilakukan proses **White Box Testing** untuk memastikan kualitas, stabilitas, dan validitas alur sistem.

---

# 🎯 Tujuan Dokumentasi

Dokumentasi ini dibuat untuk:

- mendokumentasikan proses pengujian White Box Testing
- menganalisis struktur logika aplikasi
- mengidentifikasi jalur eksekusi program
- memastikan seluruh proses reservasi berjalan dengan benar
- mengevaluasi kualitas source code dan aliran data
- memenuhi kebutuhan akademik mata kuliah Software Quality Assurance

---

# 🔬 Metode White Box Testing yang Digunakan

Project Tempat-in menggunakan 4 metode utama White Box Testing:

| No | Metode | Fokus Pengujian |
|---|---|---|
| 1 | Basis Path Testing | Jalur independen & Cyclomatic Complexity |
| 2 | Control Flow Testing | Alur kontrol & percabangan logika |
| 3 | Data Flow Testing | Aliran data & penggunaan variabel |
| 4 | Loop Testing | Struktur perulangan & iterasi data |

---

# 📂 Struktur Dokumentasi

```text
/docs
│
├── README.md
├── basis-path-testing.md
├── control-flow-testing.md
├── data-flow-testing.md
└── loop-testing.md
```

---

# ⚙️ Teknologi yang Digunakan

| Kategori | Teknologi |
|---|---|
| Backend | Laravel 12 |
| Frontend | Blade + TailwindCSS |
| Database | MySQL |
| Payment Gateway | Midtrans |
| Testing | PHPUnit |
| Visualization | Mermaid Diagram |
| Static Analysis | Larastan |

---

# 🛠️ Tools Pengujian

| Tool | Fungsi |
|---|---|
| PHPUnit | Unit & Feature Testing |
| Laravel HTTP Test | Simulasi request |
| Xdebug | Code coverage |
| Mermaid | CFG & Flow Visualization |
| Larastan | Static code analysis |

---

# 📊 Fokus Pengujian Sistem

Area utama yang diuji:

- reservation booking process
- table availability checking
- payment transaction flow
- reservation status update
- data validation
- rollback transaction
- menu iteration process

---

# ⚠️ Temuan Utama Pengujian

Berdasarkan hasil pengujian White Box Testing ditemukan beberapa poin penting:

| Temuan | Status |
|---|---|
| Jalur logika reservasi berjalan benar | ✅ |
| Data flow transaksi konsisten | ✅ |
| Rollback payment berhasil | ✅ |
| Loop iteration berjalan stabil | ✅ |
| Potensi race condition booking masih ada | ⚠️ |

---

# 🚨 Rekomendasi Perbaikan

Beberapa rekomendasi pengembangan sistem:

```php
lockForUpdate()
```

atau:

```sql
UNIQUE(table_id, reservation_date, reservation_time)
```

untuk mencegah:
- double booking
- concurrent reservation issue
- inconsistent transaction data

Selain itu direkomendasikan:
- refactor business logic ke service layer
- implementasi policy authorization Laravel
- peningkatan automated testing coverage
- optimasi database indexing

---

# 📖 Kesimpulan

Hasil White Box Testing menunjukkan bahwa sistem Tempat-in:

- memiliki struktur logika yang cukup baik
- mampu menangani proses reservasi dengan benar
- memiliki alur transaksi yang konsisten
- telah memenuhi sebagian besar validasi logika internal

Namun sistem masih memerlukan:
- hardening concurrency
- peningkatan scalability
- refactor architecture

agar lebih siap digunakan pada skala produksi yang lebih besar.

---

# 👨‍💻 Penyusun

**Project:** Tempat-in  
**Mata Kuliah:** Software Quality Assurance  
**Metode Pengujian:** White Box Testing  
**Framework:** Laravel 12

---

# 📚 Referensi

1. Pressman, R. S. (2020). *Software Engineering: A Practitioner's Approach*.
2. McCabe, T. J. (1976). *A Complexity Measure*. IEEE Transactions on Software Engineering.
3. Ndaumanu, R. I. (2023). *Pengujian Sistem Informasi Berbasis Website dengan Basis Path Testing*.
4. Suprihadi, D. (2025). *Materi White Box Testing — Software Quality Assurance*.

---

> *"Software quality begins with software testing."*