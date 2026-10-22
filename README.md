# 🐝 Bee-SMART Course — versi GitHub Pages

Folder ini adalah **tampilan** aplikasi Bee-SMART Course yang di-hosting di GitHub Pages.
Data, login, foto, dan PDF tetap diproses oleh **Web App Google Apps Script** Anda:

```
https://script.google.com/macros/s/AKfycbxSgawROEN0mg8IWZc7JlXYsrBZEWRY3EKo1szKqScj3OpOA_toTicl48LZPkDFkiRy/exec
```

Keuntungannya: alamat lebih rapi, tanpa bar abu-abu "created by a Google Apps Script user", layar penuh berfungsi penuh, dan muncul ikon + pratinjau saat link dibagikan.

## Isi folder

| File | Fungsi |
|---|---|
| `index.html` | Seluruh aplikasi (tampilan + logika) dalam satu file |
| `favicon.png`, `apple-touch-icon.png`, `icon-512.png` | Ikon di tab browser dan layar utama HP |
| `og-image.png` | Gambar pratinjau saat link dibagikan di WhatsApp |
| `manifest.webmanifest` | Agar bisa "Tambahkan ke Layar Utama" seperti aplikasi |
| `.nojekyll` | Supaya GitHub menampilkan file apa adanya (opsional) |

---

## A. Perbarui server Google (WAJIB, sekali saja)

Versi GitHub butuh jalur API baru (`doPost`) di `Code.gs`.

1. Buka editor Apps Script proyek Bee-SMART.
2. Ganti seluruh isi **`Code.gs`** dengan file `Code.gs` versi 1.2 (dikirim terpisah).
3. (Disarankan) Ganti juga isi **`Js`** dengan `Js.html` versi 1.2 agar versi Google ikut sama.
4. Tekan **Ctrl + S**.
5. Klik **Deploy ▸ Manage deployments**.
6. Pilih deployment yang sudah ada ▸ klik ikon **✏️ (Edit)**.
7. Pada **Version** pilih **New version** ▸ klik **Deploy**.

> ⚠️ Gunakan **Manage deployments**, bukan *New deployment*. Dengan begitu URL `/exec` tetap sama.
> Jika terlanjur membuat deployment baru (URL berubah), buka `index.html`, cari `window.BEE_API`, dan ganti alamatnya.

Pastikan pengaturan deployment tetap: **Execute as: Me** dan **Who has access: Anyone**.

## B. Unggah ke GitHub

1. Masuk ke **github.com** ▸ klik **＋ ▸ New repository**.
2. **Repository name**: misalnya `beesmart` ▸ pilih **Public** ▸ klik **Create repository**.
3. Di halaman repo baru, klik tautan **uploading an existing file**.
4. Tarik (drag) **semua file** dari folder ini ke halaman tersebut.
5. Klik **Commit changes**.
6. Buka tab **Settings ▸ Pages** (menu kiri).
7. Pada **Source** pilih **Deploy from a branch**, lalu **Branch: main** dan folder **/ (root)** ▸ **Save**.
8. Tunggu 1–2 menit, lalu muat ulang halaman Settings ▸ Pages. Alamat situs muncul di atas, misalnya:
   `https://namapengguna.github.io/beesmart/`

## C. Uji

1. Buka alamat GitHub Pages Anda.
2. Halaman depan tampil, lalu nama, alamat, dan jam operasional dimuat dari server.
3. Masuk dengan akun Super Admin / admin seperti biasa.

Alamat Web App Google yang lama **tetap berfungsi** sebagai cadangan.

## D. (Opsional) Pratinjau gambar di WhatsApp

WhatsApp membutuhkan alamat gambar lengkap. Setelah situs aktif, buka `index.html` di GitHub (ikon ✏️), cari baris:

```html
<meta property="og:image" content="og-image.png">
```

lalu ganti menjadi alamat lengkap, misalnya:

```html
<meta property="og:image" content="https://namapengguna.github.io/beesmart/og-image.png">
```

Klik **Commit changes**.

## E. Memperbarui di kemudian hari

- **Perubahan data / pengaturan** (nama, alamat, rekening, deskripsi): cukup lewat menu **Pengaturan** di aplikasi. Tidak perlu menyentuh GitHub.
- **Perubahan kode server** (`Code.gs`): ubah di editor Apps Script ▸ **Manage deployments ▸ ✏️ ▸ New version**.
- **Perubahan tampilan** (`Index`, `Css`, `Js`): `index.html` di GitHub perlu dibuat ulang dari ketiga file itu, lalu diunggah ulang (timpa file lama).

## F. Jika ada masalah

| Pesan | Penyebab & solusi |
|---|---|
| *Gagal terhubung ke server* | Koneksi internet, atau deployment belum **Anyone**. Periksa Manage deployments. |
| *Respons server tidak valid…* | `Code.gs` di Google belum versi 1.2 atau belum **New version**. Ulangi bagian A. |
| Halaman GitHub 404 | Pages belum aktif atau masih memproses. Tunggu 2 menit, cek Settings ▸ Pages. |
| Tampilan lama setelah update | Tekan **Ctrl + Shift + R** untuk memuat ulang tanpa cache. |

## Catatan keamanan

- Jangan unggah `Code.gs` ke repo **Public**. File ini tidak diperlukan di GitHub dan berisi kata sandi bawaan untuk pemulihan.
- Semua pemeriksaan login dan hak akses tetap dilakukan di server Google, jadi kode tampilan yang terbuka di GitHub tidak membuka akses ke data.
