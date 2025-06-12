## Lab7 PHP CodeIgniter 4 - Login System, Pagination, Search & File Upload
- Aplikasi web sederhana yang dibangun menggunakan CodeIgniter 4 untuk praktikum pemrograman web, mengimplementasikan sistem login, pagination, pencarian, dan upload file   gambar. Proyek ini mencakup fitur manajemen artikel dengan autentikasi untuk admin serta antarmuka publik untuk menampilkan artikel kepada pengunjung. Proyek ini dirancang sebagai bagian dari tugas praktikum 4, 5, dan 6 untuk mempelajari konsep dasar pengembangan web menggunakan framework PHP.

Fitur Utama

Sistem Login: Autentikasi pengguna dengan email dan password menggunakan password_hash() dan password_verify().
Manajemen Artikel: Fitur CRUD (Create, Read, Update, Delete) untuk artikel, khusus untuk admin.
Pagination: Pembatasan data artikel per halaman dengan navigasi halaman.
Pencarian: Fitur pencarian artikel berdasarkan judul menggunakan query parameter.
Upload Gambar: Mendukung unggah gambar untuk artikel dengan validasi file.
Filter Autentikasi: Melindungi halaman admin dari akses tidak sah menggunakan filter.
Antarmuka Publik: Menampilkan daftar artikel dan detail artikel untuk pengunjung umum.
Session Management: Pengelolaan session untuk menyimpan data pengguna yang login.
Database Seeder: Membuat data dummy untuk pengujian login admin.


Teknologi yang Digunakan

PHP: Versi 7.4 atau lebih tinggi
CodeIgniter 4: Framework PHP untuk pengembangan aplikasi
MySQL/MariaDB: Database untuk menyimpan data user dan artikel
Composer: Manajemen dependensi PHP
HTML5 & CSS3: Untuk antarmuka pengguna
Bootstrap-inspired CSS: Untuk styling dasar yang responsif


Prasyarat
Sebelum menginstal aplikasi, pastikan Anda memiliki:

PHP 7.4 atau lebih tinggi
MySQL atau MariaDB
Composer untuk mengelola dependensi
Web server (Apache/Nginx) atau PHP built-in server
Git untuk mengkloning repository
Akses ke terminal/command line


Struktur Folder
Berikut adalah struktur folder utama proyek:
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


Tata Cara Penginstalan
1. Clone Repository
Kloning proyek dari GitHub ke direktori lokal Anda:
git clone https://github.com/username/lab7_php_ci.git
cd lab7_php_ci

Catatan: Ganti username dengan nama pengguna GitHub Anda.
2. Install Dependensi
Jalankan perintah berikut untuk menginstal dependensi CodeIgniter melalui Composer:
composer install

3. Konfigurasi File .env

Salin file env menjadi .env:
cp env .env


Edit file .env untuk mengatur konfigurasi database dan aplikasi:
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


Sesuaikan database.default.username dan database.default.password dengan kredensial MySQL Anda.
Pastikan app.baseURL sesuai dengan URL aplikasi Anda (misalnya, http://localhost:8080).



4. Setup Database

Buat database baru bernama lab7_ci4 di MySQL:
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


Jalankan seeder untuk membuat data dummy user (admin):
php spark db:seed UserSeeder

Ini akan membuat akun admin dengan kredensial:

Email: admin@email.com
Password: admin123



5. Buat Direktori untuk Upload Gambar

Buat direktori public/gambar:
mkdir public/gambar


Berikan izin tulis pada direktori tersebut:
chmod -R 755 public/gambar



6. Konfigurasi Session
Pastikan direktori writable/session ada dan memiliki izin tulis:
mkdir writable/session
chmod -R 755 writable/session

7. Jalankan Aplikasi
Jalankan server development CodeIgniter menggunakan perintah:
php spark serve

Aplikasi akan tersedia di http://localhost:8080.

Cara Penggunaan
1. Testing Login

URL: http://localhost:8080/user/login
Email: admin@email.com
Password: admin123

2. URL dan Fitur yang Dapat Diakses
URL Publik (Tanpa Login)

http://localhost:8080/ - Halaman utama
http://localhost:8080/artikel - Daftar artikel publik
http://localhost:8080/artikel/slug-artikel - Detail artikel
http://localhost:8080/user - Daftar user
http://localhost:8080/user/login - Form login

URL Admin (Perlu Login)

http://localhost:8080/admin/artikel - Dashboard admin artikel
http://localhost:8080/admin/artikel/add - Tambah artikel baru
http://localhost:8080/admin/artikel/edit/1 - Edit artikel dengan ID 1
http://localhost:8080/admin/artikel/delete/1 - Hapus artikel dengan ID 1
http://localhost:8080/user/logout - Logout dan kembali ke login


Troubleshooting
1. Error "Unable to connect to database"

Solusi:
Pastikan MySQL service berjalan.
Periksa kredensial database di file .env (username, password, hostname, dll.).
Pastikan database lab7_ci4 sudah dibuat.



2. File Upload Tidak Berfungsi

Solusi:
Pastikan direktori public/gambar sudah dibuat.
Berikan izin tulis: chmod -R 755 public/gambar.
Periksa pengaturan upload_max_filesize dan post_max_size di php.ini.



3. Session Tidak Berfungsi

Solusi:
Pastikan direktori writable/session ada dan memiliki izin tulis: chmod -R 755 writable/session.
Periksa pengaturan session di .env (session.driver, session.savePath).



4. Route Tidak Ditemukan

Solusi:
Pastikan file app/Config/Routes.php dikonfigurasi dengan benar.
Jalankan php spark routes untuk memeriksa daftar route yang tersedia.



5. Halaman Admin Tidak Dapat Diakses

Solusi:
Pastikan Anda sudah login menggunakan kredensial yang benar.
Periksa filter autentikasi di app/Filters/Auth.php dan app/Config/Filters.php.




Perintah CLI yang Berguna

Menjalankan server development:
php spark serve


Membuat controller baru:
php spark make:controller NamaController


Membuat model baru:
php spark make:model NamaModel


Membuat seeder:
php spark make:seeder NamaSeeder


Menjalankan seeder:
php spark db:seed NamaSeeder


Melihat daftar routes:
php spark routes


Membersihkan cache:
php spark cache:clear




Kesimpulan Praktikum
Proyek ini mengimplementasikan konsep-konsep penting dalam pengembangan web menggunakan CodeIgniter 4:
Praktikum 4 - Modul Login

Autentikasi dan Otorisasi: Sistem login dengan verifikasi password menggunakan password_hash() dan password_verify().
Session Management: Pengelolaan session untuk menyimpan data pengguna yang login.
Auth Filter: Melindungi halaman admin dari akses tidak sah.
Database Seeder: Membuat data dummy untuk pengujian.
MVC Pattern: Pemisahan logic antara Model, View, dan Controller.

Praktikum 5 - Pagination dan Pencarian

Pagination: Pembatasan data per halaman menggunakan method paginate().
Search Function: Pencarian artikel berdasarkan judul dengan method like().
Query Parameter: Menangani parameter pencarian dengan getVar().
Pager Links: Navigasi halaman dengan mempertahankan parameter pencarian.

Praktikum 6 - Upload File Gambar

File Upload: Menangani upload gambar menggunakan method getFile().
File Validation: Validasi file untuk keamanan.
File Management: Menyimpan file ke direktori public/gambar.
Form Handling: Menggunakan enctype="multipart/form-data" untuk form upload.

Keuntungan Menggunakan CodeIgniter 4

Framework ringan dengan performa cepat.
Fitur bawaan seperti pagination, validation, dan session.
Keamanan bawaan seperti CSRF dan XSS filtering.
Sistem routing yang fleksibel dengan filter.
Query builder untuk mencegah SQL injection.

Konsep Keamanan

Password Hashing: Enkripsi password menggunakan PASSWORD_DEFAULT.
Session Security: Validasi session untuk autentikasi.
File Upload Security: Validasi tipe file dan lokasi penyimpanan.
Access Control: Filter auth untuk melindungi halaman admin.
SQL Injection Prevention: Menggunakan Query Builder CodeIgniter.

Best Practices

Separation of Concerns: Pemisahan logic sesuai pola MVC.
Code Reusability: Menggunakan model dan helper yang reusable.
User Experience: Validasi form dengan flash messages.
Responsive Design: CSS yang mendukung tampilan mobile.
Clean Code: Struktur kode yang rapi dan mudah dipahami.


Kontribusi
Jika Anda ingin berkontribusi pada proyek ini:

Fork repository ini.
Buat branch baru (git checkout -b feature/nama-fitur).
Commit perubahan Anda (git commit -m 'Menambahkan fitur X').
Push ke branch (git push origin feature/nama-fitur).
Buat Pull Request.


Lisensi
Proyek ini dilisensikan di bawah MIT License.

Kontak
Jika Anda memiliki pertanyaan atau membutuhkan bantuan, silakan buat issue di repository ini.
