Nama : Mochamad Gilang Fadil Hakim

NIM  : H1D022082

Shift : B

Komponen Login
Pada login.page.ts, terdapat fungsi login() yang memverifikasi input username dan password. Jika kedua input tidak kosong, data akan dikirim ke authService melalui metode postMethod, yang kemudian diarahkan ke login.php. Server akan merespons melalui res.status_login untuk memeriksa status login. Jika login berhasil, token dan username akan disimpan menggunakan saveData(), dan pengguna akan diarahkan ke halaman /home. Jika gagal, pesan kesalahan akan ditampilkan melalui notifikasi

Layanan Autentikasi (authentication.service.ts)
Layanan ini mengelola autentikasi dan status login pengguna menggunakan isAuthenticated, yang berbasis BehaviorSubject. Variabel ini menentukan status login di dalam aplikasi. Metode saveData() menyimpan token dan username pada Capacitor Preferences, sehingga pengguna tetap login hingga mereka melakukan logout. Saat aplikasi dibuka, loadData() akan memuat token dan username untuk memastikan status login tetap konsisten.

Guard dan Rute (app-routing.module.ts, auth.guard.ts, auto-login.guard.ts)
authGuard dan autoLoginGuard digunakan untuk membatasi akses ke halaman tertentu berdasarkan status login pengguna. authGuard mencegah akses ke halaman /home bagi pengguna yang belum login, sementara autoLoginGuard akan mengarahkan pengguna yang sudah login langsung ke halaman /home jika mereka mencoba mengakses halaman login.

Notifikasi Kesalahan dan Logout
Jika ada masalah koneksi atau kredensial tidak valid, notifikasi akan muncul untuk memberi tahu pengguna. Metode logout() akan menghapus token, username, dan status autentikasi pengguna, mengembalikan pengguna ke kondisi logout untuk meningkatkan keamanan.

Backend PHP (login.php, koneksi.php)
Script PHP di backend menerima data username dan password, melakukan hashing pada password, lalu membandingkannya dengan data di tabel pengguna pada database. Jika kredensial sesuai, server akan mengembalikan token berbasis waktu sebagai tanda keberhasilan autentikasi dan status_login sebagai "berhasil." Jika tidak sesuai, server mengembalikan status "gagal" tanpa token, memberi tahu pengguna bahwa login tidak berhasil.
