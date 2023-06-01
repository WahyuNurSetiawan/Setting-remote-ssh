# Setting & Remote Control(SSH) menggunakan Tremux dan Wsl Ubuntu
Remote control melalui SSH (Secure Shell) adalah proses mengakses dan mengendalikan sistem komputer yang terletak di lokasi fisik yang berbeda melalui jaringan. Dengan menggunakan koneksi SSH, Anda dapat terhubung ke komputer atau server yang jauh secara aman dan menjalankan perintah-perintah dari jarak jauh.

Berikut ini adalah beberapa kegunaan utama dari remote control melalui SSH:

1. Akses dan administrasi jarak jauh: Dengan SSH, Anda dapat mengakses dan mengendalikan sistem komputer dari jarak jauh tanpa harus berada di depan komputer fisiknya. Ini memungkinkan Anda untuk melakukan administrasi sistem, mengelola berkas dan direktori, menginstal dan memperbarui perangkat lunak, serta menjalankan perintah lainnya dengan mudah.

2. Konsolidasi dan manajemen server: SSH memungkinkan Anda untuk mengakses dan mengendalikan beberapa server dari satu lokasi. Dengan menggunakan koneksi SSH, Anda dapat mengelola dan mengkonfigurasi server secara efisien tanpa harus berpindah-pindah fisik ke setiap server secara terpisah.

3. Pemeliharaan dan pemecahan masalah: SSH memungkinkan administrator sistem untuk memelihara dan memperbaiki sistem dari jarak jauh. Anda dapat memantau sistem, menganalisis log, menjalankan skrip pemeliharaan, serta memperbaiki masalah yang mungkin timbul tanpa perlu berada di dekat komputer secara fisik.

4. Transfer berkas yang aman: Selain mengendalikan sistem, SSH juga memungkinkan Anda untuk mentransfer berkas antara komputer lokal dan jarak jauh melalui protokol SCP (Secure Copy) atau SFTP (SSH File Transfer Protocol). Ini memberikan cara yang aman untuk mengirim dan menerima berkas antara dua sistem.

5. Koneksi aman: Salah satu keunggulan utama SSH adalah keamanannya. Semua koneksi dan data yang dikirim melalui SSH dienkripsi, sehingga menjaga kerahasiaan dan integritas informasi yang dikirimkan. Hal ini sangat penting saat mengakses sistem yang berada di jaringan publik atau saat melakukan komunikasi melalui internet.

Remote control melalui SSH adalah alat yang kuat bagi administrator sistem dan pengguna yang membutuhkan akses jarak jauh ke sistem komputer. Ini memberikan kemampuan untuk mengelola dan mengontrol sistem dari mana saja, dengan tingkat keamanan yang tinggi.

## Setting awal Server
Untuk melakukan pengaturan dan koneksi jarak jauh (remote connection) melalui SSH pada Ubuntu Server, berikut adalah langkah-langkah yang dapat Anda ikuti:

Langkah 1: Menginstal OpenSSH Server
1. Buka terminal pada Ubuntu Server atau hubungkan ke server melalui koneksi shell seperti PuTTY.
2. Pastikan Anda memiliki akses root atau hak administrator.
3. Jalankan perintah berikut untuk menginstal OpenSSH Server:
   ```
   sudo apt update
   sudo apt install openssh-server
   ```

Langkah 2: Mengonfigurasi Firewall (jika diperlukan)
1. Jika Anda menjalankan firewall pada server, pastikan untuk membuka port SSH (biasanya port 22) agar dapat menerima koneksi.
2. Jalankan perintah berikut untuk membuka port SSH pada firewall menggunakan iptables:
   ```
   sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
   ```
   Jika Anda menggunakan UFW, Anda dapat menggunakan perintah berikut:
   ```
   sudo ufw allow 22
   ```

Langkah 3: Mengonfigurasi SSH
1. Buka file konfigurasi SSH menggunakan teks editor seperti nano atau vim:
   ```
   sudo nano /etc/ssh/sshd_config
   ```
2. Temukan baris yang berisi `#Port 22` dan hapus tanda pagar (`#`) di depannya jika ada. Jika Anda ingin menggunakan port selain 22, gantilah dengan port yang diinginkan.
3. Jika Anda ingin mengizinkan koneksi root melalui SSH, temukan baris yang berisi `PermitRootLogin` dan ubah nilainya menjadi `yes`. Namun, disarankan untuk membatasi akses root dan menggunakan akun pengguna terbatas.
4. Simpan perubahan yang Anda buat dan keluar dari editor.

Langkah 4: Restart SSH Service
1. Setelah mengonfigurasi SSH, restart layanan SSH agar perubahan dapat diterapkan:
   ```
   sudo service ssh restart
   ```

Langkah 5: Menggunakan Klien SSH untuk Koneksi Jarak Jauh
1. Dari komputer lokal, buka terminal atau klien SSH yang kompatibel.
2. Untuk terhubung ke server menggunakan SSH, gunakan perintah berikut:
   ```
   ssh username@alamat-ip-server
   ```
   Gantilah `username` dengan nama pengguna yang valid pada server Ubuntu, dan `alamat-ip-server` dengan alamat IP sesuai server Anda.
3. Jika ini adalah koneksi pertama kali ke server, Anda mungkin akan diminta untuk memverifikasi fingerprint SSH.
4. Setelah berhasil memasukkan pengguna dan kata sandi (atau menggunakan kunci SSH), Anda akan terhubung ke server secara jarak jauh melalui SSH.

## mengatur dan melakukan koneksi remote (SSH) antara Termux di perangkat Android dan WSL

Di Perangkat Android (Termux):
1. Pastikan Anda telah menginstal aplikasi Termux dari Google Play Store.

2. Buka aplikasi Termux di perangkat Android Anda.

3. Update paket-paket di Termux dengan menjalankan perintah berikut:
   ```
   pkg update
   ```

4. Install klien SSH di Termux dengan menjalankan perintah berikut:
   ```
   pkg install openssh
   ```

5. Setelah instalasi selesai, Anda dapat menggunakan perintah `ssh` untuk melakukan koneksi remote ke laptop WSL. Misalnya, jika IP laptop WSL adalah 192.168.1.100, Anda dapat menggunakan perintah berikut untuk melakukan koneksi SSH:
   ```
   ssh username@192.168.1.100
   ```
   Ganti `username` dengan nama pengguna yang Anda gunakan di laptop WSL.

6. Ketika diminta, masukkan kata sandi pengguna WSL Anda untuk autentikasi.

Setelah langkah-langkah di atas selesai, Anda harus terhubung melalui koneksi SSH antara Termux di perangkat Android dan WSL di laptop. Anda dapat menjalankan perintah-perintah Linux pada laptop WSL melalui Termux dan mengakses file-file yang ada di laptop melalui koneksi SSH.

Pastikan Anda memahami risiko keamanan yang terkait dengan mengaktifkan akses SSH ke sistem Anda dan pastikan Anda menjaga kata sandi pengguna WSL Anda dengan aman.

## Beberapa contoh yang bisa dilakukan remote control(ssh)
Berikut adalah beberapa contoh perintah yang dapat Anda lakukan melalui koneksi SSH:

1. Melihat informasi sistem:
   - `uname -a`: Menampilkan informasi kernel dan sistem operasi.
   - `lsb_release -a`: Menampilkan informasi rilis distribusi Linux.
   - `df -h`: Menampilkan penggunaan ruang disk.

2. Mengelola berkas dan direktori:
   - `ls`: Menampilkan daftar berkas dan direktori.
   - `cd <direktori>`: Berpindah ke direktori tertentu.
   - `pwd`: Menampilkan direktori saat ini.
   - `mkdir <nama_direktori>`: Membuat direktori baru.
   - `rm <nama_berkas>`: Menghapus berkas.
   - `cp <sumber> <tujuan>`: Menyalin berkas atau direktori.
   - `mv <sumber> <tujuan>`: Memindahkan atau mengganti nama berkas atau direktori.

3. Mengelola pengguna dan hak akses:
   - `whoami`: Menampilkan nama pengguna saat ini.
   - `id`: Menampilkan informasi ID pengguna dan grup.
   - `sudo <perintah>`: Menjalankan perintah dengan hak akses superuser.
   - `adduser <nama_pengguna>`: Membuat pengguna baru.
   - `passwd <nama_pengguna>`: Mengubah kata sandi pengguna.
   - `chmod <mode> <nama_berkas>`: Mengubah hak akses berkas.

4. Mengelola paket dan perangkat lunak:
   - `apt update`: Memperbarui daftar paket.
   - `apt upgrade`: Memperbarui paket yang terinstal.
   - `apt install <nama_paket>`: Menginstal paket baru.
   - `apt remove <nama_paket>`: Menghapus paket.

5. Menjalankan proses dan perintah:
   - `ps`: Menampilkan daftar proses yang berjalan.
   - `top`: Menampilkan tampilan dinamis dari proses yang berjalan.
   - `kill <pid>`: Menghentikan proses dengan ID proses (PID) tertentu.
   - `bg`: Menjalankan proses di latar belakang.
   - `fg`: Mengembalikan proses ke depan.

6. Menjelajah jaringan:
   - `ping <alamat_host>`: Memeriksa ketersediaan host dengan mengirim paket ICMP.
   - `traceroute <alamat_host>`: Melacak rute paket ke tujuan tertentu.
   - `ssh <nama_pengguna>@<alamat_host>`: Terhubung ke host lain melalui SSH.

Ini hanya sebagian kecil dari perintah yang bisa Anda lakukan melalui SSH. Ada banyak lagi perintah dan fungsionalitas yang tersedia di lingkungan Linux yang bisa dieksplorasi.
