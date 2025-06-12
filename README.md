# Lab7 PHP CodeIgniter 4 - Login System, Pagination, Search & File Upload
Aplikasi web sederhana yang dibangun menggunakan CodeIgniter 4 untuk praktikum pemrograman web, mengimplementasikan sistem login, pagination, pencarian, dan upload file   gambar. Proyek ini mencakup fitur manajemen artikel dengan autentikasi untuk admin serta antarmuka publik untuk menampilkan artikel kepada pengunjung. Proyek ini dirancang sebagai bagian dari tugas praktikum 4, 5, dan 6 untuk mempelajari konsep dasar pengembangan web menggunakan framework PHP.

## Fitur Utama

- Sistem Login: Autentikasi pengguna dengan email dan password menggunakan password_hash() dan password_verify().
  Manajemen Artikel: Fitur CRUD (Create, Read, Update, Delete) untuk artikel, khusus untuk admin.
- Pagination: Pembatasan data artikel per halaman dengan navigasi halaman.
  Pencarian: Fitur pencarian artikel berdasarkan judul menggunakan query parameter.
- Upload Gambar: Mendukung unggah gambar untuk artikel dengan validasi file.
  Filter Autentikasi: Melindungi halaman admin dari akses tidak sah menggunakan filter.
- Antarmuka Publik: Menampilkan daftar artikel dan detail artikel untuk pengunjung umum.
- Session Management: Pengelolaan session untuk menyimpan data pengguna yang login.
- Database Seeder: Membuat data dummy untuk pengujian login admin.


## Teknologi yang Digunakan

- PHP: Versi 7.4 atau lebih tinggi
- CodeIgniter 4: Framework PHP untuk pengembangan aplikasi
- MySQL/MariaDB: Database untuk menyimpan data user dan artikel
- HTML5 & CSS3: Untuk antarmuka pengguna
- Bootstrap-inspired CSS: Untuk styling dasar yang responsif


## Struktur Folder
Berikut adalah struktur folder utama proyek:
```
lab7_php_ci/
├── app/
│   ├── Config/
│   │   ├── Filters.php
│   │   └── Routes.php
│   ├── Controllers/
│   │   ├── BaseController.php
│   │   ├── Artikel.php
│   │   └── User.php
│   ├── Database/
│   │   └── Seeds/
│   │       └── UserSeeder.php
│   ├── Filters/
│   │   └── Auth.php
│   ├── Models/
│   │   ├── ArtikelModel.php
│   │   └── UserModel.php
│   └── Views/
│       ├── artikel/
│       │   ├── admin_index.php
│       │   ├── form_add.php
│       │   ├── form_edit.php
│       │   ├── index.php
│       │   └── detail.php
│       └── user/
│           ├── index.php
│           └── login.php
├── public/
│   ├── gambar/
│   ├── style.css
│   └── index.php
├── writable/
│   ├── session/
│   └── uploads/
└── .env
```

## Tata Cara Penginstalan
1. Clone Repository
```git clone https://github.com/username/lab7_php_ci.git```
Catatan: Ganti username dengan nama pengguna GitHub Anda.
2. Konfigurasi File .env
Salin file env menjadi .env:
```cp env .env```
Edit file .env untuk mengatur konfigurasi database dan aplikasi:
```
CI_ENVIRONMENT = development

app.baseURL = 'http://localhost:8080'

database.default.hostname = localhost
database.default.database = lab7_ci4
database.default.username = root
database.default.password =
database.default.DBDriver = MySQLi

session.driver = 'CodeIgniter\Session\Handlers\FileHandler'
session.cookieName = 'ci_session'
session.expiration = 7200
session.savePath = writable/session
session.regenerateDestroy = false
```

Sesuaikan database.default.username dan database.default.password dengan kredensial MySQL Anda.
Pastikan app.baseURL sesuai dengan URL aplikasi Anda (misalnya, http://localhost:8080).

4. Setup Database

Buat database baru bernama lab7_ci4 di MySQL:
```
CREATE DATABASE lab7_ci4;


Impor skema tabel dengan menjalankan SQL berikut di MySQL:
USE lab7_ci4;

-- Tabel user
CREATE TABLE user (
    id INT(11) AUTO_INCREMENT,
    username VARCHAR(200) NOT NULL,
    useremail VARCHAR(200),
    userpassword VARCHAR(200),
    PRIMARY KEY(id)
);

-- Tabel artikel
CREATE TABLE artikel (
    id INT(11) AUTO_INCREMENT,
    judul VARCHAR(200) NOT NULL,
    isi TEXT,
    gambar VARCHAR(200),
    status TINYINT(1) DEFAULT 0,
    slug VARCHAR(200),
    PRIMARY KEY(id)
);
```

## Jalankan seeder untuk membuat data dummy user (admin):
```php spark db:seed UserSeeder```

## 5. Jalankan Aplikasi
Jalankan server development CodeIgniter menggunakan perintah:
```php spark serve```

- Aplikasi akan tersedia di http://localhost:8080.


## Troubleshooting
1. Error "Unable to connect to database"

## Solusi:
- Pastikan MySQL service berjalan.
- Periksa kredensial database di file .env (username, password, hostname, dll.).
- Pastikan database lab7_ci4 sudah dibuat.

## 2. File Upload Tidak Berfungsi

## Solusi:
Pastikan direktori public/gambar sudah dibuat.
Berikan izin tulis: chmod -R 755 public/gambar.
Periksa pengaturan upload_max_filesize dan post_max_size di php.ini.

## 3. Session Tidak Berfungsi

## Solusi:
Pastikan direktori writable/session ada dan memiliki izin tulis: chmod -R 755 writable/session.
Periksa pengaturan session di .env (session.driver, session.savePath).

## 4. Route Tidak Ditemukan

## Solusi:
Pastikan file app/Config/Routes.php dikonfigurasi dengan benar.
Jalankan php spark routes untuk memeriksa daftar route yang tersedia.

## 5. Halaman Admin Tidak Dapat Diakses

## Solusi:
Pastikan Anda sudah login menggunakan kredensial yang benar.
Periksa filter autentikasi di app/Filters/Auth.php dan app/Config/Filters.php.




Perintah CLI yang Berguna

## Menjalankan server development:
```php spark serve```


## Membuat controller baru:
```php spark make:controller NamaController```


## Membuat model baru:
```php spark make:model NamaModel```


## Membuat seeder:
```php spark make:seeder NamaSeeder```


## Menjalankan seeder:
```php spark db:seed NamaSeeder```


## Melihat daftar routes:
```php spark routes```


## Membersihkan cache:
```php spark cache:clear```




## Kesimpulan Praktikum
Proyek ini mengimplementasikan konsep-konsep penting dalam pengembangan web menggunakan CodeIgniter 4:
## Praktikum 4 - Modul Login

- Autentikasi dan Otorisasi: Sistem login dengan verifikasi password menggunakan password_hash() dan password_verify().
- Session Management: Pengelolaan session untuk menyimpan data pengguna yang login.
- Auth Filter: Melindungi halaman admin dari akses tidak sah.
- Database Seeder: Membuat data dummy untuk pengujian.
- MVC Pattern: Pemisahan logic antara Model, View, dan Controller.

## Praktikum 5 - Pagination dan Pencarian

- Pagination: Pembatasan data per halaman menggunakan method paginate().
- Search Function: Pencarian artikel berdasarkan judul dengan method like().
- Query Parameter: Menangani parameter pencarian dengan getVar().
- Pager Links: Navigasi halaman dengan mempertahankan parameter pencarian.

## Praktikum 6 - Upload File Gambar

- File Upload: Menangani upload gambar menggunakan method getFile().
- File Validation: Validasi file untuk keamanan.
- File Management: Menyimpan file ke direktori public/gambar.
- Form Handling: Menggunakan enctype="multipart/form-data" untuk form upload.
