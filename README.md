# Altryu Corps – Website Penjualan Alat Pancing

Website dinamis berbasis **Laravel 13** untuk usaha UMKM **Altryu Corps**, yang menjual alat pancing dan perlengkapannya secara online.

## Fitur

| Kebutuhan | Implementasi |
|---|---|
| Project Laravel yang berjalan | `php artisan serve` (Laravel 13, PHP 8.3+) |
| Migrasi minimal 2 tabel berelasi | `categories` 1 → banyak `products` (`2026_11_26_000001`, `..._000002`) |
| Model Eloquent + pengambilan data dari controller | `Category`, `Product`, relasi `hasMany`/`belongsTo` |
| Halaman publik daftar & detail | `/produk`, `/produk/{slug}`, beranda, `/tentang` |
| Halaman admin CRUD | `/admin/kategori`, `/admin/produk` (tambah, ubah, hapus, daftar) |
| Upload foto produk | disimpan di `storage/app/public/products` |
| Validasi form sisi server | `app/Http/Requests/Admin/*` (wajib diisi, maksimal karakter, tipe data) |
| Tampilan responsif | Bootstrap 5 + `public/css/app.css` |
| Seeder minimal 5 data contoh | 4 kategori, 9 produk, 1 admin |

## Profil Usaha

Nama dan data usaha ada di `config/usaha.php` dan dapat diubah lewat `.env` (`USAHA_*`).

- **Nama:** Altryu Corps
- **Deskripsi:** usaha UMKM penjualan alat pancing dan perlengkapannya secara online (joran, reel, umpan & lure, aksesoris).

## Instalasi

Prasyarat: PHP 8.3+ (dengan ekstensi `sqlite3`, `mbstring`, `xml`, `curl`, `zip`, `bcmath`, `intl`, `gd`), dan Composer.

```bash
composer install
cp .env.example .env
php artisan key:generate
touch database/database.sqlite          # jika belum ada
php artisan migrate --seed
php artisan storage:link
php artisan serve
```

Buka **http://127.0.0.1:8000**.

### Akun admin (dari seeder)

- URL: http://127.0.0.1:8000/admin/login
- Email: `admin@altryu.test`
- Kata sandi: `admin12345`

Ganti kata sandi ini sebelum website dipublikasikan.

## Pengujian

```bash
php artisan test
```

Test mencakup halaman publik, login admin, CRUD kategori dan produk, validasi form, dan upload/hapus foto.

## Struktur Penting

```
app/Http/Controllers/        HomeController, ProductCatalogController, Admin/*, Auth/LoginController
app/Http/Requests/Admin/     Validasi CategoryRequest & ProductRequest
app/Models/                  Category, Product, Concerns/HasSlug
database/migrations/         categories, products
database/seeders/            Admin, Category, Product (+ sample-images/)
resources/views/             layouts, public, admin, auth, partials
public/css/app.css           Gaya tambahan (tema Altryu Corps)
public/images/               logo.svg, logo-icon.svg
config/usaha.php             Profil usaha
```

## Catatan

- Gambar contoh produk di `database/seeders/sample-images/` adalah ilustrasi sederhana. Ganti dengan foto produk asli lewat menu Admin → Produk.
- Pesan WhatsApp memakai nomor `USAHA_WHATSAPP` di `.env` (nilai awal adalah contoh; ubah ke nomor usaha yang sebenarnya).
- Alamat usaha (`USAHA_ALAMAT`) masih placeholder dan perlu diisi.
