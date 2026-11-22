# SIGAP SARPRAS SD — Paket Perbaikan Terpadu

Paket ini menyatukan frontend GitHub Pages dan backend Google Apps Script agar memakai endpoint yang sama.

## Temuan pada versi aktif

1. `app.html` yang dipublikasikan memiliki beberapa string JavaScript yang terputus oleh baris baru di dalam tanda petik tunggal. Kondisi ini dapat menyebabkan seluruh blok JavaScript gagal diparse, sehingga login lanjutan, tombol, formulir, dan fitur lain tidak berjalan.
2. URL Apps Script pada paket sebelumnya berbeda dari URL yang digunakan repository aktif. Frontend dan backend harus menunjuk ke deployment yang sama.
3. Backend perlu toleransi terhadap variasi kapitalisasi status akun dan status Draft lama. Ada pula kondisi saat Admin menyimpan status `Diterima` untuk laporan yang sudah `Diterima` yang sebelumnya bisa ditolak oleh pemeriksaan status.

## Isi paket

- `index.html` — halaman awal; statistik publik terhubung ke Apps Script aktif.
- `app.html` — aplikasi setelah login; sintaks JavaScript diperbaiki, tombol aksi ditampilkan segera sesuai role, dan status sesi kedaluwarsa ditangani.
- `Code.gs` — backend Apps Script berdasarkan file `Code(5).gs` yang diunggah, dengan normalisasi role/status, kompatibilitas Draft lama, perbaikan alur penerimaan Admin, dan penguncian saat membuat ID laporan.
- `CHECKLIST-UJI.md` — daftar uji berdasarkan alur SOP.

## URL Apps Script yang dipakai

`https://script.google.com/macros/s/AKfycbwicx0L8lGSUtnwYWLm8cXN4legFFaLYhlP_TtdtSTaymRAfw-lXn3v_2R2_fR0rXgL/exec`

URL tersebut sudah dipasang sama di `index.html` dan `app.html`. Jika Anda membuat deployment Apps Script baru dengan URL berbeda, ganti URL pada kedua file itu agar sama.

## Cara memasang

### A. Google Apps Script

1. Buka project Apps Script yang saat ini dipakai oleh aplikasi.
2. Salin/cadangkan kode lama terlebih dahulu.
3. Buka `Code.gs`, ganti isinya dengan file `Code.gs` dari paket ini, lalu simpan.
4. Pastikan project tetap terhubung ke spreadsheet yang saat ini menyimpan data SIGAP. Jangan membuat spreadsheet baru jika ingin mempertahankan data lama.
5. Jalankan `setupDatabase()` satu kali dari editor Apps Script dan berikan otorisasi yang diminta. Fungsi ini membuat sheet yang belum ada dan menambahkan header yang belum tersedia; tidak menghapus data lama.
6. Buka **Deploy → Manage deployments → Edit** pada deployment Web App yang digunakan aplikasi. Pilih **New version**, lalu Deploy.
7. Pertahankan URL `/exec` deployment yang sama. Jika URL berubah, perbarui konstanta `SHEETS_URL` di `app.html` dan `index.html`.
8. Untuk aplikasi GitHub Pages yang diakses pengguna melalui browser, Web App biasanya perlu disetel **Execute as: Me** dan **Who has access: Anyone**. Jangan mengubah setelan akses organisasi tanpa persetujuan administrator TI.

> Jangan menjalankan `migrateData()` kecuali memang ingin mengubah status kosong/`Belum` pada data lama menjadi `Draft`. Fungsi tersebut opsional.

### B. GitHub Pages

1. Ekstrak ZIP.
2. Pada repository `badungkab/sigapsarprasujicoba`, ganti `index.html` dan `app.html` dengan file dari paket.
3. Commit dan push ke branch yang dipakai GitHub Pages (umumnya `main`).
4. Tunggu proses GitHub Pages selesai, lalu buka `https://badungkab.github.io/sigapsarprasujicoba/`.
5. Lakukan hard refresh dengan `Ctrl + F5`. Jika browser masih menyimpan versi lama, coba jendela Incognito.

## Alur penggunaan

- **Operator Sekolah:** tombol Perekaman Laporan Kerusakan → isi formulir → Simpan Draft. Status tetap `Draft`.
- **Kepala Sekolah:** buka Laporan Kerusakan → daftar Draft → Validasi & Kirim atau Kembalikan dengan catatan.
- **Operator Sekolah:** perbaiki laporan yang dikembalikan → Simpan Perbaikan; status kembali `Draft` untuk divalidasi ulang.
- **Administrator/Tim Pengelola Data:** terima laporan berstatus `Terkirim ke Dinas`, pantau tindak lanjut, dan hapus laporan sesuai kewenangan.

## Catatan pengujian

Pemeriksaan yang sudah dilakukan pada paket: sintaks JavaScript frontend (`node --check`), sintaks backend (`node --check`), konsistensi URL Apps Script pada dua halaman, dan integritas arsip ZIP. Pengujian langsung ke spreadsheet dan akun produksi belum dapat dilakukan dari sini; lakukan checklist uji setelah deploy.

### Catatan tambahan perbaikan foto
Versi ini menormalkan tautan foto Google Drive ke endpoint thumbnail untuk tampilan tabel. Jika masih ada tulisan `Foto tidak tersedia`, periksa apakah file foto tersebut masih ada di Google Drive dan aksesnya mengizinkan siapa pun yang memiliki tautan untuk melihat. Foto lama tidak perlu diunggah ulang apabila file Drive aslinya masih tersedia dan dapat diakses.
