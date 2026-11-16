# SILOLI - Sistem Informasi Laundry dan Linen di RSD Madani Pekanbaru

> Rancang Bangun Sistem Informasi Laundry dan Linen Menggunakan Metode Waterfall
> Laporan Kerja Praktek | Program Studi Sistem Informasi, Universitas Riau | 2024
> Lokasi: RSD Madani Pekanbaru, Bagian Laundry dan Linen

## 1. Gambaran Proyek

SILOLI adalah sistem informasi berbasis web yang dibuat untuk membantu Bagian Laundry dan Linen di RSD Madani Pekanbaru dalam mencatat, memantau, dan melaporkan kegiatan laundry dan linen rumah sakit.

Sebelum ada sistem ini, pencatatan dilakukan secara manual dan tersebar. Akibatnya, stok linen sulit dipantau, riwayat pencucian sulit dilacak, dan laporan harus direkap ulang setiap kali dibutuhkan.

Sistem ini dibuat sebagai bagian dari Kerja Praktek. Fokusnya bukan membuat sistem yang paling canggih, tapi membuat sistem yang jelas alurnya, mudah dipakai petugas, dan datanya bisa dipertanggungjawabkan.

**Status kode saat ini:** Kode asli dari masa Kerja Praktek sudah hilang. Yang tersisa adalah laporan lengkap 38 halaman, screenshot antarmuka, dan diagram perancangan. Repo ini berisi versi publik dari laporan tersebut yang sudah disensor dari data pribadi, plus rencana rebuild versi mini dengan data dummy.

Repo ini dibuat dengan jujur. Tidak ada klaim bahwa kode di sini adalah kode asli dari 2024. Yang ada di sini adalah bukti kerja, cara berpikir, dan versi rebuild yang bisa didemo.

---

## 2. Latar Belakang dan Masalah

Rumah sakit memakai linen setiap hari untuk pasien, ruang operasi, dan ruang perawatan. Linen itu harus dicuci, disetrika, didistribusikan, dan dicatat. Kalau pencatatan berantakan, dampaknya langsung ke pelayanan.

Masalah yang ditemukan saat observasi:

1. Pencatatan laundry masih manual, sehingga mudah salah hitung dan hilang.
2. Stok linen yang bersih dan yang sedang dicuci tidak terpantau secara real time.
3. Petugas sulit mencari riwayat pencucian linen untuk satu ruangan tertentu.
4. Laporan untuk atasan harus direkap manual, sehingga lama dan rawan salah.
5. Tidak ada batas akses yang jelas, siapa yang boleh input dan siapa yang boleh lihat laporan.

Dari masalah itu, kebutuhan sistemnya menjadi jelas. Sistem harus bisa input data laundry, membedakan status linen, menampilkan stok, dan menghasilkan laporan yang bisa diunduh dan dipertanggungjawabkan.

---

## 3. Solusi yang Dibangun

Solusi yang dibangun adalah aplikasi web internal untuk Bagian Laundry dan Linen.

Prinsip yang dipakai:

1. **Satu pintu input:** Semua data laundry masuk lewat satu form yang sama, biar tidak ada versi pencatatan yang beda-beda.
2. **Status yang jelas:** Setiap linen punya status yang bisa dilacak, misalnya sedang dicuci, sudah bersih, dan sudah didistribusikan.
3. **Dashboard yang langsung kebaca:** Petugas dan atasan bisa langsung lihat kondisi hari itu tanpa harus buka banyak menu.
4. **Laporan yang siap pakai:** Laporan bisa dilihat di sistem dan tidak perlu direkap ulang di spreadsheet.
5. **Hak akses dibedakan:** Admin, petugas, dan atasan tidak punya akses yang sama.

Metode pengembangan yang dipakai adalah **Waterfall**. Alasannya sederhana. Kebutuhan di awal sudah cukup jelas dari hasil observasi dan wawancara, jadi alurnya dibuat berurutan: analisis, perancangan, implementasi, pengujian, dan pemeliharaan.

---

## 4. Pengguna dan Hak Akses

Sistem ini dirancang untuk 3 peran utama.

### 4.1. Admin

Admin adalah pengelola sistem. Tugasnya mengelola data master, mengelola akun petugas, dan memastikan data tidak berantakan.

Yang boleh dilakukan Admin:
- Kelola data pengguna dan hak akses.
- Kelola data master seperti jenis linen, ruangan, dan kategori laundry.
- Lihat semua laporan dan semua riwayat.
- Perbaiki data yang salah input.

### 4.2. Petugas Laundry

Petugas adalah pengguna harian. Tugasnya input data laundry yang masuk, update status pencucian, dan input hasil distribusi.

Yang boleh dilakukan Petugas:
- Input data laundry yang masuk.
- Update status dari sedang dicuci menjadi sudah bersih.
- Input distribusi linen ke ruangan.
- Lihat riwayat yang dia input.

Yang tidak boleh dilakukan Petugas:
- Menghapus data yang sudah masuk tanpa persetujuan Admin.
- Melihat laporan keuangan atau laporan yang bukan tugasnya.
- Mengubah data master tanpa izin.

### 4.3. Atasan atau Kepala Bagian

Atasan adalah pengguna yang memantau. Tugasnya melihat kondisi keseluruhan dan mengambil keputusan.

Yang boleh dilakukan Atasan:
- Lihat dashboard dan laporan.
- Lihat riwayat per ruangan dan per periode.
- Unduh laporan untuk rapat.

Yang tidak boleh dilakukan Atasan:
- Mengubah data input petugas. Kalau ada yang salah, Atasan minta Admin yang memperbaiki.

Pembagian ini penting. Di sistem yang datanya sensitif, tidak semua orang boleh lihat semua dan ubah semua.

---

## 5. Fitur Utama

### 5.1. Login dan Autentikasi

- Form login dengan username dan password.
- Validasi jika username atau password salah.
- Session berakhir otomatis jika tidak ada aktivitas.
- Password tidak disimpan dalam bentuk yang bisa dibaca langsung.

### 5.2. Dashboard

Dashboard menampilkan ringkasan yang langsung kebaca tanpa harus membuka banyak menu.

Isi dashboard:
- Jumlah laundry yang masuk hari ini.
- Jumlah linen yang sedang dicuci.
- Jumlah linen yang sudah bersih dan siap distribusi.
- Jumlah linen yang sudah didistribusikan.
- Daftar aktivitas terbaru.

Tujuan dashboard bukan pamer grafik. Tujuannya petugas tahu dalam 10 detik, hari ini ada apa saja yang belum beres.

### 5.3. Manajemen Data Laundry

Ini fitur inti. Petugas input data laundry yang masuk dari ruangan.

Data yang diinput:
- Tanggal masuk.
- Asal ruangan.
- Jenis linen.
- Jumlah.
- Keterangan kondisi awal.
- Petugas yang menerima.

Setelah diinput, data langsung masuk ke daftar dan statusnya tercatat sebagai sedang diproses.

### 5.4. Update Status Pencucian

Setelah dicuci, petugas update statusnya.

Alur status yang dipakai:
1. Diterima.
2. Sedang dicuci.
3. Sudah bersih.
4. Sudah didistribusikan.

Setiap perubahan status tercatat tanggal dan petugasnya. Jadi kalau ada yang bertanya, linen ini ke mana, riwayatnya bisa dilacak.

### 5.5. Distribusi Linen

Setelah bersih, linen didistribusikan ke ruangan yang meminta.

Data distribusi yang dicatat:
- Tanggal distribusi.
- Ruangan tujuan.
- Jenis dan jumlah linen yang dikirim.
- Petugas yang mengirim.

### 5.6. Laporan

Laporan bisa dilihat berdasarkan periode dan ruangan.

Jenis laporan:
- Laporan laundry masuk per periode.
- Laporan linen bersih per periode.
- Laporan distribusi per ruangan.
- Laporan stok linen.

Laporan ini yang dipakai Atasan untuk rapat, bukan rekap manual lagi.

### 5.7. Manajemen Data Master

Admin mengelola data yang dipakai berulang-ulang, seperti:
- Data ruangan.
- Data jenis linen.
- Data kategori laundry.
- Data pengguna.

Dengan data master yang rapi, input harian jadi lebih cepat dan lebih konsisten.

---

## 6. Alur Sistem

### 6.1. Alur Petugas Harian

1. Petugas login.
2. Petugas buka menu input laundry.
3. Petugas isi form sesuai linen yang masuk.
4. Sistem simpan dan tampilkan di daftar dengan status Diterima.
5. Setelah dicuci, petugas ubah status menjadi Sudah Bersih.
6. Setelah dikirim, petugas input distribusi dan status berubah menjadi Sudah Didistribusikan.
7. Atasan bisa lihat semua riwayat itu di dashboard dan laporan.

### 6.2. Alur Jika Ada Kesalahan Input

1. Petugas sadar ada salah input.
2. Petugas lapor ke Admin, tidak langsung hapus sendiri.
3. Admin cek riwayat dan perbaiki dengan catatan.
4. Perbaikan tercatat, jadi tidak ada data yang hilang tanpa jejak.

Alur ini sengaja dibuat kaku. Di sistem rumah sakit, data yang dihapus diam-diam itu lebih berbahaya daripada data yang salah tapi ketahuan.

---

## 7. Teknologi yang Dipakai

- **Bahasa:** PHP
- **Framework:** Laravel
- **Database:** MySQL
- **Frontend:** HTML, CSS, JavaScript, Blade Template Laravel
- **Metode:** Waterfall
- **Perancangan:** Use Case Diagram, Activity Diagram, Entity Relationship Diagram, dan Flowchart
- **Pengujian:** Black Box Testing

Alasan pilih Laravel dan MySQL sederhana. Laravel sudah punya sistem login, routing, dan validasi yang rapi. MySQL sudah cukup untuk data laundry yang strukturnya jelas dan relasinya tidak terlalu kompleks.

---

## 8. Perancangan Database, Gambaran Umum

Database dirancang dengan prinsip satu data dicatat satu kali, lalu dipakai di banyak tempat.

Tabel utama yang dipakai, gambaran umum:

- **users:** Menyimpan akun Admin, Petugas, dan Atasan, beserta peran dan status aktif.
- **ruangan:** Menyimpan daftar ruangan yang memakai layanan laundry.
- **jenis_linen:** Menyimpan daftar jenis linen, misalnya sprei, selimut, dan handuk.
- **laundry:** Menyimpan data utama laundry yang masuk, termasuk tanggal, ruangan asal, jumlah, dan status.
- **distribusi:** Menyimpan data pengiriman linen yang sudah bersih ke ruangan.
- **laporan:** Bukan tabel terpisah, tapi hasil olahan dari tabel laundry dan distribusi berdasarkan periode.

Relasi yang dipakai:
- Satu ruangan bisa punya banyak data laundry.
- Satu jenis linen bisa muncul di banyak data laundry.
- Satu data laundry punya satu riwayat status yang bisa berubah.
- Satu data laundry bisa punya satu data distribusi setelah bersih.

Detail lengkap ada di laporan, di bagian ERD. Di repo ini, diagram yang ditampilkan sudah versi ringkas tanpa data asli.

---

## 9. Cara Berpikir Web Developer di Proyek Ini

Ini bagian yang paling penting buat yang baca repo ini sebagai portfolio junior.

Sebelum ngoding, pertanyaan yang dipakai:

1. **Siapa yang pakai:** Apakah ini Admin, Petugas, atau Atasan. Karena tiap peran boleh lihatnya beda.
2. **Data apa yang masuk:** Apa yang diinput petugas, apa yang wajib diisi, apa yang boleh kosong.
3. **Apa yang harus terjadi:** Kalau petugas klik simpan, apa yang harus tampil. Kalau data kosong, apa yang harus tampil.
4. **Apa yang bisa salah:** Kalau petugas isi jumlah dengan huruf, kalau internet putus di tengah input, kalau ada yang iseng ganti ID di URL, sistem harus ngapain.
5. **Kalau aku jadi orang jahat, bisa tidak aku bobol ini:** Bisa tidak user biasa melihat laporan Admin cuma dengan ganti ID di URL. Bisa tidak user biasa menghapus data orang lain.

Setelah ngoding, pertanyaan tambahannya:

1. **Apakah data pribadi ikut ke tampil:** Kalau cuma butuh nama ruangan, jangan tampilkan data pegawai yang tidak perlu.
2. **Apakah ada kunci yang ikut ke upload:** Password database dan kunci lain tidak boleh ikut ke kode yang diupload.
3. **Apakah screenshot yang dipakai aman:** Screenshot yang dipakai di laporan dan portfolio tidak boleh berisi data asli.

Cara berpikir ini yang dipakai di SILOLI, bukan cuma cara ngodingnya.

---

## 10. Hasil dan Bukti

Hasil dari proyek ini:

1. Sistem berhasil dibuat dan diuji dengan Black Box Testing. Semua menu utama yang diuji dinyatakan berhasil dan sesuai dengan yang dirancang.
2. Petugas tidak perlu lagi rekap manual untuk laporan harian, karena laporan sudah bisa dilihat di sistem.
3. Riwayat laundry bisa dilacak per ruangan dan per periode, tidak perlu cari di tumpukan kertas.
4. Ada pembagian hak akses yang jelas, sehingga tidak semua orang bisa ubah semua data.

Bukti yang tersisa:
- Laporan Kerja Praktek 38 halaman, versi publik yang sudah disensor.
- Screenshot antarmuka login, dashboard, input, dan laporan.
- Diagram perancangan, termasuk Use Case dan ERD versi ringkas.

Bukti yang tidak ada:
- Kode asli dari 2024. Kode tersebut sudah hilang. Repo ini tidak mengklaim bahwa kode di sini adalah kode asli.

---

## 11. Cara Rebuild Versi Mini dari Laporan

Karena kode asli hilang, cara paling jujur adalah rebuild versi mini dari laporan dengan data dummy.

Langkah rebuild yang disarankan:

1. Buat project Laravel baru.
2. Buat tabel users, ruangan, jenis_linen, laundry, dan distribusi sesuai gambaran di bagian 8.
3. Buat autentikasi dengan 3 peran, Admin, Petugas, dan Atasan.
4. Buat fitur input laundry dengan validasi jumlah harus angka dan tanggal wajib diisi.
5. Buat fitur update status dengan 4 status, Diterima, Sedang Dicuci, Sudah Bersih, Sudah Didistribusikan.
6. Buat dashboard yang menampilkan jumlah per status hari ini.
7. Buat halaman laporan yang bisa difilter per periode dan per ruangan.
8. Isi database dengan data dummy, misalnya Ruangan A, Ruangan B, dan jenis linen palsu. Jangan pakai data asli rumah sakit.
9. Uji dengan Black Box, coba input salah, coba akses halaman Admin sebagai Petugas, dan pastikan ditolak.

Target rebuild bukan 100 persen sama dengan asli. Targetnya 3 fitur inti jalan: input, update status, dan laporan.

---

## 12. Struktur Repo yang Disarankan

```
siloli-laundry-linen-rsd-madani/
  README.md
  docs/
    LAPORAN-SILOLI-Versi-Publik.pdf
  screenshots/
    01-login.png
    02-dashboard.png
    03-input-laundry.png
    04-laporan.png
  rebuild-mini/
    README-Rebuild.md
```

Aturan:
- File PDF di folder docs adalah versi publik yang sudah disensor.
- File screenshot tidak boleh berisi nama pegawai asli, nomor induk pegawai, atau data pasien.
- File rebuild, jika ada, harus pakai data dummy.

---

## 13. Pelajaran yang Didapat

1. Sistem yang bagus itu bukan yang fiturnya paling banyak, tapi yang alurnya paling jelas buat petugas.
2. Hak akses itu bukan tambahan. Di sistem rumah sakit, hak akses itu bagian dari keamanan.
3. Data yang dihapus diam-diam lebih berbahaya daripada data yang salah tapi ketahuan. Karena itu, perbaikan harus tercatat.
4. Laporan itu sama pentingnya dengan kode. Saat kode hilang, laporan yang menyelamatkan bukti kerja.
5. Backup itu bukan opsional. Sejak proyek ini, semua project baru langsung di-push ke GitHub dari hari pertama, dan laporan disimpan di 2 tempat.

---

## 14. Catatan Privasi dan Etika Data

- Repo ini tidak berisi data pasien, data pegawai asli, nomor induk pegawai, atau password asli.
- Struktur organisasi yang ada di laporan asli sudah disensor di versi publik.
- Foto kegiatan yang ada di laporan asli tidak diupload ulang jika menampilkan wajah pegawai tanpa izin.
- Jika ada yang menemukan data sensitif di repo ini, mohon hubungi pemilik repo agar segera dihapus.

---

## 15. Kontak

- Nama: Muhammad Sulthan Muqsith Afif
- Peran: Junior Web Developer, fokus Laravel dan React
- Pendidikan: S1 Sistem Informasi, Universitas Riau
- GitHub: https://github.com/sulthanafif
- LinkedIn: https://www.linkedin.com/in/sulthanafif

Jika ada yang ingin diskusi soal sistem ini, silakan hubungi lewat GitHub atau LinkedIn. Saya lebih nyaman diskusi lewat tulisan dan dokumen, bukan telepon dadakan.
