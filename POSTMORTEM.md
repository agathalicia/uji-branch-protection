# Blameless Postmortem - Insiden Kegagalan Deployment Manual

## Ringkasan Insiden
Deployment aplikasi dilakukan secara manual sehingga proses membutuhkan beberapa langkah yang harus dilakukan satu per satu. Dalam prosesnya terjadi kegagalan deployment karena adanya langkah konfigurasi yang terlewat atau tidak konsisten. Insiden ini menunjukkan bahwa proses manual memiliki risiko kesalahan yang lebih tinggi dibandingkan proses yang sudah diotomatisasi.

## Kronologi (timeline)
1. Developer menyelesaikan kode aplikasi.
2. Hasil pekerjaan diserahkan kepada tim Operations.
3. Tim Operations menyiapkan lingkungan deployment secara manual.
4. Beberapa konfigurasi dan dependensi diperiksa dan dijalankan secara manual.
5. Deployment mengalami kegagalan karena konfigurasi belum sesuai.
6. Dilakukan pemeriksaan dan perbaikan konfigurasi.
7. Deployment dijalankan kembali hingga berhasil.
8. Setelah proses manual dievaluasi, dibuat `setup.sh` untuk mengotomatisasi proses setup dan deployment.

## Dampak (waktu terbuang, jumlah kegagalan)
Kegagalan deployment menyebabkan waktu tambahan digunakan untuk melakukan pengecekan, mencari penyebab kesalahan, dan mengulangi proses deployment. Selain itu, proses manual meningkatkan kemungkinan terjadinya kegagalan yang sama pada deployment berikutnya.

## Akar Masalah pada SISTEM (bukan pada orang)
Akar masalah berasal dari proses deployment yang masih dilakukan secara manual dan belum memiliki otomatisasi untuk menjalankan langkah konfigurasi secara konsisten. Dokumentasi dan validasi terhadap setiap langkah juga belum terintegrasi dalam satu proses sehingga kesalahan konfigurasi lebih mudah terjadi.

## Tindakan Perbaikan (action items) + penanggung jawab peran
- Membuat `setup.sh` untuk mengotomatisasi proses setup — **Developer**
- Menambahkan pemeriksaan dependensi dan konfigurasi sebelum deployment — **Developer**
- Melakukan pengujian script pada lingkungan yang sesuai sebelum digunakan — **Developer & Operations**
- Menyimpan script deployment di GitHub agar perubahan dapat dilacak — **Developer**
- Menggunakan proses deployment otomatis untuk mengurangi langkah manual — **Operations**

## Pelajaran yang Diambil
Proses deployment manual memiliki risiko kesalahan dan membutuhkan waktu lebih banyak karena setiap langkah harus dilakukan secara terpisah. Otomatisasi menggunakan script dapat membuat proses lebih konsisten, mengurangi pekerjaan berulang, dan mempermudah proses deployment. Insiden juga menunjukkan pentingnya dokumentasi, validasi, dan kolaborasi antara Developer dan Operations.
