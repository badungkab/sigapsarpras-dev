# Riwayat Perbaikan

- Mengganti URL Apps Script lama pada `index.html` dan `app.html` dengan URL deployment yang dipakai aplikasi aktif.
- Menggunakan frontend dengan string JavaScript yang sudah diperbaiki agar tidak ada literal string yang terputus oleh baris baru.
- Menampilkan tombol aksi Laporan Kerusakan segera setelah role pengguna diketahui, sebelum data selesai dimuat.
- Menangani sesi yang kedaluwarsa dengan meminta pengguna login kembali.
- Menormalisasi role dan status akun di backend, termasuk nilai `Aktif`/`aktif`.
- Mengizinkan status Draft lama yang dikenal SOP untuk diproses tanpa mengubah data lama secara massal.
- Memperbaiki alur Admin agar status `Diterima` yang sudah ada tetap dapat disimpan pada formulir monitoring.
- Menggunakan ScriptLock ketika membuat nomor laporan untuk menghindari nomor ID ganda saat dua laporan disimpan bersamaan.

## Perbaikan foto (20 November 2026)
- Tampilan foto pada dashboard, daftar laporan, validasi Kepala Sekolah, dan monitoring Admin kini menggunakan URL thumbnail Google Drive agar lebih stabil untuk elemen `<img>`.
- Tautan foto dinormalisasi dari format `uc?export=view&id=...`, `open?id=...`, maupun `/file/d/.../view`.
- Klik thumbnail membuka file pada halaman Google Drive.
- Jika file memang tidak dapat diakses, aplikasi menampilkan keterangan `Foto tidak tersedia` alih-alih ikon gambar rusak.
- Foto baru menyimpan tautan file Google Drive dalam format `/file/d/ID/view` dan tetap mengatur izin `Anyone with the link`.
