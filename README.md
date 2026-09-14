# Perpustakaan Digital SMK — paketempat

Aplikasi web manajemen perpustakaan sekolah berbasis PHP native dan MySQL, dengan tiga peran pengguna: **Admin**, **Petugas**, dan **Siswa/Anggota**. Sistem mencakup katalog buku, peminjaman & pengembalian, denda keterlambatan, dan ulasan buku.

## Fitur Utama

### 👤 Admin
- Dashboard ringkasan data perpustakaan
- Kelola data buku (tambah, edit, hapus, kelola stok)
- Kelola data anggota (tambah, edit, hapus, aktif/nonaktif)
- Kelola transaksi peminjaman
- Moderasi ulasan buku (`ulasan.php`)
- Halaman bantuan

### 🧑‍💼 Petugas
- Dashboard petugas
- Proses peminjaman buku (`proses_pinjam.php`)
- Proses pengembalian buku (`proses_kembali.php`)
- Verifikasi & konfirmasi pembayaran denda (`verifikasi_denda.php`, `bayar_denda.php`)
- Pencarian anggota via AJAX (`cari_anggota_ajax.php`)
- Laporan peminjaman

### 🎓 Siswa / Anggota
- Dashboard dan katalog buku
- Pinjam buku (`pinjam.php`) dan lihat riwayat peminjaman (`riwayat.php`)
- Pengembalian buku (`kembalikan.php`) beserta cetak struk (`struk.php`)
- Pembayaran denda mandiri (`bayar_denda.php`)
- Beri ulasan & rating buku, serta membalas ulasan (`beri_ulasan.php`, `ulasan_balas.php`)
- Edit profil (`profil.php`)
- Halaman bantuan

### 🌐 Umum
- Halaman utama (`index.php`) dengan katalog buku publik
- Login multi-role & pendaftaran anggota (`login.php`, `daftar.php`)
- Logout (`logout.php`)

## Teknologi yang Digunakan

| Komponen        | Teknologi                                   |
|------------------|----------------------------------------------|
| Bahasa backend   | PHP (native, tanpa framework)                |
| Database         | MySQL / MariaDB (ekstensi `mysqli`)          |
| Frontend         | HTML, CSS, JavaScript                        |
| UI Framework     | Bootstrap 5.3.2 + Bootstrap Icons 1.11.3 (CDN) |
| Grafik/statistik | Chart.js 4.4.4 (CDN)                         |

## Struktur Direktori

```
paketempat/
├── admin/              # Halaman & aksi untuk role Admin
├── petugas/             # Halaman & aksi untuk role Petugas
├── siswa/                # Halaman & aksi untuk role Siswa/Anggota
├── config/
│   └── koneksi.php       # Konfigurasi koneksi database (mysqli)
├── includes/             # Navbar, footer, helper, dan pengecekan login
├── partials/              # Komponen tampilan yang dapat dipakai ulang
├── assets/
│   ├── css/               # File style.css
│   ├── js/                 # Script JS (detail buku, konfirmasi, dll.)
│   ├── img/                # Gambar statis
│   ├── uploads/             # Upload cover buku, bukti bayar, dll.
│   └── video/                # Aset video (jika ada)
├── index.php              # Halaman utama & katalog publik
├── login.php               # Login (admin/petugas/siswa)
├── daftar.php               # Pendaftaran anggota baru
├── logout.php                # Logout sesi
└── perpustakaan.sql            # Dump struktur & data database
```

## Struktur Database

Database: **`perpustakaan`**

| Tabel               | Deskripsi                                                              |
|---------------------|--------------------------------------------------------------------------|
| `admin`             | Akun admin (username, password, nama)                                  |
| `petugas`           | Akun petugas perpustakaan                                                |
| `anggota`           | Data anggota/siswa (NIS, kelas, no. HP, status aktif/nonaktif)          |
| `buku`              | Data buku (kode, ISBN, judul, pengarang, kategori, stok, kondisi, cover)|
| `peminjaman`        | Transaksi peminjaman & pengembalian, denda, status bayar denda          |
| `ulasan`            | Ulasan & rating buku oleh anggota (1–5), status aktif/disembunyikan      |
| `balasan_ulasan`    | Balasan terhadap ulasan (oleh siswa atau admin)                          |
| `log_stok`          | Riwayat perubahan stok buku                                             |

## Cara Instalasi (Local — XAMPP/Laragon)

1. **Clone / salin folder proyek**
   Letakkan folder `paketempat` ke dalam direktori server lokal, misalnya:
   - XAMPP: `C:\xampp\htdocs\paketempat`
   - Laragon: `C:\laragon\www\paketempat`

2. **Buat database**
   - Jalankan Apache & MySQL melalui XAMPP/Laragon.
   - Buka phpMyAdmin, buat database baru bernama **`perpustakaan`**.
   - Import file `perpustakaan.sql` ke database tersebut (tab *Import*).

3. **Cek konfigurasi koneksi**
   Sesuaikan `config/koneksi.php` bila perlu (default berikut biasanya sudah cocok untuk XAMPP/Laragon):
   ```php
   $host     = "localhost";
   $user     = "root";
   $password = "";
   $database = "perpustakaan";
   ```

4. **Jalankan aplikasi**
   Buka browser dan akses:
   ```
   http://localhost/paketempat/
   ```

5. **Login**
   Gunakan akun admin/petugas/siswa yang ada pada dump `perpustakaan.sql`, atau daftar akun anggota baru melalui halaman **Daftar**.

## Kebutuhan Sistem

- PHP 7.4 atau lebih baru (ekstensi `mysqli` aktif)
- MySQL / MariaDB
- Web server Apache (disarankan XAMPP/Laragon untuk pengembangan lokal)
- Koneksi internet (untuk memuat Bootstrap, Bootstrap Icons, dan Chart.js dari CDN)

## Catatan

- Folder `assets/uploads/` digunakan untuk menyimpan file upload seperti cover buku dan bukti pembayaran denda — pastikan folder ini memiliki izin tulis (*writable*).
- Zona waktu aplikasi diatur ke `Asia/Jakarta` pada `config/koneksi.php`.
