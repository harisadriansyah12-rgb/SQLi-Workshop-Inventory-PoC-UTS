# Eksploitasi SQL Injection pada Sistem Manajemen Inventaris Bengkel Jaya
Dokumentasi ini dibuat sebagai bagian dari pemenuhan tugas mata kuliah Keamanan
Informasi / Keamanan Siber.
## Informasi Mahasiswa
- **Nama:** [MASUKKAN NAMA ANDA]
- **NIM:** [MASUKKAN NIM ANDA]
- **Kelas:** [MASUKKAN KELAS ANDA]
- **Mata Kuliah:** [NAMA MATA KULIAH]
- **Dosen Pengampu:** [NAMA DOSEN]
---
## Deskripsi Proyek
Proyek ini membahas analisis kerentanan keamanan pada aplikasi inventaris
bengkel, khususnya pada celah SQL Injection. Meliputi tahap identifikasi,
eksploitasi (Proof of Concept), hingga tahap mitigasi/perbaikan kode.
## Daftar Isi
1. [Prasyarat](#prasyarat)
2. [Langkah Eksploitasi](#langkah-eksploitasi)
3. [Bukti Eksploitasi](#bukti-eksploitasi)
4. [Mitigasi Keamanan](#mitigasi-keamanan)
5. [Kesimpulan](#kesimpulan)
## Prasyarat
- Database MySQL/MariaDB
- PHP 7.4+ / XAMPP
- Browser (untuk pengujian payload)
## Langkah Eksploitasi
Detail langkah-langkah serangan mulai dari pencarian parameter rentan hingga
ekstraksi data user dapat dilihat pada artikel Medium berikut:
[Link Artikel Medium Anda]
## Bukti Eksploitasi
![Dashboard Inventaris](images/dashboard.png)
*Tangkapan layar sistem manajemen inventaris.*

## Mitigasi Keamanan
Pencegahan dilakukan dengan mengganti query SQL konvensional menjadi **Prepared
Statements**. Contoh kode yang aman tersedia di folder `src/`.
## Penutup
Eksploitasi ini dilakukan dalam lingkungan terkontrol untuk tujuan edukasi.
Penting bagi pengembang aplikasi untuk selalu memvalidasi input pengguna guna
mencegah serangan injeksi.

Langkah 2: Buat file bernama mitigasi.php di folder src/.

src/mitigasi.php
<?php
/**
* Contoh Kode Aman (Mencegah SQL Injection)
* Dibuat oleh: [NAMA ANDA]
*/
// Gunakan PDO (PHP Data Objects)
$host = 'localhost';
$db = 'bengkel_jaya';
$user = 'root';
$pass = '';
try {
$pdo = new PDO("mysql:host=$host;dbname=$db", $user, $pass);
// Menerima input dari form login
$username = $_POST['username'];
// MENGGUNAKAN PREPARED STATEMENTS
$stmt = $pdo->prepare('SELECT * FROM users WHERE username = :user');
$stmt->execute(['user' => $username]);
$user_data = $stmt->fetch();
if ($user_data) {
echo "Data ditemukan secara aman.";
}
} catch (PDOException $e) {
echo "Koneksi gagal: " . $e->getMessage();
}
?>
