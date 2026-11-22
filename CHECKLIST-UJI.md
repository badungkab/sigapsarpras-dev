# Checklist Uji SIGAP SARPRAS SD

Lakukan setelah `Code.gs` di-deploy sebagai New version dan file GitHub Pages diperbarui.

## Persiapan

- [ ] Pastikan Apps Script terhubung ke spreadsheet SIGAP yang benar.
- [ ] Pastikan URL `/exec` di `index.html` dan `app.html` sama dengan deployment aktif.
- [ ] Pastikan akun Operator dan Kepala Sekolah berstatus aktif dan memiliki `sekolah_id` yang sesuai.
- [ ] Pastikan role akun adalah `operator`, `kepsek`, atau label yang dapat dinormalisasi oleh backend.
- [ ] Buka aplikasi dengan `Ctrl + F5`, lalu login ulang.

## Uji Operator Sekolah

- [ ] Menu Laporan Kerusakan tersedia.
- [ ] Tombol **PEREKAMAN LAPORAN KERUSAKAN** terlihat.
- [ ] Formulir menampilkan sekolah milik akun.
- [ ] Simpan satu laporan uji tanpa foto; respons sukses tampil.
- [ ] Baris baru muncul di sheet `LaporanKerusakan` dengan status `Draft`.
- [ ] Akun Operator tidak dapat menghapus laporan.

## Uji Kepala Sekolah

- [ ] Login dengan role Kepala Sekolah yang terhubung ke sekolah yang sama.
- [ ] Panel Daftar Persetujuan / Validasi Kepala Sekolah terlihat.
- [ ] Draft uji muncul di daftar.
- [ ] Klik **Kembalikan**, isi alasan; status berubah menjadi `Dikembalikan`.
- [ ] Operator dapat membuka dan memperbaiki laporan yang dikembalikan.
- [ ] Setelah disimpan ulang, status kembali menjadi `Draft`.
- [ ] Kepala Sekolah dapat klik **Validasi & Kirim**; status berubah menjadi `Terkirim ke Dinas`.

## Uji Administrator

- [ ] Laporan berstatus `Terkirim ke Dinas` menampilkan tombol **Terima di Dinas**.
- [ ] Setelah diterima, status berubah menjadi `Diterima`.
- [ ] Admin dapat memperbarui status `Diterima` menjadi `Dalam Proses`, lalu `Selesai`.
- [ ] Tombol **Hapus** berfungsi dan meminta konfirmasi.
- [ ] Aktivitas buat, validasi, pengembalian, penerimaan, perubahan status, dan penghapusan tercatat di `LogAktivitas`.

## Verifikasi data

- [ ] Data sekolah dan sarpras lama tetap ada.
- [ ] Data laporan lama tetap ada, kecuali laporan uji yang memang dihapus oleh Admin.
- [ ] Foto (jika diuji) tersimpan di folder Drive `SIGAP_SARPRAS_FOTO`.

Jika salah satu langkah gagal, catat pesan pada badge sinkronisasi di kanan bawah dan pesan alert yang muncul. Jangan menghapus sheet atau mengganti spreadsheet untuk mengatasi error.
